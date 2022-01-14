<script>
export default {
  props: ["searchNoteText"],
  methods: {
    clickNew: function () {
      this.$emit("clickNew");
    },
    clickDelete: function () {
      this.$emit("clickDelete");
    },
    input: function (event) {
      this.$emit("inputSearchNoteText", event.target.value);
    },
  },
};
</script>

<template>
  <div class="toolbar">
    <button v-on:click="clickNew" class="toolbar-button toolbar-button-new">New</button>
    <button v-on:click="clickDelete" class="toolbar-button toolbar-button-delete">Delete</button>
    <input
      v-bind:value="searchNoteText"
      v-on:input="input"
      class="toolbar-search"
      type="text"
      placeholder="Search..."
    />
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
