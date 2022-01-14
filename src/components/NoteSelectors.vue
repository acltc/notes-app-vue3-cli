<script>
import NoteSelector from "./NoteSelector.vue";

export default {
  components: {
    NoteSelector,
  },
  props: ["notes", "selectedNote"],
  computed: {
    transformedNotes: function () {
      return this.notes.slice().sort(function (a, b) {
        return b.timestamp - a.timestamp;
      });
    },
  },
  methods: {
    selectNote: function (note) {
      this.$emit("selectNote", note);
    },
  },
};
</script>

<template>
  <div class="note-selectors">
    <NoteSelector
      v-for="note in transformedNotes"
      v-bind:key="note.id"
      v-bind:note="note"
      v-bind:selectedNote="selectedNote"
      v-on:click="selectNote(note)"
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
