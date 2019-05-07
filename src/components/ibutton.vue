<template lang="html">
  <input v-bind:type="inputType" v-bind:class="buttonClass" v-bind:value="buttonText">
</template>

<script>
export default {
  created () {
    var $attrs = this.$attrs;
    this.buttonText = $attrs.text;
  },
  data() {
    var buttonText = '버튼';
    var inputType = 'button';
    var buttonClass = 'ibutton';
    return {
      buttonText, inputType, buttonClass
    }
  },
  methods: {
  }
}
</script>

<style lang="css" scoped>
</style>
