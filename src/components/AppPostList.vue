<template>
  <section class="posts">
    <app-filter
      @filter="filterByAuthor"
      hint="Filter by author..."
      class="posts__filter"
    ></app-filter>
    <div class="posts__wrapper">
      <div class="posts__list">
        <app-post
          v-for="post in filteredPosts"
          :key="post.id"
          :post="post"
        ></app-post>
      </div>
    </div>
    <div v-if="error" class="error">
      <span class="error__message">Couldn't fetch any data...</span>
    </div>
  </section>
</template>

<script>
import AppPost from './AppPost.vue';
import AppFilter from './AppFilter.vue';

export default {
  name: 'AppPostList',
  components: { AppPost, AppFilter },
  data() {
    return {
      posts: [],
      users: [],
      authorFilter: '',
      error: false
    };
  },
  computed: {
    filteredPosts() {
      return this.posts.filter(
        post =>
          post.author.name
            .toLowerCase()
            .indexOf(this.authorFilter.trim().toLowerCase()) !== -1
      );
    }
  },
  created() {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(json => {
        this.users = json;
        return fetch('https://jsonplaceholder.typicode.com/posts')
          .then(response => response.json())
          .then(json => {
            this.posts = json.map(post => ({
              ...post,
              author: this.users.find(user => user.id === post.userId)
            }));
          });
      })
      .catch(err => {
        this.error = true;
        console.error("Couldn't fetch any data: ", err);
      });
  },
  methods: {
    filterByAuthor(searchTerm) {
      this.authorFilter = searchTerm;
    }
  }
};
</script>

<style>
.posts__filter {
  margin: 25px 0;
}

.posts__wrapper {
  margin-left: -10px;
}

.posts__list {
  display: flex;
  flex-wrap: wrap;
}

.error {
  text-align: center;
}

.error__message {
  font-size: 20px;
  font-weight: 300;
}
</style>
