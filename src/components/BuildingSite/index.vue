<template>
  <div class="building-site">
    <div class="building-site__feed">
      <template v-for="(block, index) in blocks">
        <div
          v-if="index === 0 || 1 - (index % 3) === 0"
          :key="index + 0.5"
          :data-index="index"
          class="building-site__space"
        >
          {{ index }}
        </div>
        <div
          :key="index * 2 + 1"
          :class="[
            'building-site__block',
            'building-site__block_' + block,
            { 'building-site__block_first': index === 0 }
          ]"
        >
          {{ index }}: type={{ block.type }}
        </div>
        <div
          :key="index * 2 + 2"
          :data-index="index + 1"
          class="building-site__space"
        >
          {{ index + 1 }}
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "BuildingSite",

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
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
$block: ".building-site";

#{$block} {
  overflow: hidden;
  padding: calc(var(--gap) * 3) 0;

  &__feed {
    display: flex;
    flex-wrap: wrap;
    align-items: flex-end;
  }

  &__block {
    flex: 0 0 calc(100% / 3 - var(--gap) * 4);
    display: flex;
    align-items: center;
    justify-content: center;
    height: 200px;
    margin-top: calc(var(--gap) * 3);
    border: 1px dashed var(--color-border);

    &_first {
      flex: 0 0 calc(100% - var(--gap) * 6);
      margin-top: 0;
    }
  }

  &__space {
    flex: 0 0 calc(var(--gap) * 3);
    display: flex;
    align-items: center;
    justify-content: center;
    height: 200px;
    background: #dadada;
  }
}
</style>
