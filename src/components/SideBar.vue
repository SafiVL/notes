<template>
  <div>
    <div class="note" v-for="note in notes">
      <p class="title">{{note.title}}</p>
      <p class="desc">{{note.desc}}</p>
      <span class="date">{{note.date}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ['notes']
}
</script>
