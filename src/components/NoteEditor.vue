<script>
export default {
  inject: ["selectedNote", "updateSelectedNote"],
  methods: {
    formatTimestamp: function (timestamp) {
      return new Date(timestamp).toUTCString();
    },
    input: function (event) {
      this.updateSelectedNote(event.target.value);
    },
  },
};
</script>

<template>
  <div v-if="selectedNote.id" class="note-editor">
    <p class="note-editor-info">{{ formatTimestamp(selectedNote.timestamp) }}</p>
    <textarea
      v-bind:value="selectedNote.body"
      v-on:input="input"
      class="note-editor-input"
    ></textarea>
  </div>
</template>

<style scoped>
/* LAYOUT */
.note-editor {
  display: flex;
  flex: 1;
  flex-direction: column;
}
.note-editor-info {
  padding: 0.5em;
  text-align: center;
}
.note-editor-input {
  display: flex;
  flex: 1;
  width: 100%;
  padding: 0 2em 0 2em;
}

/* COLORS */
.note-editor-info {
  color: #dcdadc;
}

/* TYPOGRAPHY */
.note-editor,
.note-editor-input {
  font-size: 0.9em;
}
</style>
