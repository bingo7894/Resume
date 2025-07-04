<template>
  <div class="color-input">
    <label :for="inputId">{{ label }}</label>
    <input
      :id="inputId"
      type="color"
      :value="defaultColor"
      @input="onColorChange"
      aria-label="Color Picker"
    />
  </div>
</template>

<script>
export default {
  name: "ColorInput",
  props: ["label", "defaultColor"],
  computed: {
    inputId() {
      return this.label.toLowerCase().replace(/\s+/g, "-") + "-color-input";
    },
  },
  methods: {
    onColorChange(e) {
      this.$emit("color-changed", e.target.value);
    },
  },
};
</script>

<style scoped>
.color-input {
  max-width: 200px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  margin-bottom: 14px;
}

.color-input label {
  display: block;
  margin-bottom: 6px;
  font-weight: 600;
  color: #444;
  user-select: none;
}

.color-input input[type="color"] {
  width: 100%;
  height: 40px;
  border: none;
  border-radius: 9999px; /* ทำให้เป็นเม็ดยา */
  cursor: pointer;
  background: transparent;
  box-shadow: 0 0 0 1.5px #ccc;
  transition: box-shadow 0.25s ease;
  padding: 0;
}

.color-input input[type="color"]:focus {
  outline: none;
  box-shadow: 0 0 0 3px #4a90e2;
}

/* webkit color swatch ปรับให้โค้งมน */
.color-input input[type="color"]::-webkit-color-swatch-wrapper {
  padding: 0;
  border-radius: 9999px;
}

.color-input input[type="color"]::-webkit-color-swatch {
  border-radius: 9999px;
}
</style>
