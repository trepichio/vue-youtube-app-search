<template>
	<div class="container mb-3">
		<div class="d-flex mb-3">
			<div class="mr-auto">
				<h3>Search Results for "{{ reformatedSearchString }}"</h3>
			</div>
			<div class="button-group ml-auto" role="group">
				<button
					type="button"
					@click="changeDisplayMode('grid')"
					class="btn btn-outline-secondary"
					:class="{ active: displayMode === 'grid' }"
				>
					<i class="fas fa-th"></i>
				</button>
				<button
					type="button"
					@click="changeDisplayMode('list')"
					class="btn btn-outline-secondary"
					:class="{ active: displayMode === 'list' }"
				>
					<i class="fas fa-list"></i>
				</button>

			</div>
		</div>

		<div class="card-columns" v-if="displayMode === 'grid'">
			<div
				v-for="video in videos"
				:key="video.id.videoId"
				class="card"
			>
				<VideoGridItem :video="video" />
			</div>
		</div>
		<div v-else>
			<div
				v-for="video in videos"
				:key="video.id.videoId"
				class="card mb-2"
			>
				<VideoListItem :video="video" />
			</div>
		</div>
	</div>
</template>

<script>
import VideoListItem from './VideoListItem.vue';
import VideoGridItem from './VideoGridItem.vue';

export default {

  name: 'SearchResults',
  props: [ 'videos', 'reformatedSearchString' ],
  components: {
  	VideoListItem,
  	VideoGridItem
  },
  data () {
    return {
    	title: 'Search Results',
    	displayMode: 'grid'
    }
  },
  methods: {
    changeDisplayMode (displayMode) {
      this.displayMode = displayMode
    }
  }
}
</script>

<style scoped>
	button:focus {
		box-shadow: none !important
	}
</style>