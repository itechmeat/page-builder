<template>
  <main-layout>
    <Toolbar
      slot="sidebar"
      :active-type="draggedType"
      :deleting="deleting"
      :deleting-error="deletingError"
      @delete="removeCard"
    />

    <BuildingSite
      ref="builder"
      v-model="cards"
      :drag-active="isDragActive"
      :dragged-type="draggedType"
      :card-index="cardIndex"
      @clear="clearData"
    />
  </main-layout>
</template>

<script>
import Toolbar from "@/components/Toolbar";
import BuildingSite from "@/components/BuildingSite";

export default {
  name: "Home",

  components: {
    Toolbar,
    BuildingSite
  },

  data() {
    return {
      cards: [],
      isDragActive: false,
      draggedType: null,
      cardIndex: null,
      deleting: false,
      deletingError: false
    };
  },

  mounted() {
    document.addEventListener(
      "dragstart",
      event => this.handleDrag(event, true),
      false
    );

    document.addEventListener(
      "dragend",
      event => this.handleDrag(event, false),
      false
    );

    document.addEventListener(
      "dragenter",
      event => this.handleDropZone(event, true),
      false
    );

    document.addEventListener(
      "dragleave",
      event => this.handleDropZone(event, false),
      false
    );
  },

  methods: {
    handleDrag(event, state) {
      this.isDragActive = state;
      let type = null;
      let cardIndex;
      if (state) {
        type = event.target.dataset.control;
        cardIndex = Number(event.target.dataset.card);
      }
      this.draggedType = type;
      this.cardIndex = cardIndex;
    },

    handleDropZone(event, state) {
      if (!this.$refs || !this.$refs.builder) {
        return;
      }

      this.$refs.builder.handleDropZone(event, state);

      if (event.target.className.includes("dropbasket")) {
        if (isNaN(this.cardIndex)) {
          this.deletingError = state;
          return;
        }
        this.deleting = state;
      }
    },

    removeCard() {
      if (this.deletingError) {
        this.clearData();
        return;
      }
      this.$refs.builder.removeCard(this.cardIndex);
      this.clearData();
    },

    clearData() {
      this.draggedType = null;
      this.isDragActive = false;
      this.deleting = false;
      this.deletingError = false;
    }
  },

  beforeDestroy() {
    document.removeEventListener(
      "dragstart",
      event => this.handleDrag(event, true),
      false
    );

    document.removeEventListener(
      "dragend",
      event => this.handleDrag(event, false),
      false
    );

    document.removeEventListener(
      "dragenter",
      event => this.handleDropZone(event, true),
      false
    );

    document.removeEventListener(
      "dragleave",
      event => this.handleDropZone(event, false),
      false
    );
  }
};
</script>
