<template>
  <div id="app">
    <UsrMsg /> 
    <addSnippets />
    <voteSnippets />
    <resultsSnipetts />
  </div>
  
</template>

<script>
import addSnippets from "./components/addSnippets";
import voteSnippets from "./components/voteSnippets";
import resultsSnipetts from "./components/resultsSnippets";
export default {

  name: 'App',
  components: {
    addSnippets,
    voteSnippets,
    resultsSnipetts
  },
}

</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
