<template>
  <div id="app">
    <ibutton></ibutton>
    <ieditor></ieditor>
  </div>
</template>

<script>
import ibutton from './components/ibutton.vue';
import ieditor from './components/ieditor.vue';

export default {
  components: {
    ibutton, ieditor
  },
  created() {
    console.time(1);
  },
  mounted () {
    console.timeEnd(1);
  }
}
</script>

<style src="./assets/css/components.css">
</style>
