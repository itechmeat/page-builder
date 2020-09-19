<template>
  <div>
    <b />
    <i />
    <b />
    <i />
  </div>
</template>

<script>
export default {
  name: "IconText",

  props: {
    size: {
      type: Number
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

  b,
  i {
    flex: 0 0 2px;
    display: block;
    height: 2px;
    margin: calc(100% / 12) 0;
    background: var(--color-text);
  }

  i {
    margin-right: 30%;
  }
}
</style>
