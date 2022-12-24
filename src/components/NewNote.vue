<template>
  <!--new-note-->
  <div class="new-note">
    <label for="">Title</label>
    <input type="text" v-model="note.title">
    <label for="">Description</label>
    <textarea v-model="note.description"></textarea>
    <button class="btn btnPrimary" @click="addNewNote">Add new note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true
    }
  },
  name: "NewNote",
  methods: {
    addNewNote() {
      this.$emit('addNewNote', this.note)
    }
  }
}
</script>

<style lang="scss">
  .new-note {
    text-align: center;
  }
</style>