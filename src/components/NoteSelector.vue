<script>
export default {
  props: ["note", "selectedNote"],
  methods: {
    formatTitle: function (body) {
      const maxLength = 20;
      if (body.length > maxLength) {
        return body.substring(0, maxLength - 3) + "...";
      } else if (body.length === 0) {
        return "New note";
      } else {
        return body;
      }
    },
    formatTimestamp: function (timestamp) {
      return new Date(timestamp).toUTCString();
    },
  },
};
</script>

<template>
  <div class="note-selector" v-bind:class="{ active: note === selectedNote }">
    <p class="note-selector-title">{{ formatTitle(note.body) }}</p>
    <p class="note-selector-timestamp">{{ formatTimestamp(note.timestamp) }}</p>
  </div>
</template>

<style scoped>
/* LAYOUT */
.note-selector {
  padding: 1em;
}
.note-selector p {
  margin: 0;
}

/* COLORS */
.note-selector {
  border-bottom: 1px solid #dcdadc;
}
.note-selector.active {
  background-color: #fce18d;
}
.note-selector-title {
  background-color: inherit;
}
.note-selector-timestamp {
  color: #626262;
  background-color: inherit;
}

/* TYPOGRAPHY */
.note-selector-title {
  font-weight: bold;
}
.note-selector-timestamp {
  font-size: 0.7em;
}
</style>
