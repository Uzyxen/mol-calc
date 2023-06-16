<template>
    <div id="functions">
        <h2>=</h2>
        <input type="text" id="formula" autocomplete="off" v-bind:value="formula">
    </div>
</template>

<script>
    export default {
        props: ['formula']
    }
</script>

<style>

</style>
