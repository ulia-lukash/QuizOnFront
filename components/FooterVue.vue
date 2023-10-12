<template>
  <main class="main">
    <div class="logo-pic">
      <img src="../assets/images/new-logo.png" alt="" style="width: 90px">
    </div>
    <div class="sm-logos" style="margin: 0 auto">
      <div>
        <a href="https://vk.com/quizonmsk"  class="logo">
        <img src="../assets/images/vk-logo.svg" alt="" style="height: 20px; padding-bottom: 5px">
      </a>
      <div style="width: 30px; display: inline-block"></div>
      <a href="https://t.me/quizonmsk"  class="logo">
        <img src="../assets/images/tg-logo.svg" alt="" style="width: 31px;">
      </a>
      </div>
      
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

.logo{
  display: inline-block;
  width: 31px;
}
.main {
  max-width: 450px;
}
.logo-pic {
  text-align: center;
  padding-top: 3vh;
}
.navigation{
  font-family: ProductSans;
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
  text-align: center;
  font-family: ProductSans;
  font-size: 10px;
  font-weight: 700;
  line-height: 12px;
  letter-spacing: 0em;
  text-align: center;
  color: #C8C6B2;
  width: 166px;
}
.sm-logos {
  width: 100%;
  text-align: center;
  padding-top: 3vh;
}

.divider {
  width: 84%;
  border-top: 2px solid #ffffff50;
}

.copyright {
  padding-top: 13px;
  width: 100%;
  font-family: ProductSans;
  font-size: 12px;
  font-weight: 700;
  line-height: 15px;
  letter-spacing: 0px;
  text-align: center;
  color:#ffffff50;
}
.user-agreement {
  padding-top: 15px;
  padding-bottom: 13px;
  width: 100%;
  text-align: center;
}
</style>