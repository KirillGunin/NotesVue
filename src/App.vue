<template>
  <div class="wrapper">
    <div class="wrapper-content">

      <section>
        <div class="container">
          
          <!-- :message="message" передадим пропсом в дочерний класс и значение будет приходить из data-->
          <message v-if="message" :message="message"/>

          <!-- new note -->
          <newNote :note="note" @addNote="addNote" style="margin: 36px 0"/>
          
          <div class="note-header">
            <h1>{{title}}</h1>

            <!-- Search -->
            <search :value="search" placeholder="Поиск" @search="search = $event"/>

            <!-- icons -->
            <div class="icons">
              <!-- по клику будет меняться состояние с true на false и за счет стилей active будет меняться цвет -->
              <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>

          <!-- note list -->
          <notes
          :notes="notesFilter"
          :grid="grid"
          @remove="removeNote"/>

        </div>
      </section>
    </div>

  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'
export default {
  components: {
    message, newNote, notes, search
  },
  data() {
    return {
      title: 'Notes App',
      search: '',
      message: null,
      grid: true,
      note: {
        title: '',
        descr: ''
      },
      notes: [
        {
          title: 'First note',
          descr: 'Description for first note',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Second note',
          descr: 'Description for second note',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Third note',
          descr: 'Description for third note',
          date: new Date(Date.now()).toLocaleString()
        }
      ]
    }
  },
  computed: {
    notesFilter() {
      let array = this.notes,
      search = this.search
      if(!search) return array // если поиск пустой, то вернет полный массив
      search = search.trim().toLowerCase()
      array = array.filter(function(item) {
        if(item.title.toLowerCase().indexOf(search) !== -1) { // если такой элемент существует, то мы его вернем
          return item
        }
      })
      // error
      return array
    }
  },
  methods: {
        addNote() {
          // console.log(this.note)
          const { title, descr } = this.note
          if (title === '') {
            this.message = 'Заметка не может быть пустой'
            return false
          }
          this.notes.push({
            title,
            descr,
            date: new Date(Date.now()).toLocaleString()
          })
          this.note.title = ''
          this.note.descr = ''
          this.message = null
        },
        removeNote(index) {
          this.notes.splice(index, 1)
        }
      }
}
</script>

<style> 
</style>
