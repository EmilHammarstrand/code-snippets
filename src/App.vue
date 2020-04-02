<template>
  <div id="app"> 
    <addSnippets />
    <latestSnippets />
    <bestSnippets />
  </div>
  
</template>

<script>
import addSnippets from "./components/addSnippets";
import latestSnippets from "./components/latestSnippets";
import bestSnippets from "./components/bestSnippets";

export default {

  name: 'App',
  components: {
    addSnippets,
    latestSnippets,
    bestSnippets
  }
}

</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
