<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <Message v-if="message" :message="message"/>
          <NewNote :note="note" @addNewNote="addNewNote"/>
          <div class="note-header">
            <h1>{{ title }}</h1>
            <Search :value="search" @search="search = $event"/>
            <div>
              <svg :class="{ active:grid }" @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg :class="{ active:!grid }" @click="grid = false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>
          <Notes :notes="notesFilter" :grid="grid" @remove="removeNote"/>
        </div>
      </section>

    </div>
  </div>
</template>

<script>

import Message from "@/components/Message.vue";
import NewNote from "@/components/NewNote.vue";
import Notes from "@/components/Notes.vue";
import Search from "@/components/Search.vue";

export default {
  components: {Search, Notes, NewNote, Message},
  data() {
    return {
      title: 'Notes App',
      search: '',
      message: null,
      grid: true,
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
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  },
  computed: {
    notesFilter() {
      let array = this.notes,
          search = this.search
      if(!search) return array
      // Small
      search.trim().toLowerCase()
      // Filter
      array = array.filter((item) => {
        if(item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      // Error
      return array
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 800px;
}
</style>
