<template>
  <div :style="styles">
    <i />
    <b />
  </div>
</template>

<script>
export default {
  name: "IconText",

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
  display: inline-flex;
  justify-content: center;
  flex-direction: column;
  position: relative;

  &::before {
    content: "";
    flex: 0 0 calc(20% - 2px);
    display: block;
    width: 54%;
    margin: 0 auto;
    border: 2px solid var(--color-text);
    border-bottom: none;
    border-radius: inherit;
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
  }

  i,
  b {
    flex: 0 0 auto;
    display: block;
  }

  i {
    height: 2px;
    background: var(--color-text);
  }

  b {
    flex: 0 0 80%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 10%;
    border: 2px solid var(--color-text);
    border-top: none;
    border-radius: inherit;
    border-top-left-radius: 0;
    border-top-right-radius: 0;

    &::before {
      content: "";
      display: block;
      width: calc(100% / 3 + 2px);
      height: 50%;
      border: solid var(--color-text);
      border-width: 0 2px;
    }
  }

  &.ui-icon_color {
    b {
      background: var(--color-bg);
    }
  }
}
</style>
