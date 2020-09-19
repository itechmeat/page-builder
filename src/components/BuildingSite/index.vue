<template>
  <div
    :class="[
      'building-site dropzone',
      { 'building-site_active': idDragActive },
      { 'building-site_focused': isDropZoneActive }
    ]"
    @dragover.prevent
    @drop.stop.prevent="handleDrop"
  >
    <div class="building-site__feed dropzone">
      <template v-for="(block, index) in blocks">
        <BuildingGap
          v-if="index === 0 || 1 - (index % 3) === 0"
          :key="index + 0.5"
          :index="index"
          :active="activeIndex === index"
        />

        <BuildingBox :key="index * 2 + 1" :index="index" :type="block.type" />

        <BuildingGap
          :key="index * 2 + 2"
          :index="index + 1"
          :active="activeIndex === index + 1"
        />
      </template>
    </div>
  </div>
</template>

<script>
import BuildingBox from "@/components/BuildingSite/Box";
import BuildingGap from "@/components/BuildingSite/Gap";

export default {
  name: "BuildingSite",

  components: {
    BuildingBox,
    BuildingGap
  },

  data() {
    return {
      blocks: [
        {
          type: "image",
          content: ""
        },
        {
          type: "text",
          content: ""
        },
        {
          type: "placeholder"
        },
        {
          type: "image",
          content: ""
        },
        {
          type: "image",
          content: ""
        },
        {
          type: "text",
          content: ""
        }
      ],
      idDragActive: false,
      isDropZoneActive: false,
      newIndex: null,
      draggedType: null
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

  computed: {
    activeIndex() {
      if (!this.isDropZoneActive && this.newIndex === null) {
        return;
      }

      if (this.newIndex === 0) {
        return 0;
      }

      return this.newIndex || this.blocks.length;
    }
  },

  methods: {
    handleDrag(event, state) {
      this.idDragActive = state;
      let type = null;
      if (state) {
        type = event.target.dataset.control;
      }
      this.draggedType = type;
    },

    handleDropZone(event, state) {
      if (event.target.className.includes("dropzone")) {
        if (state) {
          this.newIndex = null;
        }
        this.isDropZoneActive = state;
        return;
      }

      if (event.target.className.includes("dropspace")) {
        if (!state) {
          this.newIndex = null;
          return;
        }
        this.newIndex = Number(event.target.dataset.index);
      }
    },

    handleDrop() {
      if (this.activeIndex) {
        this.blocks.splice(this.activeIndex, 0, {
          type: this.draggedType,
          content: ""
        });
      }

      this.$nextTick(() => {
        this.newIndex = null;
        this.dragged = null;
        this.draggedType = null;
        this.isDropZoneActive = false;
      });
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

<style lang="scss">
$block: ".building-site";

#{$block} {
  overflow: hidden;
  min-height: 100%;
  padding: calc(var(--gap) * 3) 0;
  transition: background 0.1s;
  will-change: background;

  &_active {
    background: rgba(#0066ff, 0.1);
  }

  &_focused {
    background: rgba(#0066ff, 0.13);
  }

  &__feed {
    display: flex;
    flex-wrap: wrap;
    align-items: flex-end;
  }
}
</style>
