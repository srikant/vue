<template>
  <div
    class="box"
    :class="{ fadeOut: isFadingOut }"
    :style="{ backgroundColor: isActive ? 'green' : 'white' }"
    @click="handleClick"
  >
    <span>{{ id }}</span>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    isActive: Boolean,
    isFadingOut: Boolean,
  },
  emits: ["box-clicked"],
  methods: {
    handleClick() {
      this.$emit("box-clicked", this.id);
    },
  },
};
</script>

<style scoped>
.box {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 18px;
  font-weight: bold;
  margin: 5px;
  cursor: pointer;
  user-select: none;
  transition: opacity 0.5s ease-in-out, background-color 0.5s ease-in-out;
}

.fadeOut {
  opacity: 0;
}
</style>
