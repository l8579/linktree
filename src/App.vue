<template>
  <div>
    <LinkTreeApp />
    <div class="WHS"></div>
  </div>
</template>

<script>
import LinkTreeApp from './views/LinkTreeApp.vue';

export default {
  name: 'App',
  components: {
    LinkTreeApp
  }
}
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  font-family: 'Kanit', sans-serif;
}

.WHS {
  height: 50px;
  width: 100%;
  margin-top: 120px;
}
</style>
