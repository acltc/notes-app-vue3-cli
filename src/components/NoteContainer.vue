<script>
import NoteSelectors from "./NoteSelectors.vue";
import NoteEditor from "./NoteEditor.vue";

export default {
  components: {
    NoteSelectors,
    NoteEditor,
  },
  methods: {
    selectNote: function (note) {
      this.$emit("selectNote", note);
    },
    inputNoteEditor: function (body) {
      this.$emit("inputNoteEditor", body);
    },
  },
};
</script>

<template>
  <div class="note-container">
    <NoteSelectors v-on:selectNote="selectNote" />
    <NoteEditor v-on:inputNoteEditor="inputNoteEditor" />
  </div>
</template>

<style scoped>
/* LAYOUT */
.note-container {
  display: flex;
  flex: 1;
}
</style>
