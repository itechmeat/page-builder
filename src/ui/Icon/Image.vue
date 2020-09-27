<template>
  <div :style="styles" />
</template>

<script>
export default {
  name: "IconImage",

  props: {
    size: {
      type: Number
    },
    radius: {
      type: Number,
      default: 8
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
  overflow: hidden;
  position: relative;
  border: 2px solid var(--color-text);

  &::before,
  &::after {
    content: "";
    position: absolute;
    border: 2px solid var(--color-text);
  }

  &::before {
    top: 20%;
    left: 20%;
    width: 22%;
    height: 22%;
    border-radius: 50%;
  }

  &::after {
    top: 60%;
    left: 20%;
    width: 100%;
    height: 100%;
    transform: rotate(45deg);
  }

  &.ui-icon_color {
    background: var(--color-info);

    &::before {
      border-color: var(--color-warning);
      background: var(--color-warning);
    }

    &::after {
      border-color: var(--color-success);
      background: var(--color-success);
    }
  }
}
</style>
