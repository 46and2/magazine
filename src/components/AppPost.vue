<template>
  <article class="post">
    <h2 class="post__title">{{ post.title }}</h2>
    <p class="post__body">{{ post.body }}</p>
    <cite class="post__author">{{ post.author.name }}</cite>
  </article>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
.post {
  margin-left: 10px;
  margin-bottom: 10px;
  padding: 15px;
  flex-basis: 100%;
  background-color: #ffffff;
  border: 1px solid #d3dce8;
  border-radius: 4px;
  font-family: Arial, Helvetica, sans-serif;
}

.post__title {
  font-size: 18px;
  color: #116fdd;
  margin: 0;
}

.post__title::first-letter {
  text-transform: capitalize;
}

.post__body::first-letter {
  text-transform: capitalize;
}

.post__author {
  font-style: normal;
  font-size: 12px;
  color: #8c949a;
}

@media (min-width: 580px) {
  .post {
    flex-basis: calc((100% - 20px) / 2);
  }
}

@media (min-width: 820px) {
  .post {
    flex-basis: calc((100% - 30px) / 3);
  }
}
</style>
