<template>
  <div class="layout">
    <div class="layout__container">
      <aside class="layout__sidebar">
        <slot name="sidebar" />
      </aside>

      <main class="layout__main">
        <slot />
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainLayout"
};
</script>

<style lang="scss">
$block: ".layout";

#{$block} {
  &__container {
    display: grid;
    grid-template-columns: var(--size-column) 1fr;
    grid-gap: calc(var(--gap) * 1.5);
    max-width: var(--max-width);
    min-width: var(--min-width);
    min-height: 100vh;
    margin: 0 auto;
  }

  &__sidebar,
  &__main {
    background: var(--color-light);
  }
}
</style>
