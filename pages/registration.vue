<template>
  <div class="main">
    <ModalVue v-show="isModalVisible" v-on:close="closeModal">
      <template v-slot:header>
        {{ headerText }}
      </template>

      <template v-slot:body>
        <p>{{ bodyText }}</p>
        <p>{{ gameDate }}</p>
        <p>{{ gameLoc }}</p>
        <p>{{ seeYa }}</p>
      </template>

      <template v-slot:footer> </template>
    </ModalVue>
    <div class="form center">
      <div class="header center">РЕГИСТРАЦИЯ НА&nbspИГРУ</div>

      <div class="game_num center">6-я игра Бауманской лиги</div>

      <div class="info center">
        <div class="info_clock"><img src="../assets/images/clock.svg" /></div>
        <div class="info_text">21 февраля, СР 19:00</div>
      </div>

      <div class="info center">
        <div class="info_loc"><img src="../assets/images/location.svg" /></div>
        <div class="info_text">345 аудитория (ГУК МГТУ им. Н.Э. Баумана)</div>
      </div>
      <div class="info center">
        <div class="info_warn"><img src="../assets/images/warning.svg" /></div>
        <div class="info_text">Регистрируется только капитан команды</div>
      </div>

      <form class="btn_container center">
        <div class="block_input center">
          <div class="block_text">ИМЯ КАПИТАНА <span class="star">*</span></div>
          <input
            v-model="form.captain_name"
            :class="{ error: formFormatters.captainNameIsEmpty }"
            required
            class="input"
            type="text"
            placeholder="Николай Эрнестович Бауман"
          />
        </div>
        <div class="block_input center">
          <div class="block_text">
            УЧЕБНАЯ ГРУППА КАПИТАНА <span class="star">*</span>
          </div>
          <input
            v-model="form.group_name"
            :class="{ error: formFormatters.groupNameIsEmpty }"
            required
            class="input"
            type="text"
            placeholder="СМ1-11"
          />
        </div>

        <div class="block_input center">
          <div class="block_text">
            НОМЕР ТЕЛЕФОНА <span class="star">*</span>
          </div>
          <input
            v-model="form.phone"
            :class="{ error: formFormatters.phoneIsEmpty }"
            required
            class="input"
            type="text"
            placeholder="8(999)888-77-66"
          />
        </div>
        <div class="block_input center">
          <div class="block_text">TELEGRAM <span class="star">*</span></div>
          <input
            v-model="form.tg_contact"
            :class="{ error: formFormatters.tgContactIsEmpty }"
            required
            class="input"
            type="text"
            placeholder="@quizonmsk"
          />
        </div>
        <div class="block_input center">
          <div class="block_text">
            НАЗВАНИЕ КОМАНДЫ <span class="star">*</span>
          </div>
          <input
            v-model="form.team_name"
            :class="{ error: formFormatters.teamNameIsEmpty }"
            required
            class="input"
            type="text"
            placeholder="КвизON"
          />
        </div>
        <div class="block_input center">
          <div class="block_text">
            КОЛИЧЕСТВО ЧЕЛОВЕК <span class="star">*</span>
          </div>
          <input
            v-model="form.amount"
            :class="{ error: formFormatters.teamSizeIsEmpty }"
            required
            class="input"
            type="text"
            placeholder="6"
          />
        </div>
        <div class="block_input center">
          <div class="block_text">ID КОМАНДЫ</div>
          <input
            v-model="form.team_id"
            required
            class="input"
            type="text"
            placeholder="0002"
          />
        </div>
        <button type="button" class="reg_btn" v-on:click="buttonClicked">
          Зарегистрироваться
        </button>
        <div class="agreement">
          Отправляя свои данные, вы соглашаетесь на&nbsp<a
            href="https://bmstu.ru/about/obrabotka-dannyh"
            class="agreement_link"
            >обработку персональных данных</a
          >
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import ModalVue from '../components/ModalVue.vue'

export default {
  name: 'registration',
  components: { ModalVue },
  data() {
    return {
      canRegister: '',
      headerText: '',
      bodyText: '',
      gameDate: '',
      gameLoc: '',
      seeYa: '',
      isModalVisible: false,
      formFormatters: {
        captainNameIsEmpty: false,
        groupNameIsEmpty: false,
        phoneIsEmpty: false,
        teamNameIsEmpty: false,
        teamSizeIsEmpty: false,
        tgContactIsEmpty: false,
      },
      form: {
        tg_contact: '',
        team_id: '',
        captain_name: '',
        group_name: '',
        phone: '',
        team_name: '',
        amount: null,
      },
    }
  },
  beforeMount() {
    this.canRegister = this.checkIfCanRegister()
  },

  methods: {
    showModal() {
      this.isModalVisible = true
    },
    closeModal() {
      this.isModalVisible = false
    },
    async checkIfCanRegister() {
      try {
        const response = await fetch(
          'https://www.quiz-on.ru/api/register-available'
        )
        const resp = await response.json()
        const available = resp.available
        if (available === 'reserve') {
          this.headerText = 'Упс... 👉🏻👈🏻'
          this.bodyText =
            'К сожалению, места на\u00A0игру закончились. Но не стоит опускать руки раньше времени! Мы можем зарегистрировать твою команду в\u00A0резерв, чтобы в\u00A0случае отказа  от\u00A0какой-то из прошедших команд, вы могли занять их место. Хочешь зарегистрироваться в\u00A0резерв?'
          this.showModal()
        }
        return available
      } catch (error) {
        this.headerText = 'Ошибка!'
        this.bodyText = 'Что-то пошло не так'
        this.showModal()
      }
    },

    buttonClicked() {
      if (this.form.captain_name === '') {
        this.formFormatters.captainNameIsEmpty = true
      } else {
        this.formFormatters.captainNameIsEmpty = false
      }
      if (this.form.group_name === '') {
        this.formFormatters.groupNameIsEmpty = true
      } else {
        this.formFormatters.groupNameIsEmpty = false
      }
      if (this.form.phone === '') {
        this.formFormatters.phoneIsEmpty = true
      } else {
        this.formFormatters.phoneIsEmpty = false
      }
      if (this.form.team_name === '') {
        this.formFormatters.teamNameIsEmpty = true
      } else {
        this.formFormatters.teamNameIsEmpty = false
      }
      if (this.form.tg_contact === '') {
        this.formFormatters.tgContactIsEmpty = true
      } else {
        this.formFormatters.tgContactIsEmpty = false
      }
      if (this.form.amount == null || this.form.amount <= 1) {
        this.formFormatters.teamSizeIsEmpty = true
      } else {
        this.formFormatters.teamSizeIsEmpty = false
      }

      if (
        this.formFormatters.captainNameIsEmpty === false &&
        this.formFormatters.groupNameIsEmpty === false &&
        this.formFormatters.phoneIsEmpty === false &&
        this.formFormatters.teamNameIsEmpty === false &&
        this.formFormatters.teamSizeIsEmpty === false &&
        this.formFormatters.tgContactIsEmpty === false
      ) {
        this.postData('https://www.quiz-on.ru/api/register', this.form).then(
          (response) => {
            if (response.status !== 200) {
              this.headerText = 'Ой 🙈!'
              this.bodyText = 'Что-то пошло не так'
              this.showModal()
            } else {
              if (this.canRegister == 'reserve') {
                this.headerText =
                  '🤓 Поздравляем, первые задания от КвизON успешно выполнены — твоя команда зарегистрирована!'
                this.bodyText =
                  'Скоро с тобой обязательно свяжутся, а если места освободятся – сообщат и предложат место на игре в порядке очереди.'
                this.gameDate = ''
                this.seeYa = ''
              } else {
                this.headerText =
                  '☃️ Поздравляем, первые задания от\u00A0КвизON успешно выполнены — твоя команда зарегистрирована!'

                this.bodyText =
                  'Посмотрим, как ты справишься с другими вопросами на\u00A0шестой игре Бауманской лиги КвизON. Напомним, что игра пройдет:'
                this.gameDate = '⚡️21 февраля, 19:00'
                this.seeYa = 'До встречи на игре!'
              }
              this.showModal()
              this.form = {
                tg_contact: '',
                team_id: '',
                captain_name: '',
                group_name: '',
                phone: '',
                team_name: '',
                amount: null,
              }
            }
          }
        )
      } else {
        this.headerText = 'Пожалуйста... 🥲'
        this.bodyText = 'Заполните все поля формы'
        this.showModal()
      }
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
  },
}
</script>

<style scoped>
.star {
  color: #f4da6a;
}
.main {
  width: 100vw;
  max-width: 450px;
  padding-top: 2vh;
  padding-bottom: 2vh;
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

.game_num {
  padding-top: 17px;
  box-sizing: border-box;
  font-size: 21px;
  font-family: ProductSans;
  font-weight: 700;
  color: #f4da6a;
  width: fit-content;
  width: 80vw;
  max-width: 360px;
}

.block_input {
  margin-top: 11px;
  width: 80vw;
  max-width: 360px;
  height: 51px;
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

.error_output {
  margin-top: 12px;
  width: 80vw;
  max-width: 360px;
  font-family: ProductSans;
  font-weight: 400;
  overflow-wrap: break-word;
  color: #9f2128;
}

.block_text {
  font-size: 13px;
  line-height: 15px;
  font-family: ProductSans;
  font-weight: 700;
  color: #ffffff;
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

.info {
  display: flex;
  margin-top: 11px;
  width: 80vw;
  max-width: 360px;
}

.info_clock {
  max-width: 5vw;
  /* max-height: 18px; */
}

.info_loc {
  max-width: 16px;
  max-height: 21px;
}

.info_text {
  color: white;
  font-family: ProductSans;
  font-weight: 400;
  font-size: 12px;
  margin-left: 8px;
  margin-top: auto;
  margin-bottom: auto;
}

.agreement {
  margin-top: 20px;
  font-family: ProductSans;
  font-weight: 400;
  font-size: 15px;
  color: white;
}

a {
  color: #f4da6a;
  text-decoration: none;
}

.error {
  border-color: #9f2128;
}
.errorBox {
  box-shadow: 0 0 0 2px #9f2128;
}
</style>
