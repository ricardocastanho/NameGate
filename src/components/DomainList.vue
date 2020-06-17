<template>
<div>
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
                      &nbsp;
                      <button class="btn btn-info" @click="openDomain(domain)">
                        <span class="fa fa-search"></span>
                      </button>
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
import AppItemList from "./AppItemList";
import axios from "axios/dist/axios"

export default {
  name: "App",
  components: {
    AppItemList
  },
	data() {
		return {
			prefixes: [],
			sufixes: []
		};
	},
  methods: {
    addPrefix(prefix){
      axios({
        url: "http://localhost:3333",
        method: "post",
        data: {
          query: `
            mutation ($data: inputItem!){
              saveItem(data: $data){
                id 
                type 
                description
              }
            }
          `,
          variables: {
            data: {
              type: "prefix",
              description: prefix
            }
          }
        }
      }).then(response => {
        this.prefixes.push(response.data.data.saveItem)
      })
    },
    addSufix(sufix){
      axios({
        url: "http://localhost:3333",
        method: "post",
        data: {
          query: `
            mutation ($data: inputItem!){
              saveItem(data: $data){
                id 
                type 
                description
              }
            }
          `,
          variables: {
            data: {
              type: "sufix",
              description: sufix
            }
          }
        }
      }).then(response => {
        this.sufixes.push(response.data.data.saveItem)
      })
    },
    deletePrefix(prefix){
      axios({
        url: "http://localhost:3333",
        method: "post",
        data: {
          query: `
            mutation ($data: idItem!){
              deleteItem(data: $data){
                id 
                type 
                description
              }
            }
          `,
          variables: {
            data: {
              id: prefix,
              type: "prefix"
            }
          }
        }
      }).then(response => {
        if(response.status == 200){
          this.getPrefixes()
        }
      })
    },
    deleteSufix(sufix){
      axios({
        url: "http://localhost:3333",
        method: "post",
        data: {
          query: `
            mutation ($data: idItem!){
              deleteItem(data: $data){
                id 
                type 
                description
              }
            }
          `,
          variables: {
            data: {
              id: sufix,
              type: "sufix"
            }
          }
        }
      }).then(response => {
        if(response.status == 200){
          this.getSufixes()
        }
      })
    },
    getPrefixes(){
      axios({
        url: "http://localhost:3333",
        method: "post",
        data: {
          query: `
            {
              prefixes{
                id type description
              }
            }
          `
        }
      }).then(response => {
        const query = response.data
        this.prefixes = query.data.prefixes
      })
    },
    getSufixes(){
      axios({
        url: "http://localhost:3333",
        method: "post",
        data: {
          query: `
            {
              sufixes{
                id type description
              }
            }
          `
        }
      }).then(response => {
        const query = response.data
        this.sufixes = query.data.sufixes
      })
    },openDomain(domain){
      this.$router.push({
        path: `/domains/${domain}`
      })
    }

  },
  computed: {
    domains(){
      const domains = []
      for( const prefix of this.prefixes ){
        for( const sufix of this.sufixes ){
          domains.push(prefix.description + sufix.description)
        }
      }
      return domains
    },
  },
  created(){
    this.getPrefixes()
    this.getSufixes()
  }
};
</script>

<style>
</style>
