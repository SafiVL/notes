<template>
  <div>
    <!-- Это у нас левая часть -->
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
    <!-- Это у нас правая часть -->
    <div class="main">
      <div v-if="editNote">
        <label>Название</label>
        <input v-model="editNote.title"/>
        <label>Описание</label>
        <textarea v-model="editNote.desc"></textarea>
        <textarea rows="30" v-model="editNote.body"></textarea>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: { // Функции что-бы потом вызывать
    save () { // Сохраняет заметки в хранилище браузера
      localStorage.setItem('notes', JSON.stringify(this.notes))
    },
    deleteNote (note, index) { // Удаляет заметку из списка
      if (confirm('Вы действительно хотите удалить заметку?')) {
        this.notes.splice(index, 1)
      }
    },
    addNote () { // Добавляет заметку в список
      let note = {
        title: 'Новая заметка',
        desc: 'Описание',
        body: '',
        date: (new Date).toLocaleString()
      }

      this.notes.unshift(note)
    },
    selectNote (note) { // Выбирает заметку для редактирования
      this.editNote = note
    }
  },
  watch: { // Надзиратель, смотрит за переменными и выполянет код если что-то в ней изменилось
    notes: {
      handler: function () {
        this.save()
      },
      deep: true
    }
  },
  mounted () { // При загрузке страницы
    this.notes = JSON.parse(localStorage.getItem('notes')) || []
  },
  data () { // Дефолтные изначальные переменные
    return {
      editNote: null,
      notes: []
    }
  }
}
</script>
