<template>
  <div class="main">
    <div class="frame first">
    <h3>ЧТО ЭТО ТАКОЕ?</h3>
    <h1>ИНТЕЛЛЕКТУАЛЬНО-РАЗВЛЕКАТЕЛЬНАЯ ИГРА</h1>
    <div class="logo-img">
      <img src="../assets/images/new-logo.png" alt="" style="width: 270px">
    </div>
    <div class="play-button">
      <nuxt-link class="link" to="/RegisterPage">
      <button  >ИГРАТЬ</button>
    </nuxt-link>
    </div>
    
    </div>
    <div class="frame second">
      <h3>А МОЖНО ПОДРОБНЕЕ?</h3>
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
    <div class="frame third">
      <h3>А МОЖНО ПОДРОБНЕЕ?</h3>
      <h1>В ИГРЕ ВАС ЖДЕТ</h1>
      <h1 class="hcolor">7 РАУНДОВ:</h1>
      <div class="divider"></div>
      <p style="font-weight: 700; margin-top: 2vh; font-size: 20px;">Вопросы на различные темы:</p>
      <p>от классической музыки до современных сериалов и кино, от науки до бытовой культуры</p>
      <p style="margin-top: 2vh;"><span style="font-weight: 700; font-size: 20px;">2 часа</span> интеллектуального сражения за звание самых умных игроков вечера и целого сезона</p>
    </div>
  </div>
</template>

<script>

export default {


}
</script>

<style scoped>
.main{
  width: 100vw;
  max-width: 450px;
}
.link {
  text-decoration: none;
  color: white;
}
.frame {
  /* width: 90vw;
  max-width: 405px; */
  margin-top: 2.5vh;
  margin-left: 5vw;
  border: 1px solid #F4DA6A;
  border-radius: 21px;
  box-shadow: 0px 0px 10px 5px rgba(0, 0, 0, 0.383);
}
.first {
   background-image: radial-gradient(150% 60% at 30.72% 40.29%, rgba(0, 0, 0, 0.274) 0%, rgba(0, 0, 0, 0.281) 15%, #182a3ebe 30.33%, #182A3E 100%), url("../assets/images/background-first.jpg");
   height: 100%;
   width: 90%;
   background-position: center center;
   background-size: cover;
}
.second {
  background-image: radial-gradient(100.19% 40.35% at 78.13% 40.9%, rgba(0, 0, 0, 0.514) 0%,  rgba(15, 26, 46, 0.64) 48.58%, #182A3E 100%), url("../assets/images/background-second.jpg");
  height: 100%;
   width: 90%;
   background-position: center center;
   background-size: cover;
}
.third {
  background-image: radial-gradient(60% 90% at 40.78% 65.16%, rgba(0, 0, 0, 0.342) 0%, rgba(0, 0, 0, 0.452) 25.74%, rgba(15, 26, 46, 0.64) 53.56%, #182A3E 100%), url("../assets/images/background-third.jpg");

  height: 100%;
   width: 90%;
   background-position: center center;
   background-size: cover;
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

.hcolor{
  color: #F4DA6A;
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
  border: 2px solid #F4DA6A;
  border-radius: 17vw;
  background-color: #F4DA6A;
  font-family: ProductSans;
  font-size: 22px;
  font-weight: 700;
  line-height: 22px;
  letter-spacing: 0em;
  text-align: center;
  color: black;
}
.play-button{
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
margin-left: 25px;
border: 1px solid white;
}

.disabled{
  pointer-events: none
}
</style>