<template>
</template>

<script>
export default {

  name: 'App',
  components: {},
  data () {
    return {
      videos: [],
      reformatedSearchString: '',
      api: {
        baseUrl: 'https://www.googleapis.com/youtube/v3/search?',
        type: 'video',
        part: 'snippet',
        order: 'videoCount',
        maxResults: 12,
        q: '',
        key: YOUTUBE_API_KEY
        prevPageToken: '',
        nextPageToken: '',
      }
    }
  },
  methods: {
    search (searchParams) {
      this.reformatedSearchString = searchParams.join(' ')
      this.api.q = this.searchParams.join('+')
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