<template>
	<div class="container">
		<nav>
			<ul class="pagination justify-content-end">
				<li class="page-item"
					:class="{ disabled: prevPageToken === undefined }"
				>
					<a href="#" class="page-link" @click="prevPage">Previous</a>
				</li>
				<li class="page-item"
					:class="{ disabled: nextPageToken === undefined }"
				>
					<a href="#" class="page-link" @click="nextPage">Next</a>
				</li>
			</ul>
		</nav>
	</div>
</template>

<script>
export default {

  name: 'Pagination',
  props: [ 'prevPageToken', 'nextPageToken'],
  data () {
    return {

    }
  },
  methods: {
    nextPage () {
      this.$emit('next-page')
    },
    prevPage () {
      this.$emit('prev-page')
    }
  }
}
</script>

<style scoped>
</style>