<script>
import NoteSelectors from "./NoteSelectors.vue";
import NoteEditor from "./NoteEditor.vue";

export default {
  components: {
    NoteSelectors,
    NoteEditor,
  },
};
</script>

<template>
  <div class="note-container">
    <NoteSelectors />
    <NoteEditor />
  </div>
</template>

<style scoped>
/* LAYOUT */
.note-container {
  display: flex;
  flex: 1;
}
</style>
