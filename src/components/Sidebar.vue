<template>
  <div class="sidebar">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
};
</script>

<style scoped>
.sidebar {
  width: 200px;
  padding: 20px;
  border-right: 1px solid #ddd;
}
</style>
