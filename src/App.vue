<template>
  <div>
    <div class="row">
      <BoxComponent
        v-for="id in [1, 2, 3]"
        :key="id"
        :id="id"
        :isActive="activeBoxes.includes(id)"
        :isFadingOut="fadingBoxes.includes(id)"
        @box-clicked="onBoxClick"
      />
    </div>
    <div class="row">
      <BoxComponent
        v-for="id in [4, 5]"
        :key="id"
        :id="id"
        :isActive="activeBoxes.includes(id)"
        :isFadingOut="fadingBoxes.includes(id)"
        @box-clicked="onBoxClick"
      />
    </div>
    <div class="row">
      <BoxComponent
        v-for="id in [6, 7, 8]"
        :key="id"
        :id="id"
        :isActive="activeBoxes.includes(id)"
        :isFadingOut="fadingBoxes.includes(id)"
        @box-clicked="onBoxClick"
      />
    </div>
  </div>
</template>

<script>
import BoxComponent from "./components/BoxComponent.vue";

export default {
  components: {
    BoxComponent,
  },
  data() {
    return {
      activeBoxes: [],
      fadingBoxes: [],
    };
  },
  methods: {
    onBoxClick(id) {
      if (id === 8) {
        this.triggerFadeOut();
      } else {
        this.toggleBox(id);
      }
    },
    toggleBox(id) {
      if (!this.activeBoxes.includes(id)) {
        this.activeBoxes.push(id);
      }
    },
    async triggerFadeOut() {
      while (this.activeBoxes.length) {
        const lastBox = this.activeBoxes.pop();
        this.fadingBoxes.push(lastBox);

        await new Promise((resolve) => setTimeout(resolve, 500));

        this.fadingBoxes = this.fadingBoxes.filter(
          (boxId) => boxId !== lastBox
        );
      }
    },
  },
};
</script>

<style scoped>
.row {
  display: flex;
  justify-content: center;
  margin: 10px 0;
}
</style>
