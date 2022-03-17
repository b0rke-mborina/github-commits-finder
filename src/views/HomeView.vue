<template>
	<div class="homePage">
		<h1 class="pageTitle">Find a list of commits of a Vue.js Github repository</h1>
		<list-of-commits />
	</div>
</template>

<script>
import ListOfCommits from '../components/ListOfCommits.vue'

export default {
	name: 'HomeView',
	components: {
		ListOfCommits,
	},
}
</script>

<style scoped>
	.homePage {
		font-family: Arial, Helvetica, sans-serif;
	}
	.pageTitle {
		text-align: center;
		font-weight: bold;
		padding-top: 50px !important;
		padding-bottom: 30px !important;
	}
</style>