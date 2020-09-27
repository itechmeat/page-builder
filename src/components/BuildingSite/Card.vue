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

        <div ref="image" v-else-if="value.type === 'image'" class="card__image">
          <input v-if="!value.content" type="file" @change="handleFile" />
          <img
            v-else
            ref="photo"
            :src="value.content"
            alt=""
            class="card__photo"
          />
        </div>

        <div v-else>{{ index }}: type={{ value.type }}</div>

        <button
          ref="clear"
          v-if="value.content"
          class="card__clear"
          @click="handleClear"
        >
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

    handleFile(event) {
      const file = event.target.files[0];
      const reader = new FileReader();

      reader.onloadend = () => {
        this.value.content = reader.result;
      };

      if (file) {
        reader.readAsDataURL(file);
      } else {
        this.value.content = null;
      }
    },

    handleClear() {
      this.value.content = null;
      this.$refs.clear.blur();

      if (this.value.type === "image") {
        const preview = this.$refs.photo;
        this.value.content = null;
        preview.src = "";
      }
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
  cursor: move;

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

  &__text,
  &__image {
    height: 134px;
    margin: var(--gap);
    margin-right: calc(var(--gap) * 2);
    line-height: 1.4;
  }

  &__text {
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 6;
    -webkit-box-orient: vertical;
    outline: none;
  }

  &__image {
    cursor: default;
  }

  &__photo {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
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
