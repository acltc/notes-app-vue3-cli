<script>
import NoteSelector from "./NoteSelector.vue";

export default {
  components: {
    NoteSelector,
  },
  props: ["notes"],
  computed: {
    transformedNotes: function () {
      return this.notes.slice().sort(function (a, b) {
        return b.timestamp - a.timestamp;
      });
    },
  },
};
</script>

<template>
  <div class="note-selectors">
    <NoteSelector v-for="note in transformedNotes" v-bind:key="note.id" v-bind:note="note" />
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
