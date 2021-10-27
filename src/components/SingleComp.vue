<template>
  <div v-click-outside="unselect" :class="['item', {
          'active': selected
        }]" @click="selectItem">
    <img :src="getIconUrl(item.type)" alt="" class="icon single-icon">
    {{ item.name }}
  </div>
</template>

<script>
import clickOutside from "../utils/directives/clickOutside";

export default {
  name: "SingleComp",

  directives: {
    clickOutside
  },

  props: {
    item: {
      type: Object,
      default: () => {},
    },
  },

  data: () => ({
    selected: false
  }),

  methods: {
    selectItem () {
      this.selected = !this.selected
    },
    unselect() {
      this.selected = false
    },
    getIconUrl(type) {
      const icons = require.context('../assets/icons/', false, /\.svg$/)
      return icons('./' + type + '.svg')
    }
  },
};
</script>