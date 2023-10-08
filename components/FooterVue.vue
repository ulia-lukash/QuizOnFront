<template>
  <main class="main">
    <div class="logo-pic">
      <img src="../assets/images/logo.svg" alt="">
    </div>
    <div class="navigation">
      <nuxt-link class="link" to="/mainPage">ГЛАВНАЯ</nuxt-link>
      <br>
      <nuxt-link class="link" to="/scheduleVue">КАЛЕНДАРЬ ИГР</nuxt-link>
      <br>
      <nuxt-link class="link" to="/ratingPage">РЕЙТИНГ</nuxt-link>
      <br>
      <nuxt-link class="link" to="/contactsPage">КОНТАКТЫ</nuxt-link>
    </div>
    <div class="sm-logos">
      <a href="https://vk.com/quizonmsk">
        <img src="../assets/images/vk-logo.svg" alt="">
      </a>
      
    </div>
    <hr class="divider">
    <div class="copyright">© 2023 КвизON</div>
    <div class="user-agreement">
      <nuxt-link class="link" to="/userAgreement">СОГЛАШЕНИЕ ОБ ОБРАБОТКЕ ПЕРСОНАЛЬНЫХ ДАННЫХ</nuxt-link>
      </div>
  </main>
</template>

<script>
export default {
  data() {
      return {
      }
    }
}
</script>

<style scoped>
.main {
  margin-top: 25px;
}
.logo-pic {
  text-align: center;
}
.navigation{
  font-family: "Montserrat";
  font-size: 12px;
  font-weight: 700;
  line-height: 15px;
  letter-spacing: 0em;
  text-align: left;
  padding: 30px;
}

.link {
  display: inline-block;
  text-decoration: none; 
  color: #CAC8B4;
}
.sm-logos {
  width: 9.5vw;
  margin: 0 auto;
}

.divider {
  width: 84vw;
  border-top: 2px solid #ffffff50;
}

.copyright {
  padding-top: 13px;
  width: 102px;
  font-family: "Montserrat";
  font-size: 12px;
  font-weight: 700;
  line-height: 15px;
  letter-spacing: 0px;
  text-align: left;
  color:#ffffff50;
  margin: auto;
}
.user-agreement {
  padding-top: 13px;
  padding-bottom: 13px;
  font-family: "Montserrat";
  font-size: 10px;
  font-weight: 700;
  line-height: 12px;
  letter-spacing: 0em;
  text-align: center;
  color: #C7C6B2;
  width: 166px;
  margin: auto;
}
</style>