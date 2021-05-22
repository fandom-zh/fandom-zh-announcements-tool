<template>
  <select :v-model="name" :name="name" :id="name" :title="tooltip">
    <slot></slot>
  </select>
</template>

<script>
export default {
  props: {
    name: String,
    tooltip: String,
  },
};
</script>
