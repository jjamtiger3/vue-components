
<template lang="html">
  <input v-bind:type="editorType" v-bind:class="editorClass" v-bind:value="editorValue">
</template>

<script>
export default {
  data() {
    var editorValue = '';
    var editorType = 'text';
    var editorClass = 'ieditor';
    return {
      editorValue, editorType, editorClass
    }
  },
  methods: {
  }
}
</script>

<style lang="css" scoped>
</style>
