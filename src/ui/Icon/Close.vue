<template>
  <div :style="styles" />
</template>

<script>
export default {
  name: "IconClose",

  props: {
    size: {
      type: Number
    }
  },

  computed: {
    styles() {
      return {
        borderRadius: this.size / 8 + "px"
      };
    }
  }
};
</script>

<style lang="scss" scoped>
div {
  position: relative;
  border: 2px solid var(--color-text);

  &::before,
  &::after {
    content: "";
    position: absolute;
    top: calc(50% - 1px);
    left: 15%;
    width: 70%;
    height: 2px;
    border-radius: 2px;
    background: var(--color-text);
    transform: rotate(45deg);
  }

  &::after {
    transform: rotate(-45deg);
  }

  &.ui-icon_color {
    background: var(--color-light);
  }
}
</style>
