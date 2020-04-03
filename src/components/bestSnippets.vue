<template>
<div class="root">
    <div class="formGroup">
        <button @click="getBestSnippets(); clicked=true" :disabled="clicked" >Best Snippets</button>
    </div>

    <div>
        <h2 class="code-snippets" v-if="modelBestSnippet">Best Snippets</h2>
    </div>

    <div class="snippetResult">
        <div class="list">
            <div v-for="(bestSnippet, i) in bestSnippetsList" class="bestSnippet" :key="`${i}-${bestSnippet.id}`">
                <div v-if="modelBestSnippet"> {{bestSnippet}} </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
const baseUrl = "https://www.forverkliga.se/JavaScript/api/api-snippets.php?";

export default {

  data: () => ({
      bestSnippetsList: [],
      modelBestSnippet: null, // title, content and id from api
      clicked: false 
  }),

  methods:{
      getBestSnippets(){
           this.$http.get(baseUrl, {  params: { best: '' }})
			.then(response => {
				console.log('getBestSnippets: ', typeof response.data, response.data);
				this.modelBestSnippet = {
                    title: response.data.title,
                    content: response.data.content,
                    score: response.data.score
                }
                response.data.some((bestSnippet, index) => {
                    this.bestSnippetsList.push(" Title:" + bestSnippet.title + " Content:" + bestSnippet.content + " Votes:" + bestSnippet.score)
                        return index >= 6
                })
			})
			.catch(error => {
				console.log('Something went wrong', error);
			});
        }
    }
}
</script>

<style>

</style>

  


