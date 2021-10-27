<template>
  <div class="directory">
    <details>
      <summary @click="toggleOpen">
        
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
            :item="content"
          ></dir-comp>

          <single-comp v-else :item="content"></single-comp>
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
  },

  data: function () {
    return {
      opened: false,
    };
  },

  methods: {
    toggleOpen() {
      this.opened = !this.opened;
    },
  },
};
</script>