<script>
import { computed, ref } from "vue";
import NoteToolbar from "./components/NoteToolbar.vue";
import NoteContainer from "./components/NoteContainer.vue";

export default {
  components: {
    NoteToolbar,
    NoteContainer,
  },
  setup: function () {
    const notes = ref([
      { id: 1, body: "This is a first test", timestamp: Date.now() - 2000000 },
      { id: 2, body: "This is a second test", timestamp: Date.now() - 1000000 },
      { id: 3, body: "This is a third test", timestamp: Date.now() },
    ]);
    const selectedNote = ref(notes.value[0]);
    const searchNoteText = ref("");

    const transformedNotes = computed(function () {
      const searchLower = searchNoteText.value.toLowerCase();
      return notes.value
        .filter(function (note) {
          const bodyLower = note.body.toLowerCase();
          return bodyLower.indexOf(searchLower) !== -1;
        })
        .sort(function (a, b) {
          return b.timestamp - a.timestamp;
        });
    });

    return {
      notes,
      selectedNote,
      searchNoteText,
      transformedNotes,
    };
  },
  provide: function () {
    return {
      notes: computed(() => this.transformedNotes),
      selectedNote: computed(() => this.selectedNote),
      selectNote: this.selectNote,
      updateSelectedNote: this.updateSelectedNote,
    };
  },
  methods: {
    selectNote: function (note) {
      this.selectedNote = note;
    },
    updateSelectedNote: function (body) {
      this.selectedNote.body = body;
      this.selectedNote.timestamp = Date.now();
    },
    createNote: function () {
      const newNote = {
        id: Date.now(),
        body: "",
        timestamp: Date.now(),
      };
      this.notes.push(newNote);
      this.selectedNote = newNote;
    },
    deleteNote: function () {
      const index = this.notes.indexOf(this.selectedNote);
      if (index !== -1) {
        this.notes.splice(index, 1);
        if (this.transformedNotes.length > 0) {
          this.selectedNote = this.transformedNotes[0];
        } else {
          this.selectedNote = {};
        }
      }
    },
    updateSearch: function (newSearchText) {
      this.searchNoteText = newSearchText;
      if (this.transformedNotes.length === 0) {
        this.selectedNote = {};
      } else if (this.transformedNotes.indexOf(this.selectedNote) === -1) {
        this.selectedNote = this.transformedNotes[0];
      }
    },
  },
};
</script>

<template>
  <div id="app">
    <NoteToolbar
      v-bind:searchNoteText="searchNoteText"
      v-on:clickNew="createNote"
      v-on:clickDelete="deleteNote"
      v-on:inputSearchNoteText="updateSearch"
    />
    <NoteContainer />
  </div>
</template>

<style>
/* RESET */
* {
  margin: 0;
  padding: 0;
  border: 0;
  outline: none;
  box-sizing: border-box;
}

/* LAYOUT */
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

/* COLORS */
* {
  color: #454545;
  background-color: #fafaf8;
}

/* TYPOGRAPHY */
body {
  font-family: sans-serif;
}
</style>
