<template>
  <main-layout>
    <Toolbar slot="sidebar" :active-type="activeType" />

    <BuildingSite @drag="handleDrag" />
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
      activeType: null
    };
  },

  methods: {
    handleDrag(type) {
      this.activeType = type;
    }
  }
};
</script>
