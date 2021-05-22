<template>
  <input
    :v-model="name"
    :name="name"
    :id="name"
    :title="tooltip"
  />
</template>

<script>
export default {
  props: {
    name: String,
    tooltip: String,
  },
};
</script>
