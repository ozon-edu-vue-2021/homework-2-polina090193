<template>
  <div class="item" @click="toggleActive">
    <v-icon v-if="item.type === 'file'">
      {{ "mdi-file-document-outline" }}
    </v-icon>
    <v-icon v-else-if="item.type === 'link'">
      {{ "mdi-link" }}
    </v-icon>
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
  },

  methods: {
    toggleActive(e) {
      e.target.classList.toggle('active')
    }
  }
};
</script>

<style lang="scss">
  .item {
    &:hover, &.active {
      background-color: #e4e4e4;
    }
  }
</style>