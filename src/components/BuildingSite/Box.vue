<template>
  <div :class="classes">{{ index }}: type={{ type }}</div>
</template>

<script>
export default {
  name: "BuildingBox",

  props: {
    index: {
      type: Number,
      required: true
    },
    type: {
      type: String,
      required: true
    }
  },

  computed: {
    classes() {
      return ["box", "box_" + this.type, { box_first: this.index === 0 }];
    }
  }
};
</script>

<style lang="scss">
$block: ".box";

#{$block} {
  flex: 0 0 calc(100% / 3 - var(--gap) * 4);
  display: flex;
  align-items: center;
  justify-content: center;
  height: 200px;
  margin-top: calc(var(--gap) * 3);
  border: 1px dashed var(--color-border);
  background: #fff;

  &_first {
    flex: 0 0 calc(100% - var(--gap) * 6);
    margin-top: 0;
  }
}
</style>
