<template>
  <div>
<div class="b-popup">
    <div class="b-popup-content">
        <p style="font-weight: 700">{{alertHeader}}</p>
        <p>{{alertText}}</p>
        
    </div>
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


.b-popup{
    width:100%;
    min-height:100%;
    background-color: rgba(0, 0, 0, 0.092);
    overflow:hidden;
    position:fixed;
    top:0px;
    left: 0px;
    font-family: ProductSans;
}
.b-popup .b-popup-content{
    margin: 25vh auto 0px auto;
    width:250px;
    height: 130px;
    padding:10px;
    background-color: #F4DA6A;
    border-radius: 21px;
    box-shadow: 0px 0px 10px #000;
    text-align: center;
}
</style>