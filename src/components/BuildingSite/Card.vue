<template>
  <div :class="classes">
    <div class="card__box" draggable="true" :data-card="index">
      <div
        v-if="value.type !== 'placeholder'"
        class="card__content"
        @click.self="handleContentClick"
      >
        <div
          ref="text"
          v-if="value.type === 'text'"
          class="card__text"
          contenteditable
          v-html="value.content || '&nbsp;'"
          @blur="handleTextBlur"
        />
        <div v-else>{{ index }}: type={{ value.type }}</div>
        <button ref="clear" class="card__clear" @click="handleClear">
          <ui-icon name="close" :size="24" color class="card__icon" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { clearText } from "@/libs/utils";

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
  },

  methods: {
    handleContentClick() {
      if (this.value.type === "text") {
        this.$refs.text.focus();
      }
    },

    handleTextBlur(e) {
      this.value.content = clearText(e.target.innerHTML);
    },

    handleClear() {
      this.value.content = null;
      this.$refs.clear.blur();
    }
  }
};
</script>

<style lang="scss">
@import "@/styles/_mixins.scss";

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

  &__box {
    @extend %fill;
    border: 1px dashed var(--color-border);

    #{$block}_active & {
      opacity: 0.3;
    }
  }

  &__content {
    overflow: hidden;
    position: absolute;
    top: var(--gap);
    right: var(--gap);
    bottom: var(--gap);
    left: var(--gap);
    background: var(--color-bg);

    #{$block}_text & {
      cursor: text;
    }

    &:focus-within {
      background: var(--color-text-hint);
    }
  }

  &__text {
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 6;
    -webkit-box-orient: vertical;
    height: 134px;
    margin: var(--gap);
    margin-right: calc(var(--gap) * 2);
    line-height: 1.4;
    outline: none;
  }

  &__clear {
    @extend %resetButton;
    position: absolute;
    top: calc(var(--gap) / 2);
    right: calc(var(--gap) / 2);
    outline: none;
  }
}
</style>
