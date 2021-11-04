<template>
  <div class="directory">
    <details>
      <summary @click="toggleOpen">
        <img src="../assets/icons/folder.svg" alt="" class="icon directory-icon">
        {{ item.name }}
      </summary>

      <div v-if="opened" class="directory-inner">
        <nav
          class="directory-items"
          v-for="(content, i) in item.contents"
          :key="i"
        >
          <dir-comp
            v-if="content.type === 'directory'"
            :item="content" v-on="$listeners" :path="compPath"
          ></dir-comp>

          <single-comp :path="compPath" v-else :item="content" v-on="$listeners"></single-comp>
        </nav>
      </div>
    </details>
  </div>
</template>

<script>
import SingleComp from "./SingleComp";

export default {
  name: "DirComp",

  components: { SingleComp },

  props: {
    item: {
      type: Object,
      default: () => {},
    },
    path: {
      type: String,
      default: '',
    }
  },

  data: function () {
    return {
      opened: false,
      compPath: this.path + this.item.name + '/',
    }
  },

  provide() {
    return {
      selectedItem: this.selectedItem,
    };
  },

  methods: {
    toggleOpen() {
      this.opened = !this.opened;
    },
  },
};
</script>