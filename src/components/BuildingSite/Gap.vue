<template>
  <div :class="classes">
    <div class="gap__dilator dropspace" :data-index="index" />
  </div>
</template>

<script>
export default {
  name: "BuildingGap",

  props: {
    index: {
      type: Number,
      required: true
    },
    active: Boolean
  },

  computed: {
    classes() {
      return ["gap", { gap_active: this.active }];
    }
  }
};
</script>

<style lang="scss">
$block: ".gap";

#{$block} {
  flex: 0 0 calc(var(--gap) * 3);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  height: 200px;

  &::before,
  &::after {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    left: calc(50% - 2);
    pointer-events: none;
    opacity: 0;
    transition: opacity 0.1s;
    will-change: opacity;
  }

  &::before {
    width: 4px;
    border-radius: 4px;
    background: var(--color-info);
  }

  &::after {
    border-left: 4px dotted var(--color-info);
    box-shadow: 0 0 20px var(--color-info);
  }

  &_active {
    &::before {
      opacity: 0.3;
    }

    &::after {
      opacity: 1;
    }
  }

  &__dilator {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    width: 100%;
    opacity: 0;
    pointer-events: none;

    .building-site_active & {
      opacity: 1;
      pointer-events: auto;
    }
  }
}
</style>
