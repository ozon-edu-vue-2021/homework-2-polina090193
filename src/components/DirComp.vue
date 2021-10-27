<template>
  <div class="directory">
    <details>
      <summary>
        <v-icon>{{ "mdi-folder" }}</v-icon>
        {{ item.name }}
      </summary>

      <nav
        class="directory-items"
        v-for="(content, i) in item.contents"
        :key="i"
      >
          <dir-comp v-if="content.type === 'directory'" :item="content"></dir-comp>

          <single-comp v-else :item="content"></single-comp>
      </nav>
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
};
</script>