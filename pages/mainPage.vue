<template>
  <div class="main">
    <div class="frame first">
    <!-- Здесь задним фоном используются какие-то переменные картинки... -->
    <h3>ЧТО ЭТО ТАКОЕ?</h3>
    <h1>ИНТЕЛЛЕКТУАЛЬНО-РАЗВЛЕКАТЕЛЬНАЯ ИГРА</h1>
    <div class="logo-img">
      <img src="../assets/images/Logo-circle.svg" alt="">
    </div>
    <div class="play-button">
      <nuxt-link class="link" to="/RegisterPage">
      <button>ИГРАТЬ</button>
    </nuxt-link>
    </div>
    
  </div>
  <div class="frame second">
    <h3>А МОЖНО ПО ПОДРОБНЕЕ?</h3>
    <h1>КОНЕЧНО!</h1>
    <div class="text-group">
      <h2>КВИЗ<span class="hcolor">ON —</span></h2>
      <p>это интеллектуально- развлекательная командная игра и отличный вариант времяпровождения после тяжелого рабочего дня с друзьями.</p>
      <h2 class="hcolor">ЧТО НУЖНО СДЕЛАТЬ?</h2>
      <p>Вы собираете команду из 2-9 человек, регистрируете ее на сайте и становитесь участником нашей интеллектуальной схватки.</p>
      <h2 class="hcolor">КАК ЭТО ПРОИСХОДИТ?</h2>
      <p>В течение игры вам предстоит отвечать на вопросы из разных областей. Все они призваны задействовать вашу эрудицию, логику, внимательность и скорость мышления.</p>
    </div>
  </div>

  </div>
  
</template>

<script>
export default {

}
</script>

<style scoped>
.main{
  max-width: 450px;
}
.link {
  text-decoration: none;
  color: white;
}
.frame {
  margin-top: 2.5vh;
  border: 2px solid #cba362;
  background: radial-gradient(295.69% 61.62% at 21.72% 28.29%, rgba(255, 255, 255, 0) 0%, rgba(0, 0, 0, 0.04) 19.2%, rgba(15, 26, 46, 0.64) 58.33%, #0F1A2E 100%);
  border-radius: 18px;
}
.first {
  background: radial-gradient(295.69% 61.62% at 21.72% 28.29%, rgba(255, 255, 255, 0) 0%, rgba(0, 0, 0, 0.04) 19.2%, rgba(15, 26, 46, 0.64) 58.33%, #0F1A2E 100%);
} 
.second {
  background: radial-gradient(67.19% 57.35% at 78.13% 25.9%, rgba(255, 255, 255, 0) 0%, rgba(0, 0, 0, 0.04) 25.74%, rgba(15, 26, 46, 0.64) 48.58%, #0F1A2E 100%);
}

h3 {
  margin-top: 25px;
  margin-left: 25px;
  font-family: Bebas;
  font-size: 16px;
  font-weight: 700;
  line-height: 16px;
  letter-spacing: 1px;
  text-align: left;
  color: white;
}

.hcolor{
  color: #CBA262;
}

h2 {
  margin-left: 50px;
  font-family: Bebas;
  font-size: 24px;
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 2px;
  text-align: left;
  color: white;
}
h1 {
  margin-left: 25px;
  font-family: Bebas;
  font-size: 30px;
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
  border: 2px solid #CBA262;
  border-radius: 17vw;
  background-color: #030B18;
  font-family: Montserrat;
  font-size: 22px;
  font-weight: 700;
  line-height: 22px;
  letter-spacing: 0em;
  text-align: center;
  color: white;
}
.play-button{
  width: 100%;
  max-width: 450px;
  text-align: center;
}
p {
  font-family: Montserrat;
  font-size: 18px;
  font-weight: 400;
  line-height: 20px;
  letter-spacing: 0px;
  text-align: left;
  color: white;
  margin-left: 50px;
  margin-right: 30px;
  margin-top: -5px;
}

.divider {
color: white;
width: 92.5vw;
margin-left: 25px;
border: 1px solid white;
}
</style>