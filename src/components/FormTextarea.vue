<template>
  <textarea
    :v-model="name"
    :name="name"
    :id="name"
    :title="tooltip"
    :placeholder="tooltip"
    :readonly="readonly"
    spellcheck
    rows="20"
    class="form-textarea"
  />
</template>

<script>
export default {
  props: {
    name: String,
    type: String,
    tooltip: String,
    readonly: String,
  },
};
</script>

<style scoped>
.form-textarea {
  resize: none;
}
</style>
