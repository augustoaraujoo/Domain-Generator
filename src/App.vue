<template>
	<div>
		<div id="slogan" class="text-center">
			<h1>Generator</h1>
			<br/>
			<h6 class="text-secondary">Gerador de nomes utilizando Vue.js, GraphQL e Node</h6>
		</div>
		<div id="main">
		<DomainList/>
		</div>
	</div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import DomainList from "./components/DomainList.vue";
export default {
	name: "app",
	data:function(){
		return {	
			sufix:"",
			prefix:"",
			prefixes: ["Air", "Jet", "Flight"],
			sufixes:  ["Hub", "Station", "Mart"]
		};
	},
	components:{
		DomainList
	}
};
</script>

<style>
.badge-info{
	background-color: #0077ff;
}
#slogan {
	margin: 30px;
}
#main {
	background-color: 
	#F1F1F1;padding:30px;
}
</style>