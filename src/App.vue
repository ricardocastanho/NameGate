<template>
<div>
  <div id="slogam" class="text-center">
    <h1 class="text-center">NameGator</h1>
  </div>
  <div id="main">
    <DomainList></DomainList>
  </div>
</div>
</template>

<script>
import "font-awesome/css/font-awesome.css";
import DomainList from "./components/DomainList";

export default {
  name: "App",
  components: {
    DomainList
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
