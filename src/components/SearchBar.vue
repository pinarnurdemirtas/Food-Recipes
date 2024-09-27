<template>
    <input
      type="text"
      placeholder="Yemek ara..."
      class="border p-2 rounded w-1/3"
      @input="onSearch"
    />
  </template>
  
  <script>
  export default {
    methods: {
      onSearch(event) {
        this.$emit('search', event.target.value);
      }
    }
  };
  </script>
  