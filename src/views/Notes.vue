<template>
  <div>
    <div class="sidebar">
      <div>
        <div class="add-note" @click="addNote">
          +
        </div>
        <div class="note" v-for="note, index in notes" @click="selectNote(note)">
          <p class="title">{{note.title}}</p>
          <p class="desc">{{note.desc}}</p>
          <span class="delete" @click="deleteNote(note, index)">Удалить</span>
          <span class="date">{{note.date}}</span>
        </div>
      </div>
    </div>
    <div class="main">
      <div v-if="editNote">
        <h1>{{editNote.title}}</h1>
        <input v-model="editNote.title"/>
        <textarea v-model="editNote.desc"></textarea>
        <textarea rows="30" v-model="editNote.body"></textarea>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    deleteNote (note, index) {
      if (confirm('Вы действительно хотите удалить заметку?')) {
        this.notes.splice(index, 1)
      }
    },
    addNote () {
      let note = {
        title: 'Новая заметка',
        desc: 'Описание',
        body: '',
        date: (new Date).toLocaleString()
      }

      this.notes.unshift(note)
    },
    selectNote (note) {
      this.editNote = note
    }
  },
  data() {
    return {
      editNote: null,
      notes: [
        { title: 'Моя заметка', desc: 'Описание', body: 'Текст', date: (new Date).toLocaleString() },
        { title: 'Моя заметка 2', desc: 'Описание 2', body: 'Текст 2', date: (new Date).toLocaleString() }
      ]
    }
  }
}
</script>
