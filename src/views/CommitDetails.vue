<template>
	<v-container column v-if="commit && !loading" class="mainDiv">
		<v-card class="commitCard">
			<v-card-title class="gridDiv">
				<span class="gridItem">Commit</span>
				<strong class="gridItem">[{{ shaID }}]</strong>
			</v-card-title>
			<div>
				<div class="gridDiv">
					<strong class="gridItem">Date:</strong>
					<span class="gridItem">{{ new Date(commit.commit.author.date).toDateString() }}</span>
				</div>
				<div class="gridDiv">
					<strong class="gridItem">Author name:</strong>
					<span class="gridItem">{{ commit.commit.author.name }}</span> 
				</div>
				<div class="gridDiv">
					<strong class="gridItem">Author email:</strong>
					<span class="gridItem">{{ commit.commit.author.email }}</span> 
				</div>
				<div class="gridDiv">
					<strong class="gridItem">Commit message:</strong>
					<span class="gridItem">{{ commit.commit.message }}</span> 
				</div>
			</div>
		</v-card>
		<v-card-actions>
			<button color="error" @click="returnHome" class="backBtn">Back</button>
		</v-card-actions>
	</v-container>
	<v-container column v-else>
		<h3 v-if="errorMsg"> {{ errorMsg }} </h3>
	</v-container>
</template>

<script>
import axios from "axios";

export default {
	name: "CommitDetails",
	mounted() {
		axios.get('https://api.github.com/repos/vuejs/vue/commits/' + this.shaID)
			.then((response) => {
				console.log(response.data);
				this.commit = response.data;
				this.loading = false;
			})
			.catch((error) => {
				console.log(error);
			});
	},
	data() {
		return {
			shaID: this.$route.params.shaID,
			loading: true,
			commit: null,
			errorMsg: '',
		};
	},
	methods: {
		returnHome() {
			this.$router.replace({ name: "HomeView" });
		},
	},
};
</script>

<style scoped>
	.mainDiv {
		font-family: Arial, Helvetica, sans-serif;
	}
	.commitCard {
		margin-top: 50px;
		margin-top: 20px;
		background-color: lightskyblue;
	}
	.gridDiv {
		display: grid;
		grid-template-columns: 1fr 4fr;
		gap: 15px;
		padding: 10px;
	}
	.gridItem {
		text-align: center;
	}
	.backBtn {
		margin-left: auto;
		margin-right: auto;
		margin-top: 10px;
		padding: 8px 12px;
		border: 1px solid black;
		border-radius: 3px;
		background-color: lightskyblue;
	}
</style>