<template>
  <div :style="styles">
    <b />
  </div>
</template>

<script>
export default {
  name: "IconClose",

  props: {
    size: {
      type: Number
    },
    radius: {
      type: Number,
      default: 6
    }
  },

  computed: {
    styles() {
      return {
        borderRadius: this.size / this.radius + "px"
      };
    }
  }
};
</script>

<style lang="scss" scoped>
div {
  position: relative;

  b {
    position: absolute;
    top: 0;
    left: calc(50% - 1px);
    width: 2px;
    height: 70%;
    border-radius: 2px;
    background: var(--color-text);

    &::before,
    &::after {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: inherit;
      height: 50%;
      border-radius: inherit;
      background: inherit;
      transform: rotate(45deg);
      transform-origin: 0 2%;
    }

    &::after {
      transform: rotate(-45deg);
      transform-origin: 100% 2%;
    }
  }

  &::after {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 45%;
    border: 2px solid var(--color-text);
    border-top: none;
    border-radius: inherit;
    border-top-left-radius: 0;
    border-top-right-radius: 0;
  }
}
</style>
