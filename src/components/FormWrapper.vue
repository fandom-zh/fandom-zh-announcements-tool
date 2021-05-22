<template>
  <fieldset :id="formId">
    <legend>{{ title }}</legend>

    <slot></slot>
  </fieldset>
</template>

<script setup>
import { defineProps } from "vue";

defineProps({
  title: String,
  formId: String,
});
</script>

<style scoped>
fieldset {
  margin: 10px;
  display: inline-block;
}
</style>
