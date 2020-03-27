<template>
<div class="root">
-------------
    <a class="upvote" v-on:click="count += 1">up</a>
    <a class="downvote" v-on:click="count -= 1">down</a>
    <a class="report" v-on:click="reported()" >Report</a>
    <div class="countResult">
    {{count}}
    </div>
------------>
</div>
</template>

<script>

export default {
    data: () => {
        return {
            count: 0
        }
    },
    computed: {
        
    }
   /*  methods: {
        thumbsUp: () => {
            this.count += 1;
        }
    } */
}

</script>

<style>

a:hover {
    cursor: pointer;
    -webkit-user-select: none;
}

.upvote{
    color: green;
}

.downvote{
    color: red;
}
</style>

  function newFunction() {
    return "You have reported this snippet"
  }
