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

    <div class="tree vuetify-tree">
      <h1 class="title">Vuetify</h1>
      <v-treeview
        v-model="tree"
        :items="items"
        :item-children="'contents'"
        activatable
        open-on-click
      >
        <template v-slot:prepend="{ item }">
          <v-icon v-if="item.type === 'directory'">
            {{ "mdi-folder" }}
          </v-icon>
          <v-icon v-else-if="item.type === 'file'">
            {{ "mdi-file-document-outline" }}
          </v-icon>
          <v-icon v-else-if="item.type === 'link'">
            {{ "mdi-link" }}
          </v-icon>
        </template>
      </v-treeview>
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
    tree: [],
  }),
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
</style>
