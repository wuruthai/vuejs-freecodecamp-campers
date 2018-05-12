<template lang="html">
<tbody>

  <tr v-for="(camper, index) in campers">
    <td >{{index+1}}</td>
    <td ><img  :src="camper.img  " :alt=" `${camper.username} image` " ><p>{{camper.username}}</p> </td>
    <td >{{camper.recent}}</td>
    <td >{{camper.alltime}}</td>
  </tr>
</tbody>
</template>

<script>
export default {
	props: ["campers"],

}
</script>

<style lang="css">
tr {

}

td:first-child{
  text-align: center;
}


img {
  width: 50px;
  float: left;
  margin: 5px;
  margin-right: 10px;
}

</style>
