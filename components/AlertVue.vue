<template>
  <div class="main">
    <img src="../assets/images/alert-back.svg" alt="">
        <h2> {{ alertHeader }}</h2>
        <p>{{ alertText }}</p>
        <div v-on:click="dismissAlert" class = "button">OK</div>
  </div>
</template>

<script>
export default {
    props: [
        'alertText', 'alertHeader'
    ],
    methods: {
        dismissAlert() {
            this.$emit('dismissAlert')
        }
    }
}
</script>

<style scoped>

.main {
    position: fixed;
    top: 20vh;
    left: 10vw;
}
img{
    width: 80vw;
    height: 25vh;
}
h2 {
    position: fixed;
    top: 23vh;
    left: 10vw;
    width: 80vw;
    height: 6.25vh;
    color: white;
    font-family: ProductSans;
    font-weight: 700;
    font-size: 4vh;
    line-height: 4vh;
    letter-spacing: 0em;
    text-align: center;
    color: black;
}

p {
    width: 80vw;
    color: white;
    font-family: ProductSans;
    font-weight: 700;
    font-size: 2.5vh;
    letter-spacing: 0em;
    text-align: center;
    position: fixed;
    top: 31vh;
    left: 10vw;
}

.button {
    background-color: #182A3E;
    border: 2px solid #E0AC59;
    border-radius: 17.3457px;
    border-color: #E0AC59;
    width: 50vw;
    max-width: 180px;
    height: 35px;
    font-family: ProductSans;
    font-weight: 700;
    text-align: center;
    color: #FFFFFF;
    font-size: 22px;
    line-height: 35px;
    letter-spacing: 0em;
    position: fixed;
    top: 40vh;
    left: 25vw;

}
</style>