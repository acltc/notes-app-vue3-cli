<script>
import NoteSelectors from "./NoteSelectors.vue";
import NoteEditor from "./NoteEditor.vue";

export default {
  components: {
    NoteSelectors,
    NoteEditor,
  },
  props: ["notes", "selectedNote"],
  methods: {
    selectNote: function (note) {
      this.$emit("selectNote", note);
    },
  },
};
</script>

<template>
  <div class="note-container">
    <NoteSelectors
      v-bind:notes="notes"
      v-bind:selectedNote="selectedNote"
      v-on:selectNote="selectNote"
    />
    <NoteEditor v-bind:selectedNote="selectedNote" />
  </div>
</template>

<style scoped>
/* LAYOUT */
.note-container {
  display: flex;
  flex: 1;
}
</style>
