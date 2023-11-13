<template>
  <div>
    <div class="main">
      <mainPage />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import mainPage from './main-page.vue'

export default Vue.extend({
  components: { mainPage },
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
