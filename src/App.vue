

<template>
	<div class='container'>
		<SearchBar @termChange='onTermChange'></SearchBar>
		<div class='row'>
			<VideoDetail :video='selectedVideo' />
			<VideoList :videos='videos' @videoSelect='onVideoSelect'></VideoList>
		</div>
	</div>
</template>


<script>
import axios from 'axios'
import SearchBar from './components/SearchBar'
import VideoList from './components/VideoList'
import VideoDetail from './components/VideoDetail'

const API_KEY = 'AIzaSyCFGQJ67k45URaTy5b8q3WiO9bKxkA5mOg'


//Props - Communicate from parent to child
//Emit Events - Communicate from child to parent

export default {
	name:'App',

	components: {
		SearchBar,
		VideoList,
		VideoDetail,
	},

	data: function() {
		return {
			videos:[],
			selectedVideo:null,
		}
	},

	methods:{
		onVideoSelect(video) {
			this.selectedVideo = video
		},

		onTermChange(searchTerm) {
			
			axios.get('https://www.googleapis.com/youtube/v3/search', {
				params: {
					key:API_KEY,
					type:'video',
					part:'snippet',
					q:searchTerm,
				}
			}).then(
				response => this.videos = response.data.items
			).catch(
				error => console.log(error)
			)
		},
	}
}
</script>


<style>
</style>


