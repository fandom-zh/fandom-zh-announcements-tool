<template>
  <fieldset class="form-wrapper">
    <legend class="form-legend">{{ title }}</legend>

    <slot></slot>
  </fieldset>
</template>

<script setup>
import { defineProps } from "vue";

defineProps({
  title: String,
});
</script>

<style scoped>
.form-wrapper {
  margin: 10px;
  display: inline-block;
}
.form-legend {
  padding-left: 5px;
  padding-right: 5px;
}
</style>
