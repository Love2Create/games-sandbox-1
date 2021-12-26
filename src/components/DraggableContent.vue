<template>
  <div
    class="draggable"
    @mousedown="mouseDown"
    @mouseup="mouseUp"
    @mousemove="mouseMove"
    :style="{ left: `${mousePosition.x}px`, top: `${mousePosition.y}px` }"
  >
    <div class="dragContent"><slot></slot></div>
    <div class="dragger"></div>
    <div v-if="isDragging" class="overlay"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDragging: false,
      mousePosition: {
        x: "",
        y: "",
        rectX: "",
        rectY: "",
        offsetX: "",
        offsetY: "",
      },
    };
  },
  methods: {
    mouseDown(e) {
      this.isDragging = true;
      this.mousePosition.rectX = e.currentTarget.getBoundingClientRect().left;
      this.mousePosition.rectY = e.currentTarget.getBoundingClientRect().top;
      this.mousePosition.offsetX = this.mousePosition.rectX - e.clientX;
      this.mousePosition.offsetY = this.mousePosition.rectY - e.clientY;

      //   console.log(this.mousePosition.rectX, this.mousePosition.rectY, this.mousePosition.offsetX, this.mousePosition.offsetY)
    },
    mouseUp() {
      this.isDragging = false;
      console.log("mouse is up");
    },
    mouseMove(e) {
      if (this.isDragging) {
        this.mousePosition.x = e.clientX + this.mousePosition.offsetX;
        this.mousePosition.y = e.clientY + this.mousePosition.offsetY;
      }
    },
  },
};
</script>

<style scoped>
.draggable {
  position: absolute;
}
.dragger {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 10;
}
</style>