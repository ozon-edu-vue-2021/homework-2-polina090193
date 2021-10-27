<template>
  <div id="app">
    <div class="tree components-tree">
      <h1 class="title">Components</h1>
      <div class="directories-root" v-for="(item, i) in items" :key="i">
        <nav v-if="item.type === 'directory'">
          <dir-comp :item="item"></dir-comp>
        </nav>

        <nav v-else>
          <single-comp :item="content"></single-comp>
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
  })

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
  &:hover, &.active {
    background-color: #e4e4e4;
  }
}
</style>
