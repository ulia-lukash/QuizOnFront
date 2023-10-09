<template>
  <div class="main">
    <main-page />
  </div>
  
</template>

<script lang="ts">
import Vue from 'vue'
import MainPage from './mainPage.vue'

export default Vue.extend({
  components: { MainPage },
  name: 'IndexPage',
  data() {
    return {
      
    }
  }
})
</script>

<style>

.main {
  max-width: 450px;
  background-color: #030B18;
  margin: 0 auto;
}
</style>