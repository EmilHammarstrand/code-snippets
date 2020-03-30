<template>
  <div id="app"> 
    <addSnippets />
    <voteSnippets />
  </div>
  
</template>

<script>
import addSnippets from "./components/addSnippets";
import voteSnippets from "./components/voteSnippets";

export default {

  name: 'App',
  components: {
    addSnippets,
    voteSnippets
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
