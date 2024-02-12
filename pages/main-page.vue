<template>
  <div>
    <div class="main">
      <ModalVue v-show="isModalVisible" v-on:close="closeModal">
        <template v-slot:header>
          {{ headerText }}
        </template>

        <template v-slot:body>
          <span style="color: black">{{ bodyText }}</span>
          <br />
          <br />
          <span style="color: black">{{ bodyTextTwo }}</span>
        </template>

        <template v-slot:footer> </template>
      </ModalVue>
      <div class="frame first">
        <h3>ЧТО ЭТО ТАКОЕ?</h3>
        <h1>ИНТЕЛЛЕКТУАЛЬНО-РАЗВЛЕКАТЕЛЬНАЯ ИГРА</h1>
        <div class="logo-img">
          <img
            src="../assets/images/new-logo.png"
            alt=""
            style="width: 270px"
          />
        </div>
        <div v-on:click="buttonClicked" class="play-button">
          <!-- <nuxt-link
          :event="disabled ? '' : 'click'"
          class="link"
          to="/registration"
        > -->
          <button>ИГРАТЬ</button>
          <!-- </nuxt-link> -->
        </div>
      </div>
      <div class="frame second">
        <h3>А МОЖНО ПОДРОБНЕЕ?</h3>
        <h1>КОНЕЧНО!</h1>
        <div class="text-group">
          <h2>КВИЗ<span class="hcolor">ON —</span></h2>
          <p>
            это интеллектуально-развлекательная игра в формате викторины,
            которая станет отличным вариантом для отдыха в хорошей компании
          </p>
          <h2 class="hcolor">ЧТО НУЖНО СДЕЛАТЬ?</h2>
          <p>
            Собрать команду от 4 до 8 человек, зарегистрировать ее на сайте и
            прийти в указанные время и место на игру
          </p>
          <h2 class="hcolor">КАК ЭТО ПРОИСХОДИТ?</h2>
          <p>
            Игра включает в себя несколько раундов и самые разные форматы
            вопросов. Вместе с командой вам предстоит побороться в этой битве
            логики, эрудиции и скорости мышления!
          </p>
        </div>
      </div>
      <div class="frame third">
        <h3>А МОЖНО ПОДРОБНЕЕ?</h3>
        <h1>В ИГРЕ ВАС ЖДЕТ</h1>
        <h1 class="hcolor">7 РАУНДОВ:</h1>
        <div class="divider"></div>
        <p style="margin-top: 2vh">
          <span style="font-weight: 700; font-size: 20px"
            >Вопросы на различные темы:</span
          >
          от классической музыки до современных сериалов и кино, от науки до
          бытовой культуры
        </p>
        <p style="margin-top: 2vh">
          <span style="font-weight: 700; font-size: 20px">2 часа</span>
          интеллектуального сражения за звание самых умных игроков вечера и
          целого сезона
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import ModalVue from '../components/ModalVue.vue'

export default {
  components: { ModalVue },
  data() {
    return {
      isModalVisible: false,
      canRegister: '',
      headerText: '',
      bodyText: '',
      bodyTextTwo: '',
      disabled: false,
    }
  },

  methods: {
    showModal() {
      this.isModalVisible = true
    },
    closeModal() {
      this.isModalVisible = false
    },
    buttonClicked() {
      this.checkIfCanRegister()
      this.checkAvailability()
    },
    async checkIfCanRegister() {
      try {
        const response = await fetch(
          'https://www.quiz-on.ru/api/register-available'
        ).then((respone) => {
          return respone.json()
        })
        const available = response.available
        this.canRegister = response.available
        if (available === 'closed') {
          this.headerText = '😪 КвизOFF...'
          this.bodyText =
            'К сожалению, больше нет мест на\u00A0предстоящую игру. Следите за\u00A0новостями в\u00A0наших социальных сетях, чтобы точно успеть зарегистрироваться в\u00A0следующий раз'
          this.showModal()
        } else if (available === 'not_opened_yet') {
          this.headerText = 'Ой 🤭'
          this.bodyText =
            'Очень рады, что ты хочешь попасть на\u00A0игру! Но, к\u00A0сожалению, регистрация еще закрыта.'
          this.bodyTextTwo =
            'Чтобы не\u00A0пропустить регистрацию на\u00A0следующую игру, следи за\u00A0анонсами в\u00A0социальных сетях – там будет вся актуальная информация.'
          this.showModal()
          // this.disabled = true
        } else if (available === 'available' || available === 'reserve') {
          this.$router.push('/registration')
          this.$router.go('1')
          // this.disabled = false
        }
        return available
      } catch (error) {
        this.headerText = 'Ошибка!'
        this.bodyText = 'Что-то пошло не так'
        this.showModal()
      }
    },
    checkAvailability() {
      console.log(this.canRegister)
      if (this.canRegister === 'closed') {
        this.headerText = '😪 КвизOFF...'
        this.bodyText =
          'К сожалению, больше нет мест на\u00A0предстоящую игру. Следите за\u00A0новостями в\u00A0наших социальных сетях, чтобы точно успеть зарегистрироваться в\u00A0следующий раз'
        this.showModal()
      } else if (this.canRegister === 'not_opened_yet') {
        this.headerText = 'Ой 🤭'
        this.bodyText =
          'Очень рады, что ты хочешь попасть на\u00A0игру! Но, к\u00A0сожалению, регистрация еще закрыта.'
        this.bodyTextTwo =
          'Чтобы не\u00A0пропустить регистрацию на\u00A0следующую игру, следи за\u00A0анонсами в\u00A0социальных сетях – там будет вся актуальная информация.'
        this.showModal()
      }
    },
  },
}
</script>

<style scoped>
.main {
  width: 100vw;
  max-width: 450px;
}
.link {
  text-decoration: none;
  color: white;
}
.frame {
  margin-top: 2.5vh;
  border: 1px solid #f4da6a;
  border-radius: 21px;
  box-shadow: 0px 0px 10px 5px rgba(0, 0, 0, 0.383);
}
.first {
  background-image: radial-gradient(
      150% 60% at 30.72% 40.29%,
      rgba(0, 0, 0, 0.274) 0%,
      rgba(0, 0, 0, 0.281) 15%,
      #182a3ebe 30.33%,
      #182a3e 100%
    ),
    url('../assets/images/background-first.jpg');
  height: 100%;
  width: 90%;
  background-position: center center;
  background-size: cover;
  margin: 2.5vh auto;
}
.second {
  background-image: radial-gradient(
      100.19% 40.35% at 78.13% 40.9%,
      rgba(0, 0, 0, 0.514) 0%,
      rgba(15, 26, 46, 0.64) 48.58%,
      #182a3e 100%
    ),
    url('../assets/images/background-second.jpg');
  height: 100%;
  width: 90%;
  background-position: center center;
  background-size: cover;
  margin: 2.5vh auto;
}
.third {
  background-image: radial-gradient(
      60% 90% at 40.78% 65.16%,
      rgba(0, 0, 0, 0.529) 0%,
      rgba(0, 0, 0, 0.648) 25.74%,
      rgba(15, 26, 46, 0.64) 53.56%,
      #182a3e 100%
    ),
    url('../assets/images/background-third.jpg');

  height: 100%;
  width: 90%;
  background-position: center center;
  background-size: cover;
  margin: 2.5vh auto;
}

h3 {
  margin-top: 25px;
  margin-left: 25px;
  font-family: ProductSans;
  font-size: 16px;
  font-weight: 700;
  line-height: 16px;
  letter-spacing: 1px;
  text-align: left;
  color: white;
}

.hcolor {
  color: #f4da6a;
}

h2 {
  margin-left: 25px;
  font-family: ProductSans;
  font-size: 24px;
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 2px;
  text-align: left;
  color: white;
}
h1 {
  margin-left: 25px;
  font-family: ProductSans;
  font-size: 27px;
  font-weight: 700;
  line-height: 30px;
  letter-spacing: 1px;
  text-align: left;
  color: white;
}
.logo-img {
  margin-top: 9vh;
  text-align: center;
}
button {
  margin-top: 9vh;
  margin-bottom: 5vh;
  width: 52vw;
  max-width: 234px;
  height: 17vw;
  max-height: 76.5px;
  border: 2px solid #f4da6a;
  border-radius: 17vw;
  background-color: #f4da6a;
  font-family: ProductSans;
  font-size: 22px;
  font-weight: 700;
  line-height: 22px;
  letter-spacing: 0em;
  text-align: center;
  color: black;
}
.play-button {
  width: 100%;
  max-width: 450px;
  text-align: center;
}
p {
  font-family: ProductSans;
  font-size: 18px;
  font-weight: 400;
  line-height: 20px;
  letter-spacing: 0px;
  text-align: left;
  color: white;
  margin-left: 25px;
  margin-right: 30px;
  margin-top: -5px;
}

.divider {
  color: white;
  width: 90%;
  /* margin-left: 25px; */
  border: 1px solid white;
}

.disabled {
  pointer-events: none;
}
</style>
