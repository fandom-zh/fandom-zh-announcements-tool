<template>
  <section :id="name">
    <h2 class="form-title">{{ title }}</h2>
    <div class="form">
      <slot></slot>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    name: String,
    title: String,
  },
};
</script>

<style scoped>
.form-title {
  margin-left: 15px;
  display: inline-block;
  background-image: linear-gradient(
    to top,
    rgba(0, 155, 190, 0.15) 54%,
    transparent 54%,
    transparent 100%
  );
}
</style>
