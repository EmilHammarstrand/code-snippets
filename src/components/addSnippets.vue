<template>
<div class="root">
----------------
    <div class="formGroup">
        <label>Alias</label>
        <input type="text" v-model="alias">
    </div>
    
    <div class="formGroup">
        <label>Your code snippet</label>
        <textarea type="text" v-model="codeSnippet"></textarea>
    </div>

    <div class="button">
        <!-- <button @click="asd"></button> -->
    </div>

    <div class="snippetResult">
        {{alias}}
    </div>
----------------->
    <!-- <button @click="displayText">Publish</button> -->
</div>
</template>

<script>

export default {

    
    data: () => ({
        alias: "",
        codeSnippet: ""
    }),
    method:{

    }
}

</script>

<style>

</style>

