<template>
  <div class="main">
    <div class="logo-image">
      <nuxt-link to="/mainPage">
        <img src="../assets/images/new-logo.png" alt="" style="height: 40px;">
      </nuxt-link>
        
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
.logo-image {
    display: inline-block;
    width: 19vw;
    margin-top: 5%;
    margin-left: 5%;
}
/* .menu-icon {
  display: inline-block;
  margin-left: 62vw;
} */
</style>