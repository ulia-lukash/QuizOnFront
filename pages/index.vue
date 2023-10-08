<template>
  <div class="main">
    <main-page />
  </div>
  
</template>

<script lang="ts">
import Vue from 'vue'
import FooterVue from '~/components/FooterVue.vue'
import HeaderVue from '~/components/HeaderVue.vue'
import MainPage from './mainPage.vue'

export default Vue.extend({
  components: { FooterVue, HeaderVue, MainPage },
  name: 'IndexPage',
})
</script>

<style>

.main {
    background-color: #030B18;
}
</style>