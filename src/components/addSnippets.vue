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
        <button :disabled="!isCompleted || !nameIsValid" @click=" addSnippetCode(); uploadSnippet(); ">Add snippet</button>
    </div>
</div>

<div class="code-snippets">
   <h2>Code Snippets</h2>
</div>
    <div class="snippetResult">
        
        <div class="list">
            <div v-for="snippet in addSnippet" :key="snippet">
                {{snippet}}
            </div>
        </div>

    </div>
</div>
</template>

<script>

export default {

    
    data: () => ({
        alias: "",
        code: "",
        addSnippet: [],
        nameIsTouched: false,
        codeIsTouched: false
        
    }),
    computed: {
        nameErrorMessage(){
            return "Please enter at least four characters."
        },
        nameIsValid() {
            return this.alias.length >= 4;
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
        addSnippetCode(){
            this.addSnippet.push(this.alias + this.code);
        },
        uploadSnippet() {
            this.$http.get("https://www.forverkliga.se/JavaScript/api/api-snippets.php?add", { params: {title: "", content: ""} })
            .then(response => {
                this.dataFromApi = response.data;
            })
            .catch(this.handleError);
        }
    },
    
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

</style>

