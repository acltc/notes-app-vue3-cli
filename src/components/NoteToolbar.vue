<script>
export default {
  methods: {
    clickNew: function () {
      this.$emit("clickNew");
    },
  },
};
</script>

<template>
  <div class="toolbar">
    <button v-on:click="clickNew" class="toolbar-button toolbar-button-new">New</button>
    <button class="toolbar-button toolbar-button-delete">Delete</button>
    <input class="toolbar-search" type="text" placeholder="Search..." />
  </div>
</template>

<style scoped>
/* LAYOUT */
.toolbar {
  padding: 0.5em;
}
.toolbar-button,
.toolbar-search {
  padding: inherit;
  border-radius: 0.3em;
}
.toolbar-search {
  float: right;
}

/* COLORS */
.toolbar {
  background-color: #dcdadc;
}
.toolbar-button {
  background-color: #ffffff;
}
.toolbar-button:active {
  background-color: #aaaaaa;
}
</style>
