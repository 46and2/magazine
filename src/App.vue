<template>
  <div id="app">
    <div class="container">
      <app-post-list></app-post-list>
    </div>
  </div>
</template>

<script>
import AppPostList from './components/AppPostList.vue';

export default {
  name: 'App',
  components: { AppPostList }
};
</script>

<style>
.container {
  max-width: 960px;
  margin: 0 auto;
  padding: 0 10px;
}
</style>
