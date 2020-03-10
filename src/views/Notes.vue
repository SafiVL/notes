<template>
  <div>
    <div class="sidebar">
      <side-bar :notes="notes"/>
    </div>
    <div class="main">
      <h1>Главная</h1>
    </div>
  </div>
</template>

<script>
import SideBar from '@/components/SideBar'

export default {
  components: {
    SideBar
  },
  data () {
    return {
      notes: [
        { title: 'Моя заметка', desc: 'Описание', body: 'Мой текст', date: (new Date).toLocaleString()  },
         { title: 'Моя заметка 2', desc: 'Описание 2', body: 'Мой текст 2', date: (new Date).toLocaleString()  }
      ]
    }
  }
}
</script>
