<template lang="html">
  <canvas v-bind:polygonType="polygonType" v-bind:class="polygonClass" @redraw="redraw"></canvas>
</template>

<script>
export default {
  data () {
    var polygonClass = 'ipolygon';
    var POLYGON = {
      TYPE: {
        RECT: 'rect',
        ROUNTRECT: 'roundrect',
        CIRCLE: 'circle',
        DIAMOND: 'diamond'
      }
    };
    return {
      polygonClass, POLYGON
    }
  },
  created () {
    var $attrs = this.$attrs;
    this.polygonType = $attrs.polygonType || this.POLYGON.TYPE.RECT;
  },
  mounted () {
    this.redraw();
  },
  methods: {
    redraw () {
      var c = this.$el;
      var ctx = c.getContext("2d");
      // 추후 변수처리
      var left = 0;
      var top = 0;
      var width = 300;
      var height = 150;
      ctx.clearRect(left, top, width, height);

      switch(this.polygonType) {
        case 'rect':
          ctx.rect(left, top, width, height);
          break;
        case 'diamond':
          ctx.beginPath();
          ctx.moveTo(0, height / 2);
          ctx.lineTo(width / 2, 0);
          ctx.lineTo(width, height / 2);
          ctx.lineTo(width / 2, height);
          ctx.lineTo(0, height / 2);
          ctx.closePath();
          break;
      }
      ctx.stroke();
    }
  }
}
</script>

<style lang="css" scoped>
</style>
