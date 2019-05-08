<template lang="html">
  <canvas v-bind:polygonType="polygonType" v-bind:class="polygonClass" v-bind:polygonColor="polygonColor" @redraw="redraw"></canvas>
</template>

<script>
export default {
  data () {
    var polygonClass = 'ipolygon';
    var polygonColor = this.polygonColor;
    var POLYGON = {
      TYPE: {
        RECT: 'rect',
        ROUNTRECT: 'roundrect',
        CIRCLE: 'circle',
        DIAMOND: 'diamond'
      }
    };
    return {
      polygonClass, polygonColor, POLYGON
    }
  },
  created () {
    var $attrs = this.$attrs;
    this.polygonType = $attrs.polygonType || this.POLYGON.TYPE.RECT;
    this.polygonColor = $attrs.polygonColor;
  },
  mounted () {
    var canvas = this.$el;
    var width = parseInt(canvas.style.width);
    var height = parseInt(canvas.style.height);
    width = isNaN(width) ? 300 : width;
    height = isNaN(height) ? 150 : height;
    this.$el.width = width;
    this.$el.height = height;
    this.redraw();
  },
  methods: {
    redraw () {
      var canvas = this.$el;
      var ctx = canvas.getContext("2d");
      // 추후 변수처리
      var left = 0;
      var top = 0;
      var width = parseInt(canvas.style.width);
      var height = parseInt(canvas.style.height);
      width = isNaN(width) ? 300 : width;
      height = isNaN(height) ? 150 : height;

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
      if(this.polygonColor) {
        ctx.fillStyle = this.polygonColor;
        ctx.fill();
      }
    }
  }
}
</script>

<style lang="css" scoped>
</style>
