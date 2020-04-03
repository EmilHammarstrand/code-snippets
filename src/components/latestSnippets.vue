<template>
<div class="root">
    <div class="formGroup">
        <button @click="getLatestSnippets(); clicked=true" :disabled="clicked" >Latest Snippets</button>
    </div>

    <div>
        <h2 class="code-snippets" v-if="modelLatestSnippet">Latest Snippets</h2>
    </div>

    <div class="snippetResult" >
        <div class="list" >
            <div v-for="(latestSnippet, i) in latestSnippetsList" class="latestSnippet" :key="`${i}-${latestSnippet.id}`">
                <div v-if="modelLatestSnippet"> {{latestSnippet}} </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
const baseUrl = "https://www.forverkliga.se/JavaScript/api/api-snippets.php?";

export default {
    
  data: () => ({
    modelLatestSnippet: null, // title and content from api
    latestSnippetsList: [],
    clicked: false
  }),

  methods:{
      getLatestSnippets() {
			this.$http.get(baseUrl, {  params:{ latest: '' }})
			.then(response => {
				console.log('getLatestSnippets: ', typeof response.data, response.data);
				this.modelLatestSnippet = {
                    title: response.data.title,
                    content: response.data.content,
                    uploaddt: response.data.upload_dt
                }
                response.data.some((snippet, index) => {
                    this.latestSnippetsList.unshift( "Title:" + snippet.title + " Content:" + snippet.content + " Date:" + snippet.upload_dt)
                        return index >= 6 })
			})
			.catch(error => {
				console.log('Something went wrong', error);
            })
        }},
  }
</script>

<style>

</style>

  
