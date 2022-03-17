<template>
	<div class="mainDiv">
		<button @click="getCommits" class="loadBtn">Load commits</button>
		<h3 v-if="errorMsg" class="errMsg"> {{ errorMsg }} </h3>
		<v-card v-for="commit in commits" :key="commit.sha" :id="commit.sha" :details="commit.commit.message" class="listItem">
			<v-card-title class="gridEl">
				<span class="gridItem">Commit ID:</span>
				<span class="gridItem">{{ commit.sha }}</span>
			</v-card-title>
			<v-card-text class="gridEl">
				<span class="gridItem">Message / name:</span>
				<span class="gridItem">{{ commit.commit.message }}</span>
			</v-card-text>
			<v-card-actions>
				<router-link :to="{ name: 'CommitDetails', params: {shaID: commit.sha} }" class="btn">
					<button>More details</button>
				</router-link>
			</v-card-actions>
		</v-card>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: 'ListOfCommits',
	data() {
		return {
			commits: [],
			errorMsg: '',
		}
	},
	methods: {
		getCommits() {
			axios.get("https://api.github.com/repos/vuejs/vue/commits")
				.then((response) => {
					console.log(response.data)
					this.commits = response.data
				})
				.catch((error) => {
					console.log(error)
					this.errorMsg = "Error retrieving data"
				})
		}
	}
}
</script>

<style scoped>
	.mainDiv {
		font-family: Arial, Helvetica, sans-serif;
		padding-left: 10%;
		padding-right: 10%;
	}
	.loadBtn {
		margin: 0;
		position: absolute;
		left: 50%;
		transform: translateX(-50%);
		padding: 8px 12px;
		border: 1px solid black;
		border-radius: 3px;
		background-color: lightskyblue;
		color: black;
	}
	.errMsg {
		text-align: center;
		color: red;
		padding-top: 15px;
		padding-bottom: 20px;
	}
	.listItem {
		margin-top: 10px;
		margin-top: 10px;
		background-color: lightskyblue !important;
	}
	.gridEl {
		display: grid;
		grid-template-columns: 1fr 4fr;
		gap: 15px;
		padding: 10px;
	}
	.gridItem {
		text-align: center;
	}
	.detailsBtn {
		text-decoration: none;
	}
	.btn {
		margin-left: auto;
		margin-right: auto;
		padding: 8px 12px;
		border: 1px solid black;
		border-radius: 3px;
		background-color: blue;
		color: black;
	}
</style>
