<script>
export default {
  props: ["searchNoteText"],
  setup: function (props, context) {
    console.log(props.searchNoteText);

    const clickNew = function () {
      context.emit("clickNew");
    };

    const clickDelete = function () {
      context.emit("clickDelete");
    };

    const input = function (event) {
      context.emit("inputSearchNoteText", event.target.value);
    };

    return { clickNew, clickDelete, input };
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
