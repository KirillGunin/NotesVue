<template>
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true, // обязательное параметр значения
    }
  }
}
</script>

<style lang="scss" scoped>
.message {
  color: #f52020;
  text-align: center;
  padding: 20px;
}
</style>
