<template>
  <div class="message" v-if="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true
    }
  },
  name: "Message"
}
</script>

<style lang="scss" scoped>
  .message {
    text-align: center;
    padding: 20px;
    color: red;
  }
</style>