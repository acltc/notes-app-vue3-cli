<template>
  <div class="note-selector">
    <p class="note-selector-title">First note...</p>
    <p class="note-selector-timestamp">Timestamp here...</p>
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
