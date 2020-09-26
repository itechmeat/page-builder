<template>
  <div
    :class="[
      'building-site dropzone',
      { 'building-site_active': dragActive },
      { 'building-site_focused': isDropZoneActive }
    ]"
    @dragover.prevent
    @drop.stop.prevent="handleDrop"
  >
    <div class="building-site__feed dropzone">
      <template v-for="(card, index) in cards">
        <BuildingGap
          v-if="index === 0 || 1 - (index % 3) === 0"
          :key="index + 0.5"
          :index="index"
          :active="activeIndex === index"
        />

        <BuildingCard
          :key="index * 2 + 1"
          :index="index"
          :value="card"
          :active="index === cardIndex"
        />

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
import BuildingCard from "@/components/BuildingSite/Card";
import BuildingGap from "@/components/BuildingSite/Gap";

export default {
  name: "BuildingSite",

  components: {
    BuildingCard,
    BuildingGap
  },

  props: {
    dragActive: Boolean,
    draggedType: {
      type: String,
      default: null
    },
    cardIndex: {
      type: Number,
      default: null
    }
  },

  data() {
    return {
      cards: [
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
      isDropZoneActive: false,
      newIndex: null
    };
  },

  computed: {
    activeIndex() {
      if (!this.isDropZoneActive && this.newIndex === null) {
        return;
      }

      if (this.newIndex === 0) {
        return 0;
      }

      return this.newIndex || this.cards.length;
    }
  },

  methods: {
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
      if (this.activeIndex !== undefined) {
        if (this.draggedType) {
          this.cards.splice(this.activeIndex, 0, {
            type: this.draggedType,
            content: ""
          });
        }

        if (this.cardIndex || this.cardIndex === 0) {
          const card = this.cards[this.cardIndex];
          if (this.cardIndex < this.activeIndex) {
            this.cards.splice(this.activeIndex, 0, card);
            this.cards.splice(this.cardIndex, 1);
          } else {
            this.cards.splice(this.cardIndex, 1);
            this.cards.splice(this.activeIndex, 0, card);
          }
        }
      }

      this.$nextTick(() => {
        this.$emit("clear");
        this.newIndex = null;
        this.dragged = null;
        this.isDropZoneActive = false;
      });
    },

    removeCard(index) {
      this.cards.splice(index, 1);
    }
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
