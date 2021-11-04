<template>
  <div id="app">
    <div class="tree components-tree">
      <p class="title">Selected Item: {{selectedPath || 'Nothing is selected'}}</p>
      <div class="directories-root" v-for="(item, i) in items" :key="i">
        <nav v-if="item.type === 'directory'">
          <dir-comp :item="item" :path="path" @select-item="selectItem"></dir-comp>
        </nav>

        <nav v-else>
          <single-comp :path="path" :item="content" @select-item="selectItem"></single-comp>
        </nav>
      </div>
    </div>
  </div>
</template>

<script>
import items from "../public/static/node_modules.json";
import DirComp from "./components/DirComp";
import SingleComp from "./components/SingleComp";

export default {
  components: { DirComp, SingleComp },
  data: () => ({
    items: [items],
    selectedPath: '',
    path: 'Root/'
  }),
  provide() {
    return {
      selectedPath: this.selectedPath,
    };
  },
  methods: {
    selectItem(e, pathToComp) {
      this.selectedPath = pathToComp;
    },
  }
};
</script>

<style lang="scss">
.tree {
  margin: 3rem;
}
.item,
.directory {
  cursor: pointer;
  margin-left: 20px;
  margin-top: 10px;
}
.item {
  &:hover,
  &.active {
    background-color: #e4e4e4;
  }
}
.icon {
  position: relative;
  top: 5px;
  width: 20px;
  height: 20px;
  margin-right: 5px;
}
</style>
