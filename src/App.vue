<template>
  <div id="app">
    <Loading :loading="loading"/>
    <SearchControl :onSearch="handleSearch"/>
    <NewsList :news="news"/>
  </div>
</template>

<script>
import SearchControl from './components/SearchControl';
import NewsList from './components/NewsList';
import Loading from './components/Loading';
import { getNews } from './services/api';

export default {
  data() {
    return {
      news: null,
      loading: false
    };
  },
  components: {
    NewsList,
    SearchControl,
    Loading
  },
  methods: {
    handleSearch(topic) {
      this.loading = true;

      getNews(topic).then(data => {
        this.news = data.articles;
        this.loading = false;
      });
    }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 30px;
  position: relative;
}
</style>