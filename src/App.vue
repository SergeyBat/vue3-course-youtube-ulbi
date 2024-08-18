<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="app__buttons">
      <my-button
        @click="showDialog"
      >
        Создать пост
      </my-button>
      <my-select
        v-model="selectedSort"
        :modelValue="selectedSort"
        :options="sortOptions"
      />
    </div>
    <my-dialog
      v-model:show="dialogVisible"
    >
      <post-form
        @create="createPost"
      />
    </my-dialog>
    <post-list
      :posts="posts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div
      v-else
    >
      Идет загрузка...
    </div>
  </div>
</template>


<script>
  import PostForm from "@/components/PostForm.vue";
  import PostList from "@/components/PostList.vue";
  import MyDialog from "@/components/UI/MyDialog.vue";
  import MyButton from "@/components/UI/MyButton.vue";
  import axios from "axios";
  import MySelect from "@/components/UI/MySelect.vue";
  export default {
    components: {
      MySelect,
      MyButton,
      MyDialog,
      PostForm,
      PostList
    },
    data () {
      return {
        posts: [
          {id: 1, title: 'Пост о JvaScript', body: 'JvaScript универсальный язык программирования'},
          {id: 2, title: 'Пост о JvaScript 2', body: 'JvaScript универсальный язык программирования 2'},
          {id: 3, title: 'Пост о JvaScript 3', body: 'JvaScript универсальный язык программирования 3'},
        ],
        dialogVisible: false,
        isPostsLoading: false,
        selectedSort: '',
        sortOptions: [
          {value: 'title', name: 'По названию'},
          {value: 'body', name: 'По содержимому'}
        ]
      }
    },
    methods: {
      createPost(post) {
        this.posts.push(post)
        this.dialogVisible = false;
      },
      removePost(post) {
        this.posts = this.posts.filter(item => item.id !== post.id)
      },
      showDialog() {
        this.dialogVisible = true;
      },
      async fetchPosts() {
        try {
          const {data: response} = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          this.posts = response
          console.log("=>(App.vue:82) response", response);
          this.isPostsLoading = false
        } catch (e) {
          alert('Ошибка')
        }
      },
    },
    mounted() {
      this.fetchPosts()
    }
  }
</script>


<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .app {
    padding: 20px;
  }

  form {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }

  .app__buttons {
    display: flex;
    justify-content: space-between;
  }
</style>
