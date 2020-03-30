<template>
<div class="root">

    <div class="formGroup">
        <label>Alias</label>
        <input type="text" v-model="alias" :class="nameClass" @blur.once="nameIsTouched = true" >
        <span v-if="nameIsTouched && !nameIsValid" class="error"> {{ nameErrorMessage }} </span>
    </div>
    
    <div class="formGroup">
        <label>Your code snippet</label>
        <textarea  class="codeInput" type="text" v-model="code"></textarea>
    </div>

    <div class="button">
        <button :disabled="!isCompleted || !nameIsValid" @click=" addSnippetCode(); ">Add snippet</button>
    </div>
    
<label>Code-snippets</label>
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
        nameIsTouched: false
        
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
            return this.alias && this.code;
        },
        
    },
    methods: {
        addSnippetCode(){
            this.addSnippet.push(this.alias, this.code);
        },
    },
    
}

</script>

<style>

    .list{
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr;
    }

    .formGroup{
        border: 1px solid black;
        display: flex;
        justify-content: center;
    }

    .error {
        color: red;
    }
    

</style>

