<template>
	<div>
		<div id="slogan" class="text-center">
			<h1>Generator</h1>
			<br/>
			<h6 class="text-secondary">Gerador de nomes utilizando Vue.js, GraphQL e Node</h6>
		</div>
		<div id="main">
			<div class="container">
				<div class="row">
					<div class="col-md">
						<h5>Prefixos <span class="badge badge-info">{{ prefixes.length }}</span></h5>
						<div class="card">
							<div class="card-body">
								<ul class="list-group">
									<li class="list-group-item" v-for="prefix in prefixes" :key="prefix">
										<div class="row">
											<div class="col-md">		
												{{ prefix }}
											</div>
										</div>
										<div class="col-md text-right">
											<button class="btn btn-info" @click="removePrefix(prefix)"><span class="fa fa-trash"></span></button>
										</div>
									</li>
								</ul>
								<br/>
								<div class="input-group">
									<input class="form-control" type="text" @keypress.enter="addprefixo(prefix)" v-model="prefix" placeholder="Digite o prefixo"/>
									<div class="input-group-append">
										<button class="btn btn-info" @click="addprefixo(prefix)"><span class="fa fa-plus"></span></button>
									</div>
								</div>
							</div>
						</div>
					</div>
					<div class="col-md">
						<h5>Sufixos <span class="badge badge-info">{{ sufixes.length }}</span></h5>
						<div class="card">
							<div class="card-body">
								<ul class="list-group">
									<li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
										<div class="row">
											<div class="col-md">
												{{ sufix }}
											</div>
										</div>
										<div class="col-md text-right">
											<button class="btn btn-info" @click="removeSufix(sufix)"><span class="fa fa-trash"></span></button>
										</div>
									</li>
								</ul>
								<br/>
								<div class="input-group">
									<input class="form-control" type="text" @keypress.enter="addSufixo(sufix)" v-model="sufix" placeholder="Digite o sufixo"/>
									<div class="input-group-append">
										<button class="btn btn-info" @click="addSufixo(sufix)"><span class="fa fa-plus"></span></button>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
				<br/>
				<h5>Domínios <span class="badge badge-info">{{ domains.length }}</span></h5>
				<div class="card">
					<div class="card-body">
						<ul class="list-group">
							<li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
								<div class="row">
									<div class="col-md">		
										{{domain.name}}
									</div>
									<div class="col-md text-end">
										<a class="btn btn-info" v-bind:href="domain.checkout" target="_blank">
											<span class="fa fa-shopping-cart"></span>
										</a>
									</div>
								</div>
							</li>
						</ul>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
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
	methods:{
		addprefixo(prefix){
			this.prefixes.push(prefix);
			this.prefix = "";
		},
		removePrefix(prefix){
			this.prefixes.splice(this.prefixes.indexOf(prefix),1);
		},
		addSufixo(sufix){
			this.sufixes.push(sufix);
			this.sufix = "";
		},
		removeSufix(sufix){
			this.sufixes.splice(this.sufixes.indexOf(sufix),1);
		},

	},
	computed:{
		domains(){
			const domains = [];
			for(const prefix of this.prefixes){
				for(const sufix of this.sufixes){
					const name = prefix + sufix;
					const url = name.toLowerCase();
					const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;
					domains.push({
						name,
						checkout,
					});
				}
			}
			return domains;
		}
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