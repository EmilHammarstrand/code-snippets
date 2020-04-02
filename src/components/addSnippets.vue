<template>
<div class="root">
    <div class="wholeForm">
        <div class="formGroup">
            <label>Alias</label>
                <input type="text" v-model="alias" :class="nameClass" @blur.once="nameIsTouched = true" >
            <span v-if="nameIsTouched && !nameIsValid" class="error"> {{ nameErrorMessage }} </span>
        </div>

        <div class="formGroup">
        <label>Your code snippet</label>
            <textarea  class="codeInput" type="text" v-model="code" :class="codeClass" @blur.once="codeIsTouched = true"></textarea>
            <span v-if="!codeIsValid && codeIsTouched" class="error"> {{ codeErrorMessage }} </span>
        </div>

        <div class="formGroup">
            <button :disabled="!isCompleted || !nameIsValid" @click="uploadSnippet(); show = true">Add snippet</button>
        </div>
    </div>

    <div class="code-snippets">
        <h2 v-show="show">Your Snippets</h2>
    </div>
        <div class="snippetResult">
            <div class="list">
                <div class="snippet" v-for="(snippet, i) in addSnippetList" :key="`${i}-${snippet.id}`">
                   <div class="snippetText"> {{snippet}} </div>
                <button class="deleteButton" @click="deleteSnippet(snippet)">Delete</button>
                </div>
            </div>
        </div>
</div>
</template>

<script>
const baseUrl = "https://www.forverkliga.se/JavaScript/api/api-snippets.php?";

export default {

    data: () => ({
        alias: "",
        code: "",
        addSnippetList: [],
        nameIsTouched: false,
        codeIsTouched: false,
        show: false
    }),

    computed: {
        nameErrorMessage(){
            return "Please enter at least three characters."
        },
        nameIsValid() {
            return this.alias.length >= 3;
        },
        nameClass() {
			if( !this.nameIsTouched ) return '';
			return this.nameIsValid ? 'valid' : 'invalid';
        },
        isCompleted(){
            return this.alias && this.code && this.codeIsValid;
        },
        codeIsValid(){
            return this.code.length >= 10;
        },
        codeErrorMessage(){
            return "Please enter at least 10 characters."
        },
        codeClass(){
            if(!this.codeIsTouched) return "";
            return this.codeIsValid ? "valid" : "invalid";
        }
    },

    methods: {
        uploadSnippet() {
            this.$http.post(baseUrl, { add: '',  title: this.alias, content: this.code})
            .then(response => {
                console.log("axiosData:", response.data);
                this.addSnippetList.unshift( "Title:" + this.alias + " " + "Code: " + this.code);
            })
            .catch( error => {
                console.log("Error.", error)
            })
        },

        deleteSnippet(addSnippet){
            this.$http.post(baseUrl, {delete: '', id: this.alias+this.code})
            .then(response => {
                console.log("axiosData:", response.data);
                this.addSnippetList = this.addSnippetList.filter(
                snippet => snippet != addSnippet
            );
            })
            .catch( error => {
                console.log("Error.", error)
            })       
        }
    }
}
</script>

<style>
    .root{
        padding: 1em;
        margin: 1em;
        
    }

    .list {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: 1fr;
        justify-items: center;
    }

    .list > div{
        border: 1px solid black;
        width: 10em;
        height: 10em;
        margin: 1em;
    }

    .formGroup{
        margin: 0.3em;
        padding: 0.3em;
        display: block;
    }

    .error {
        color: red;
        display: block;
    }
    
    .formGroup label {
        display: block;
    }
    input.valid { border-color: green; }
    input.invalid { border-color: red; }

    textarea.valid { border-color: green; }
    textarea.invalid { border-color: red; }

    .code-snippets {
        text-align: center;
    }

    .code-snippets > h1 {
        display: inline-block;
    }

    .deleteButton{
        justify-content: flex-end;
    }

    .snippet {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

</style>

