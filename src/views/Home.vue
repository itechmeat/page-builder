<template>
  <main-layout>
    <Toolbar slot="sidebar" />

    <building-site />
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
  }
};
</script>
