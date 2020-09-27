<template>
  <label class="ui-upload-button">
    <input type="file" class="ui-upload-button__input" @change="handleFile" />
    <ui-icon name="upload" :size="16" color class="ui-upload-button__icon" />
    <span class="ui-upload-button__label">{{ label }}</span>
  </label>
</template>

<script>
export default {
  name: "UiUploadButton",

  props: {
    label: {
      type: String,
      default: "Upload"
    }
  },

  methods: {
    handleFile(val) {
      this.$emit("change", val);
    }
  }
};
</script>

<style lang="scss" scoped>
$block: ".ui-upload-button";

#{$block} {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  position: relative;
  height: 28px;
  padding: 0 var(--gap);
  border-radius: var(--border-raius);
  background: var(--color-gray);
  cursor: pointer;

  &:hover {
    background: var(--color-text-hint);
  }

  &__input {
    position: absolute;
    left: -9999px;
  }

  &__icon {
    vertical-align: middle;
  }

  &__label {
    display: inline-block;
    font-size: var(--font-size-tiny);
    font-weight: bold;
    text-transform: uppercase;
    vertical-align: middle;
  }
}
</style>
