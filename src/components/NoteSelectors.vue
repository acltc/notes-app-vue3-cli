<script>
import NoteSelector from "./NoteSelector.vue";

export default {
  components: {
    NoteSelector,
  },
  inject: ["notes", "selectedNote", "selectNote"],
  methods: {
    onClickNote: function (note) {
      this.selectNote(note);
    },
  },
};
</script>

<template>
  <div class="note-selectors">
    <NoteSelector
      v-for="note in notes"
      v-bind:key="note.id"
      v-bind:note="note"
      v-bind:selectedNote="selectedNote"
      v-on:click="onClickNote(note)"
    />
  </div>
</template>

<style scoped>
/* LAYOUT */
.note-selectors {
  flex: 0 0 13em;
}

/* COLORS */
.note-selectors {
  border-right: 1px solid #dcdadc;
}
</style>
