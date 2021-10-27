<template>
  <div v-click-outside="unselect" :class="['item', {
          'active': selected
        }]" @click="selectItem">
    
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
    }
  },
};
</script>