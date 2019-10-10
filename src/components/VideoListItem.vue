<template>
	<div>
		<div class="card-body">
			<h5 class="card-title">
				<a
					target="_blank"
					class="card-link"
					:href="`https://youtube.com/watch?v=${video.id.videoId}`">{{ video.snippet.title }}</a>
			</h5>
			<h6 class="card-subtitle mb-2 text-muted">
				{{ video.snippet.channelTitle }} | {{ video.snippet.publishedAt | formatDate }}
			</h6>
			<p class="card-text">
				{{ video.snippet.description }}
			</p>
		</div>
	</div>
</template>

<script>
export default {

  name: 'VideoListItem',
  props: [ 'video'],
  data () {
    return {

    }
  }
}
</script>