<template>
  <b-container>
    <b-row class="mb-5">
      <input @input="onInput">
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: 'Search',
  model: {
    event: 'teamSearch'
  },
  methods: {
    onInput(event) {
      this.$emit('teamSearch', event.target.value)
    }
  },
  props: ['value']
}
</script>

<style>
input {
  width: 80%;
  margin: 0 auto !important;
  border: 2px #374785 solid;
  border-radius: 4px;
}
</style>
