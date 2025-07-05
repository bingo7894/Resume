<template>
  <button
    class="edit-toggle"
    @click="toggleEdit"
    :aria-pressed="editing.toString()"
    :title="editing ? 'Exit Edit Mode' : 'Enter Edit Mode'"
  >
    <svg
      v-if="editing"
      xmlns="http://www.w3.org/2000/svg"
      class="icon icon-editing"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
      aria-hidden="true"
    >
      <path d="M12 20h9" />
      <path d="M16.5 3.5a2.121 2.121 0 1 1 3 3L7 19l-4 1 1-4 12.5-12.5z" />
    </svg>
    <svg
      v-else
      xmlns="http://www.w3.org/2000/svg"
      class="icon icon-not-editing"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
      aria-hidden="true"
    >
      <circle cx="12" cy="12" r="10" />
      <line x1="9" y1="12" x2="15" y2="12" />
    </svg>
    <span class="label">{{ editing ? activeLabel : inactiveLabel }}</span>
  </button>
</template>

<script>
export default {
  name: "EditToggle",
  props: {
    activeLabel: {
      type: String,
      default: "Exit Edit Mode",
    },
    inactiveLabel: {
      type: String,
      default: "Enter Edit Mode",
    },
  },
  data() {
    return {
      editing: false,
    };
  },
  methods: {
    toggleEdit() {
      this.editing = !this.editing;
      this.$emit("edit-mode-toggled", this.editing);
    },
  },
};
</script>

<style scoped>
.edit-toggle {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background-color: #007bff;
  border: none;
  border-radius: 6px;
  color: white;
  padding: 8px 16px;
  font-weight: 600;
  cursor: pointer;
  user-select: none;
  transition: background-color 0.25s ease;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  margin-bottom: 20px;
}

.edit-toggle:hover {
  background-color: #0056b3;
}

.edit-toggle:focus {
  outline: 2px solid #0056b3;
  outline-offset: 2px;
}

.icon {
  width: 20px;
  height: 20px;
}

.icon-editing {
  stroke: #fff;
}

.icon-not-editing {
  stroke: #fff;
}

.label {
  font-size: 14px;
  line-height: 1;
}
</style>
