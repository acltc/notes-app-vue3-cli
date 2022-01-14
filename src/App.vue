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
  },
};
</script>

<template>
  <div id="app">
    <NoteToolbar />
    <NoteContainer
      v-bind:notes="notes"
      v-bind:selectedNote="selectedNote"
      v-on:selectNote="selectNote"
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
