<template>
  <div>
    <div class="main">
    <main-page />
  </div>
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
      width: 0
    }
  },
  beforeMount() {
    this.width = window.innerWidth
  }
})
</script>

<style>

.main {
  max-width: 450px;
  background-color: #182A3E;
  margin: 0 auto;
}
</style>