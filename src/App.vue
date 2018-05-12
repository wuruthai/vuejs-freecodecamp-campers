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
			<th>{{th3}}</th>
			<th>{{th4}}</th>
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
			campers: []
		}
	},
	methods: {

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
#app {}

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
