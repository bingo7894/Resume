<template>
  <h4 class="section-headline" contenteditable="true" @input="notifyParent">
    {{ headline }}
  </h4>
</template>

<script>
export default {
  props: ["headline"],
  methods: {
    notifyParent(event) {
      this.$emit("headlineEdited", event.target.innerText);
    },
  },
};
</script>

<style scoped>
.section-headline {
  font-size: 20px;
  font-weight: var(--headline-weight);
  margin-bottom: 15px;
  margin-top: 0;
}
.right-col .section-headline {
  color: var(--highlight-color-right);
}
.left-col .section-headline {
  border-bottom: 1px solid var(--highlight-color-left);
  padding-bottom: 5px;
  margin-right: -30px;
  padding-right: 10px;
  color: var(--highlight-color-left);
}
</style>
