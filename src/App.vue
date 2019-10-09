<template>
  <div id="app">
    <Header />
    <SearchForm @search="search"/>
    <SearchResults
      v-if="videos.length > 0"
      :videos="videos"
      :reformatedSearchString="reformatedSearchString"
    />
    <Pagination
      v-if="videos.length > 0"
      :prevPageToken="api.prevPageToken"
      :nextPageToken="api.nextPageToken"
      @prev-page="prevPage"
      @next-page="nextPage"
    />
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import SearchForm from './components/SearchForm.vue';
import SearchResults from './components/SearchResults.vue';
import Pagination from './components/Pagination.vue';
import youtubeKey from './api.config.js'

export default {

  name: 'App',
  components: {
    Header,
    SearchForm,
    SearchResults,
    Pagination,
  },
  data () {
    return {
      videos: [],
      reformatedSearchString: '',
      api: {
        baseUrl: 'https://www.googleapis.com/youtube/v3/search?',
        type: 'video',
        part: 'snippet',
        order: 'viewCount',
        maxResults: 12,
        q: '',
        key: youtubeKey,
        prevPageToken: '',
        nextPageToken: '',
      }
    }
  },
  methods: {
    search (searchParams) {
      this.reformatedSearchString = searchParams.join(' ')
      this.api.q = searchParams.join('+')
      const { baseUrl, type, part, order, maxResults, q, key } = this.api
      const apiUrl = `${baseUrl}part=${part}&type=${type}&order=${order}&maxResults=${maxResults}&key=${key}&q=${q}`
      this.getData(apiUrl)
    },
    prevPage () {
      const { baseUrl, type, part, order, maxResults, q, key, prevPageToken } = this.api
      const apiUrl = `${baseUrl}part=${part}&type=${type}&order=${order}&maxResults=${maxResults}&key=${key}&q=${q}&prevPageToken=${prevPageToken}`
      this.getData(apiUrl)
    },
    nextPage () {
      const { baseUrl, type, part, order, maxResults, q, key, nextPageToken } = this.api
      const apiUrl = `${baseUrl}part=${part}&type=${type}&order=${order}&maxResults=${maxResults}&key=${key}&q=${q}&nextPageToken=${nextPageToken}`
      this.getData(apiUrl)
    },
    getData (apiUrl) {
      axios
        .get(apiUrl)
        .then(res => {
          this.videos = res.data.items
          this.api.prevPageToken = res.data.prevPageToken
          this.api.nextPageToken = res.data.nextPageToken
        })
        .catch(error => console.error(error))
    },
  }
}
</script>

<style scoped>
</style>