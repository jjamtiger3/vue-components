<template lang="html">
  <canvas v-bind:polygonType="polygonType"></canvas>
</template>

<script>
export default {
  data () {
    return {
      POLYGON: {
        TYPE: {
          RECT: 'rect',
          ROUNTRECT: 'roundrect',
          CIRCLE: 'circle',
          DIAMOND: 'diamond'
        }
      }
    }
  },
  created () {
    var $attrs = this.$attrs;
    this.polygonType = $attrs.polygonType || this.POLYGON.TYPE.RECT;
  },
  methods: {
    redraw () {

    }
  }
}
</script>

<style lang="css" scoped>
</style>
