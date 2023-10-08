<template>
  <div class="main">
    <h2> {{ alertHeader }}</h2>
    <div class="inner-rect">
        <p>{{ alertText }}</p>
        <div v-on:click="dismissAlert" class = "button">OK</div>
    </div>
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
    width: 85vw;
    height: 50vw;
    max-width: 85vw;
    max-height: 50vw;
    margin: 0 auto;
    background-color: #CBA262;
    border-radius: 30px;
    border: 2px solid #CBA262;

    margin: auto;
    display: block;
    position: relative;

}
.inner-rect {
    background-color: #0F1A2E;
    border-radius: 30px;
    width: 98%;
    height: 75%;
    position: absolute;
    margin-left: 1%;
    top: 12vw;
}
h2 {
    height: 10vw;
    width: 80vw;
    color: white;
    font-family: "Bebas Neue";
    font-weight: 700;
    font-size: 30px;
    line-height: 20px;
    letter-spacing: 0em;
    text-align: center;
    color: black;
    text-align: center;
}

p {
    width: 80vw;
    padding-top: 5vw;
    color: white;
    font-family: "Montserrat";
    font-weight: 700;
    font-size: 15px;
    line-height: 18px;
    letter-spacing: 0em;
    text-align: center;

}

.button {
    background-color: rgb(10, 18, 33);
    border: 2px solid #CBA262;
    border-radius: 17.3457px;
    border-color: #CBA262;
    width: 66%;
    height: 35px;

    font-family: Bebas;
    font-weight: 700;
    text-align: center;
    color: #FFFFFF;
    font-size: 22px;
    line-height: 35px;
    letter-spacing: 0em;
    margin: auto;

    position: absolute;
    margin-left: 17%;
    top: 23vw;
}
</style>