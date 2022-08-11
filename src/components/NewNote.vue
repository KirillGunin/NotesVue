<template>
  <!-- new note -->
    <div class="new-note">
      <label>Тема</label>
      <input v-model="note.title" type="text">
      <label>Описание</label>
      <textarea v-model="note.descr"></textarea>
      <button class="btn btnPrimary" @click="addNote">Добавить заметку</button>
    </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    }
  },
  methods: {
    addNote() {
      // с помощью this.$emit передадим пропсом данные обратно родителю
      this.$emit('addNote', this.note) // первый параметр это метод который отправляем
    }
  }
}
</script>

<style lang="scss">
.new-note {
  text-align: center;
}
</style>
