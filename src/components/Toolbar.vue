<template>
  <div class="toolbar">
    <div class="toolbar__list">
      <div
        v-for="(control, index) in controls"
        :key="index"
        class="toolbar__item"
      >
        <div class="toolbar__control" role="button">
          <div class="toolbar__view">
            <ui-icon :name="control.type" :size="72" class="toolbar__icon" />
            <div v-if="control.label" class="toolbar__label">
              {{ control.label }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Toolbar",

  data() {
    return {
      controls: [
        {
          type: "placeholder",
          label: "Placeholder"
        },
        {
          type: "image",
          label: "Image"
        },
        {
          type: "text",
          label: "Text"
        },
        {
          type: "basket"
        }
      ]
    };
  }
};
</script>

<style lang="scss">
@import "@/styles/_mixins.scss";

$block: ".toolbar";

#{$block} {
  padding: calc(var(--gap) * 3) var(--gap);

  &__item {
    &:not(:first-child) {
      margin-top: var(--gap);
    }
  }

  &__control {
    @extend %resetButton;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: calc(var(--size-column) - var(--gap) * 2);
    border-radius: var(--border-raius);
    background: var(--color-gray);
    text-align: center;
  }

  &__icon {
    margin: 0 auto;
  }

  &__label {
    margin: calc(var(--gap) / 2) 0 0;
    color: var(--color-text-secondary);
    font-size: 12px;
    font-weight: bold;
    line-height: 1;
    text-transform: uppercase;
  }
}
</style>
