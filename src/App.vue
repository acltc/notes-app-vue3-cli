<script>
import NoteToolbar from "./components/NoteToolbar.vue";
import NoteContainer from "./components/NoteContainer.vue";

export default {
  components: {
    NoteToolbar,
    NoteContainer,
  },
  data: function () {
    return {
      notes: [],
      selectedNote: {},
    };
  },
  computed: {
    transformedNotes: function () {
      return this.notes.slice().sort(function (a, b) {
        return b.timestamp - a.timestamp;
      });
    },
  },
  created: function () {
    this.notes = [
      { id: 1, body: "This is a first test", timestamp: Date.now() - 2000000 },
      { id: 2, body: "This is a second test", timestamp: Date.now() - 1000000 },
      { id: 3, body: "This is a third test", timestamp: Date.now() },
    ];
    this.selectedNote = this.notes[0];
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
  },
};
</script>

<template>
  <div id="app">
    <NoteToolbar v-on:clickNew="createNote" v-on:clickDelete="deleteNote" />
    <NoteContainer
      v-bind:notes="transformedNotes"
      v-bind:selectedNote="selectedNote"
      v-on:selectNote="selectNote"
      v-on:inputNoteEditor="updateSelectedNote"
    />
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
