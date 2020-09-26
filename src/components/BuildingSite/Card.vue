<template>
  <div :class="classes">
    <div class="card__card" draggable="true" :data-card="index">
      {{ index }}: type={{ value.type }}
    </div>
  </div>
</template>

<script>
export default {
  name: "BuildingCard",

  props: {
    index: {
      type: Number,
      required: true
    },
    value: {
      type: Object,
      required: true
    },
    active: Boolean
  },

  computed: {
    classes() {
      return [
        "card",
        "card_" + this.value.type,
        { card_first: this.index === 0 },
        { card_active: this.active }
      ];
    }
  }
};
</script>

<style lang="scss">
$block: ".card";

#{$block} {
  position: relative;
  flex: 0 0 calc(100% / 3 - var(--gap) * 4);
  height: 200px;
  margin-top: calc(var(--gap) * 3);

  &_first {
    flex: 0 0 calc(100% - var(--gap) * 6);
    margin-top: 0;
  }

  &__card {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    z-index: 10;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 1px dashed var(--color-border);
    background: #fff;

    #{$block}_active & {
      opacity: 0.3;
    }
  }
}
</style>
