<template>
	<div class="container">
		<SearchBar @termChange="onTermChange"></SearchBar>
		<div class="row">
			<VideoDetail :video="current"></VideoDetail>
			<VideoList
				:videos="videos"
				@videoSelect="onVideoSelect"
			></VideoList>
		</div>
	</div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';
import VideoDetail from './components/VideoDetail.vue';

export default {
	name: 'App',
	data() {
		return {
			term: '',
			key: process.env.VUE_APP_API_KEY,
			videos: [],
			current: null,
		};
	},
	components: {
		SearchBar,
		VideoList,
		VideoDetail,
	},
	created() {
		this.onTermChange('cheese');
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
				.then((response) => {
					this.videos = response.data.items;

					if (this.current === null) {
						this.current = this.videos[0];
					}
				});
		},
		onVideoSelect(video) {
			this.current = video;
		},
	},
};
</script>
