<template>
<div>
  <div id="slogam" class="text-center">
    <h1 class="text-center">NameGator</h1>
  </div>
  <div id="main">
    <div class="container">
      <div class="row">
        <div class="col-md">
          <AppItemList title="Prefixo" v-bind:items="prefixes" v-on:addItem="addPrefix" v-on:deleteItem="deletePrefix"></AppItemList> 
        </div>
        <div class="col-md">
          <AppItemList title="Sufixo" v-bind:items="sufixes" v-on:addItem="addSufix" v-on:deleteItem="deleteSufix"></AppItemList> 
        </div>
      </div>
      <br>
      <h5>Domínios <span class="badge badge-info">{{ domains.length }}</span></h5>
          <div class="card">
            <div class="card-body">
              <ul class="list-group">
                <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">
                  <div class="row">
                    <div class="col-md">
                      {{ domain }}
                    </div>
                    <div class="col text-right">
                      <a class="btn btn-info" href="http://google.com.br" target="_blank">
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
import "font-awesome/css/font-awesome.css";
import AppItemList from "./components/AppItemList";

export default {
  name: "App",
  components: {
    AppItemList
  },
	data() {
		return {
			prefixes: ["Air", "Jet", "Fligth"],
			sufixes: ["Hub", "Station", "Mart"]
		};
	},
  methods: {
    addPrefix(prefix){
      this.prefixes.push(prefix)
    },
    addSufix(sufix){
      this.sufixes.push(sufix)
    },
    deletePrefix(prefix){
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1)
    },
    deleteSufix(sufix){
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1)
    }
  },
  computed: {
    domains(){
      const domains = []
      for( const prefix of this.prefixes ){
        for( const sufix of this.sufixes ){
          domains.push(prefix + sufix)
        }
      }
      return domains
    },
  }
};
</script>

<style>
#main{
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
#slogam{
  margin-top: 30px;
  margin-bottom: 30px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
