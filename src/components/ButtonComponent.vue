<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "ButtonComponent",
  props: {
    text: {
      type: String,
      default: "Button Component",
    },
    color: String,
  },
  emits: ["button-click"],
  methods: {
    onClick() {
      this.$emit("button-click");
    },
  },
};
</script>

<style scoped></style>
