<template>
  <b-row class="mb-3">
      <b-col cols="6" class="ml-auto mr-auto">
        <b-form-input ref="searchInput" :value="value.input" @input="search()" placeholder="Search for team..."></b-form-input>
      </b-col>
    </b-row>
</template>

<script>
export default {
  name: 'Search',
  props: ['value'],
  methods: {
    search(event) {
      this.$emit('input', {
        input: +this.$refs.searchInput.value
      })
    }
  }
}
</script>

<style>

</style>
