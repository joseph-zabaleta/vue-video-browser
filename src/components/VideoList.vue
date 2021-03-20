<template>
	<ul>
		<VideoListItem
			:key="video.id.videoId"
			v-for="video in videos"
			:video="video"
		></VideoListItem>
	</ul>
</template>

<script>
import VideoListItem from './VideoListItem.vue';

export default {
	name: 'VideoList',
	props: {
		videos: Array,
	},
	components: {
		VideoListItem,
	},
};
</script>

<style></style>
