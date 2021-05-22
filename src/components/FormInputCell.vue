<template>
  <div class="input-cell">
    <label class="input-label" :for="name">{{ label }}</label>

    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    name: String,
  },
};
</script>

<style scoped>
.input-cell {
  display: inline-block;
  margin: 5px;
}
.input-label {
  display: block;
}
</style>
