<template>
  <div
    :class="[
      'item',
      {
        active: selected,
      },
    ]"
    @click="selectItem"
  >
    <img :src="getIconUrl(item.type)" alt="" class="icon single-icon" />
    {{ item.name }}
    <!-- v-click-outside="unselect" -->
  </div>
</template>

<script>
// import clickOutside from "../utils/directives/clickOutside";

export default {
  name: "SingleComp",

  /* directives: {
    clickOutside
  }, */

  props: {
    item: {
      type: Object,
      default: () => {},
    },
    path: {
      type: String,
      default: "",
    },
  },

  inject: ["selectedPath"],

  data() {
    return {
      compPath: this.path + this.item.name,
      selected: this.selectedPath === this.path,
    };
  },

  methods: {
    selectItem(e) {
      // this.selected = !this.selected
      this.$emit("select-item", e, this.compPath);
    },
    /* unselect() {
      this.selected = false
      this.$emit('unselect-item')
    }, */
    getIconUrl(type) {
      const icons = require.context("../assets/icons/", false, /\.svg$/);
      return icons("./" + type + ".svg");
    },
  },
};
</script>