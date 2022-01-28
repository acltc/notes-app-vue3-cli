<script>
import { computed, provide, readonly, ref } from "vue";
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

    const selectNote = function (note) {
      selectedNote.value = note;
    };

    const updateSelectedNote = function (body) {
      selectedNote.value.body = body;
      selectedNote.value.timestamp = Date.now();
    };

    const createNote = function () {
      const newNote = {
        id: Date.now(),
        body: "",
        timestamp: Date.now(),
      };
      notes.value.push(newNote);
      selectedNote.value = newNote;
    };

    const deleteNote = function () {
      const index = notes.value.indexOf(selectedNote.value);
      if (index !== -1) {
        notes.value.splice(index, 1);
        if (transformedNotes.value.length > 0) {
          selectedNote.value = transformedNotes.value[0];
        } else {
          selectedNote.value = {};
        }
      }
    };

    const updateSearch = function (newSearchText) {
      searchNoteText.value = newSearchText;
      if (transformedNotes.value.length === 0) {
        selectedNote.value = {};
      } else if (transformedNotes.value.indexOf(selectedNote.value) === -1) {
        selectedNote.value = transformedNotes.value[0];
      }
    };

    provide("notes", readonly(transformedNotes));
    provide("selectedNote", readonly(selectedNote));
    provide("selectNote", selectNote);
    provide("updateSelectedNote", updateSelectedNote);

    return {
      notes,
      selectedNote,
      searchNoteText,
      transformedNotes,
      selectNote,
      updateSelectedNote,
      createNote,
      deleteNote,
      updateSearch,
    };
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
