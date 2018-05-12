<template>
<div id="app">
	<header>
		<img v-bind:src="logoUrl" alt="">
		<h1>{{header}}</h1>
	</header>

	<table border="1">
		<tr>
			<th>{{th1}}</th>
			<th>{{th2}}</th>
			<th v-on:click="sortCampers(recent)">{{th3}}&dArr;

			</th>
			<th v-on:click="sortCampers(alltime)">{{th4}} &dArr;</th>
		</tr>
		<camperlist :campers="campers"></camperlist>
	</table>

</div>
</template>

<script>
import camperlist from "./components/camperlist";

export default {
	name: 'app',
	components: {
		camperlist
	},
	data() {
		return {
			logoUrl: 'https://d33wubrfki0l68.cloudfront.net/cce87b74a290f321f582cb56a12007343ff2d77e/bb9e6/img/glyph.png',
			header: 'FreeCodeCamp Camper List',
			th1: '#',
			th2: 'Camper Name',
			th3: 'Last 30 Days',
			th4: 'Alltime',
			campers: [],
			alltime: "alltime",
			recent: "recent",
			recentStatus: true,
			allTimeStatus: false,
		}
	},
	methods: {

		sortCampers(col) {
			let campers = this.campers;
			let allTimeStatus = this.allTimeStatus;
			let recentStatus = this.recentStatus;

			if (col === "alltime") {
				campers.sort((a, b) => {

					if (allTimeStatus === true) {
						return b.alltime - a.alltime;
					} else {
						return a.alltime - b.alltime;
					}
				});
				this.allTimeStatus = !allTimeStatus;
			}


			if (col === "recent") {
				campers.sort((a, b) => {

					if (recentStatus === true) {
						return b.recent - a.recent;
					} else {
						return a.recent - b.recent;
					}
				});
				this.recentStatus = !recentStatus;
			}



			this.campers = campers;
		}
	},

	created() {
		fetch("https://fcctop100.herokuapp.com/api/fccusers/top/recent")
			.then((res) => {
				return res.json();
			})
			.then((res) => {
				this.campers = res;
				console.log(this.campers)
			})
	}


}
</script>

<style>
header {
	display: block;
	background-color: green;
	padding: 20px;
}

header img {
	float: left;
	width: 100px;
}

header h1 {
	color: white;
	margin-left: 115px;
}


table,
tr {
	width: 100%;

}

th {
	width: 32%;
}

th:first-child {
	width: 4%;
}
</style>
