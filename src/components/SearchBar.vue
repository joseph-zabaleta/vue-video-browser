<template>
	<div class="mb-3">
		<label class="form-label ">Search for A Video</label>
		<input class="form-control " @input="onInput" />
	</div>
</template>

<script>
export default {
	name: 'SearchBar',
	methods: {
		onInput: function(e) {
			this.$emit('termChange', e.target.value);
		},
	},
};
</script>

<style scoped>
input {
	width: 100%;
}

div {
	text-align: left;
	margin: 20px;
	padding: 15px;
	border: 1px solid #ddd;
}

label {
	font-weight: 500;
}
</style>
