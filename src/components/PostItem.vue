<template>
  <div class="post">
    <div class="post__data">
      <div>
        <strong>Название:</strong>
        {{post.title}}
      </div>
      <div>
        <strong>Описание:</strong>
        {{post.body}}
      </div>
    </div>
    <div class="post__buttons">
      <my-button
        @click="$emit('remove', post)"
      >
        Удалить
      </my-button>
    </div>

  </div>
</template>

<script>

export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
  .post {
    width: 100%;
    max-width: 450px;
    height: fit-content;
    min-height: 100px;
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;
    justify-content: space-between;
  }

  .post__buttons {
    display: flex;
    align-self: flex-end;
  }
</style>
