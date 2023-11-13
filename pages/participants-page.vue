<template>
  <NuxtLayout :name="custom">
    <div class="main">
      <div v-if="positiveResponse" class="participantsPageTable">
        <h1>УЧАСТНИКИ</h1>

        <div class="container">
          <table class="table">
            <thead>
              <tr>
                <th>№</th>
                <th>Команда</th>
                <th>Телеграм</th>
                <th>ID команды</th>
                <th>Капитан</th>
                <th>Группа</th>
                <th>Телефон</th>
                <th>Участников</th>
                <th>Время регистрации</th>
              </tr>
            </thead>
            <tbody id="rows"></tbody>
          </table>
        </div>
      </div>
      <div v-if="!positiveResponse" class="loginPageView">
        <ModalVue v-show="isModalVisible" v-on:close="closeModal">
          <template v-slot:header>
            {{ headerText }}
          </template>

          <template v-slot:body>
            <p>{{ bodyText }}</p>
          </template>

          <template v-slot:footer> </template>
        </ModalVue>
        <div class="form center">
          <div class="header center">ВВЕДИТЕ ПАРОЛЬ</div>

          <form class="btn_container center">
            <div class="block_input center">
              <input
                v-model="form.password"
                required
                class="input"
                type="text"
                placeholder="кек лол арбидол"
              />
            </div>

            <button type="button" class="reg_btn" v-on:click="buttonClicked">
              ВОЙТИ
            </button>
          </form>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script>
// import Vuetable from 'vuetable-2'

export default {
  components: {
    // Vuetable
  },
  data() {
    return {
      headerText: '',
      bodyText: '',
      isModalVisible: false,
      positiveResponse: false,
      form: {
        password: '',
      },
    }
  },
  methods: {
    buttonClicked() {
      this.postData('https://www.quiz-on.ru/api/registrations', this.form).then(
        (response) => {
          if (response.status === 200) {
            response.json().then((data) => {
              this.getParticipants(data)
            })
            this.positiveResponse = true
          } else {
            this.headerText = 'Ошибка!'
            this.bodyText = 'Неправильный пароль!'
            this.showModal()
          }
        }
      )
    },
    async postData(url, data) {
      try {
        const response = await fetch(url, {
          method: 'POST',
          mode: 'cors',
          cache: 'no-cache',
          credentials: 'same-origin',
          headers: {
            'Content-Type': 'application/json',
          },
          redirect: 'follow',
          referrerPolicy: 'no-referrer',
          body: JSON.stringify(data),
        })

        return response
      } catch (error) {
        this.headerText = 'Ошибка!'
        this.bodyText = 'Что-то пошло не так'
        this.showModal()
      }
    },
    getParticipants(data) {
      if (data.length > 0) {
        let temp = ''
        for (const itemData of data) {
          const teamId = itemData.team_id ?? ''

          temp +=
            "<tr style='height: 70px; border: solid; border-width: 0.2px 0; border-color: rgba(255, 255, 255, 0.5);'>"
          temp += "<td style='padding: 10px;'>" + itemData.number + '</td>'
          temp += "<td style='padding: 10px;'>" + itemData.team_name + '</td>'
          temp += "<td style='padding: 10px;'>" + itemData.tg_contact + '</td>'
          temp += "<td style='padding: 10px;'>" + teamId + '</td>'
          temp +=
            "<td style='padding: 10px;'>" + itemData.captain_name + '</td>'
          temp += "<td style='padding: 10px;'>" + itemData.group_name + '</td>'
          temp += "<td style='padding: 10px;'>" + itemData.phone + '</td>'
          temp += "<td style='padding: 10px;'>" + itemData.amount + '</td>'
          temp +=
            "<td style='padding: 10px;'>" + itemData.registered_at + '</td>'
        }
        document.getElementById('rows').innerHTML = temp
      }
    },
    showModal() {
      this.isModalVisible = true
    },
    closeModal() {
      this.isModalVisible = false
    },
  },
}
</script>

<style scoped>
.main {
  width: 100vw;
  padding-top: 2vh;
  padding-bottom: 2vh;
}
.participantsPageTable {
  width: 100%;
}
.loginPageView {
  width: 100%;
}
.form {
  width: 90vw;
  max-width: 405px;
  background-color: #1f354b;
  border-radius: 21px;
  box-shadow: 0px 0px 10px 5px rgba(0, 0, 0, 0.383);
}

.center {
  margin: 0 auto;
}

.header {
  padding-top: 17px;
  box-sizing: border-box;
  font-size: 24px;
  font-family: ProductSans;
  font-weight: 700;
  color: white;
  width: 80vw;
  max-width: 360px;
}

.block_input {
  margin-top: 11px;
  width: 80vw;
  height: 51px;
  max-width: 360px;
}
.reg_btn {
  margin-top: 20px;
  background-color: #182a3e;
  border: 1.33428px solid #f4da6a;
  border-radius: 17.3457px;
  width: 80vw;
  max-width: 360px;
  height: 35px;
  font-family: ProductSans;
  font-weight: 700;
  font-size: 17px;
  color: #ffffff;
  cursor: pointer;
}

.btn_container {
  width: 80vw;
  max-width: 360px;
  font-size: 12px;
  padding-bottom: 30px;
}


::placeholder {
  font-family: ProductSans;
  font-weight: 400;
  font-size: 12px;
  color: #ffffff33;
}

.input {
  padding: 8px;
  margin-top: 6px;
  box-sizing: border-box;
  width: 100%;
  max-width: 360px;
  height: 32px;
  border-radius: 12px;
  border-width: 2px;
  background-color: #182a3e;
  border-color: #ffffff33;
  color: #ffffff;
}

h1 {
  padding-bottom: 3vh;
  font-family: ProductSans;
  font-size: 36px;
  font-weight: 700;
  line-height: 36px;
  letter-spacing: 2px;
  text-align: center;
  color: white;
}
table {
  background: #0f1a2e;
  border-radius: 15px;
  border-collapse: collapse;
  margin: 0 auto;
}
th {
  font-family: ProductSans;
  font-size: 15px;
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 0px;
  text-align: left;
  color: #e0ac59;
  padding: 10px;
}
tbody {
  font-family: ProductSans;
  font-size: 15px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0px;
  text-align: left;
  color: white;
}
</style>
