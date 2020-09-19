<template>
  <component
    :is="icon + '-icon'"
    :style="styles"
    :size="size"
    :title="name"
    :class="classes"
  />
</template>

<script>
import PlaceholderIcon from "./Placeholder";
import UploadIcon from "./Upload";
import BasketIcon from "./Basket";
import ImageIcon from "./Image";
import CloseIcon from "./Close";
import TextIcon from "./Text";

const ICONS = ["placeholder", "upload", "basket", "image", "close", "text"];

export default {
  name: "UiIcon",

  components: {
    PlaceholderIcon,
    UploadIcon,
    BasketIcon,
    ImageIcon,
    CloseIcon,
    TextIcon
  },

  props: {
    name: {
      type: String,
      required: true
    },
    size: {
      type: Number,
      default: 18
    },
    color: Boolean
  },

  computed: {
    icon() {
      if (!ICONS.includes(this.name)) {
        return "close";
      }

      return this.name;
    },

    classes() {
      return ["ui-icon", { "ui-icon_color": this.color }];
    },

    styles() {
      return {
        width: this.size + "px",
        height: this.size + "px"
      };
    }
  }
};
</script>

<style lang="scss">
$block: ".ui-icon";

#{$block} {
  display: inline-block;
  font-size: 10px;
  vertical-align: middle;
}
</style>
