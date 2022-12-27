<template>
  <!--note list-->
  <div class="notes">
    <div class="note" v-for="(note, index) in notes" :key="index">
      <div class="note-header">
        <p>{{ note.title }}</p>
        <p style="cursor: pointer" @click="removeNote(index)">x</p>
      </div>
      <div class="note-body">
        <p>{{ note.description }}</p>
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true
    }
  },
  methods: {
    removeNote(index) {
      this.$emit('remove', index)
    }
  },
  name: "Notes"
}
</script>

<style lang="scss">
  .notes {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 40px 0;
  }

  .note {
    width: calc(50% - 8px);
    padding: 18px 20px;
    margin-bottom: 16px;
    background-color: #ffffff;
    border-radius: 8px;
  }

  .note-header {
    display: flex;
    align-items: center;
    justify-content: space-between;

    p {
      font-size: 24px;
      color: #0949ec;
    }
  }
  .note-body {
    p {
      margin: 16px 0;
    }
    span {
      font-size: 14px;
      color: #999;
    }
  }
</style>