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
})
</script>

<style>
.main {
  width: 100vw;
  max-width: 450px;
  background-color: #182a3e;
}
</style>
