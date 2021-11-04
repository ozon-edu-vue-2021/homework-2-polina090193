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
  </div>
</template>

<script>

export default {
  name: "SingleComp",

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

  inject: ["getSelectedPath"],

  computed: {
    selectedPath() {
      return this.getSelectedPath();
    },
    selected() {
      return this.selectedPath === this.compPath
    },
  },

  data() {
    return {
      compPath: this.path + this.item.name,
    };
  },

  methods: {
    selectItem(e) {
      this.$emit("select-item", e, this.compPath);
    },
    getIconUrl(type) {
      const icons = require.context("../assets/icons/", false, /\.svg$/);
      return icons("./" + type + ".svg");
    },
  },
};
</script>