<template>
    <div class="alert alert-success text-center">
        <h1>Wrong Answer </h1>
        <h1>Total Score : {{counter}} / 10 </h1>
        <hr>
        <button class="btn btn-primary" @click="onNextQuestion">Next Question</button>
    </div>
</template>
<style>

</style>
<script>

    export default{
        props:['counter'],
        methods: {
            onNextQuestion() {
                this.$emit('confirmed');
            }
        }
    }
</script>
