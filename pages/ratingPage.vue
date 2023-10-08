<template>
  <div class="main">
    <div class="header">рейтинг команд</div>
    <div class="buttons">
      <button type="button" v-on:click="generalRankWasClicked" class = "btn" :class = "{ active: buttonFormatters.generalRankIsActive }">ОБЩИЙ РЕЙТИНГ</button>
      <button type="button" v-on:click="lastGamesWasClicked" class = "btn right" :class = "{ active: buttonFormatters.lastGamesRankIsActive }">ПОСЛЕДНИЕ ИГРЫ</button>

    </div>
  </div>
</template>

<script>
export default {
  name: 'RankingPage',
    data() {
      return {
        buttonFormatters: {
          generalRankIsActive: true,
          lastGamesRankIsActive: false
        },
      };
    },
    methods: {
      generalRankWasClicked() {
        this.buttonFormatters.generalRankIsActive = true;
        this.buttonFormatters.lastGamesRankIsActive = false;
      },
      lastGamesWasClicked() {
        this.buttonFormatters.generalRankIsActive = false;
        this.buttonFormatters.lastGamesRankIsActive = true;
      }
    }
}
</script>

<style scoped>

.header {
  padding-top: 5vh;
  padding-bottom: 3vh;
  font-family: Bebas;
  font-size: 36px;
  font-weight: 700;
  line-height: 36px;
  letter-spacing: 2px;
  text-align: center;
  color: white;
}
.btn {
  display: inline-block;
  width: 45vw;
  height: 36px;
  border: 2px solid #CBA262;
  border-radius: 18px;
  background-color: #030B18;
  font-family: Montserrat;
  font-size: 12px;
  font-weight: 700;
  line-height: 12px;
  letter-spacing: 0em;
  text-align: center;
  color: white;
}

.active {
  background-color: #CBA262;
  color: #030B18
}
.buttons {
  width: 96vw;
  margin: 0 auto;
}
.right {
  margin-left: 5vw;
}
</style>