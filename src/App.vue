<template>
  <div id="app">
    <ibutton text="버튼1"></ibutton>
    <ibutton text="버튼2"></ibutton>
    <ibutton text="버튼3"></ibutton>
    <ieditor pattern="ZZZ-ZZ-ZZZZZ, ZZZZZZ-ZZZZZZZ"></ieditor>
    <ieditor pattern="AAAA-AAAA-AAAA-AAAA, AAA-AAA-AAAAA"></ieditor>
    <ipolygon></ipolygon>
    <ipolygon polygonType="diamond"></ipolygon>
    <div>
      <ipolygon style="width: 100px; height: 100px" polygonColor="blue"></ipolygon>
      <ipolygon style="width: 100px; height: 150px" polygonType="diamond" polygonColor="#ff0000"></ipolygon>
    </div>
  </div>
</template>

<script>
import ibutton from './components/ibutton.vue';
import ieditor from './components/ieditor.vue';
import ipolygon from './components/ipolygon.vue';

export default {
  components: {
    ibutton, ieditor, ipolygon
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
