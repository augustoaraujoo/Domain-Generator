<template>
	<div>
		<div id="main">
			<div class="container">
				<div class="row">
					<div class="col-md">
					<AppItemList title="Prefixos" :items="prefixes" v-on:addItem="addprefixo" v-on:deleteItem="removePrefix"/>
					</div>
					<div class="col-md">
					<AppItemList title="Sufixos" :items="sufixes" v-on:addItem="addSufixo" v-on:deleteItem="removeSufix"/>
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
import AppItemList from "./AppItemList.vue";
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
		AppItemList
	},
	methods:{
		addprefixo(prefix){
			this.prefixes.push(prefix);
		},
		removePrefix(prefix){
			this.prefixes.splice(this.prefixes.indexOf(prefix),1);
		},
		addSufixo(sufix){
			this.sufixes.push(sufix);
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
</style>