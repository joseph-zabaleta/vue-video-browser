<template>
	<div>
		<SearchBar @termChange="onTermChange"></SearchBar>
		<VideoList :videos="videos"></VideoList>
	</div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';

export default {
	name: 'App',
	data() {
		return {
			term: '',
			key: process.env.VUE_APP_API_KEY,
			videos: [],
		};
	},
	components: {
		SearchBar,
		VideoList,
	},
	methods: {
		onTermChange(term) {
			this.term = term;

			axios
				.get('https://www.googleapis.com/youtube/v3/search', {
					params: {
						key: this.key,
						type: 'video',
						part: 'snippet',
						q: this.term,
					},
				})
				.then((response) => (this.videos = response.data.items));
		},
	},
};
</script>
