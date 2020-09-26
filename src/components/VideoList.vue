

<template>
	<ul class='col-md-4 list-group'>
		<VideoListItem 
			v-for="video in videos"
			:key='video.etag' 
			:video='video'
			@videoSelect='onVideoSelect'
		></VideoListItem>
	</ul>
</template>


<script>
import VideoListItem from './VideoListItem'

export default {
	name:'VideoList',

	//register component
	components : {
		VideoListItem
	},

	//passed from parent
	props:['videos'],

	methods : {
		onVideoSelect(video) {
			//Emit event as videoSelect to parent
			this.$emit('videoSelect', video)
		}
	}
	
}
</script>


<style>
</style>