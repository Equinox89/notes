<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1>{{ title }}</h1>

          <Message v-if="message" :message="message"/>
          <NewNote :note="note" @addNewNote="addNewNote"/>
          <!--note list-->
          <div class="notes">
            <div class="note" v-for="(note, index) in notes" :key="index">
              <div class="note-header">
                <p>{{ note.title }}</p>
              </div>
              <div class="note-body">
                <p>{{ note.description }}</p>
                <span>{{ note.date }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>

    </div>
  </div>
</template>

<script>

import Message from "@/components/Message.vue";
import NewNote from "@/components/NewNote.vue";

export default {
  components: {NewNote, Message},
  data() {
    return {
      title: 'Notes App',
      message: null,
      note: {
          title: '',
          description: '',
      },
      notes: [
        {
          title: 'First note',
          description: 'Some Description',
          date: new Date().toLocaleString()
        },
        {
          title: 'Second note',
          description: 'Some Description',
          date: new Date().toLocaleString()
        },
        {
          title: 'Thirs note',
          description: 'Some Description',
          date: new Date().toLocaleString()
        },
      ]
    }
  },
  methods: {
    addNewNote () {
      let { title, description } = this.note

      if(title) {
        this.notes.push({
          title,
          description,
          date: new Date().toLocaleString()
        })

        this.note.title = ''
        this.note.description = ''
        this.message = null

      } else {
        this.message = 'This field can\'t be blank!'
        return false
      }
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 800px;
}
</style>
