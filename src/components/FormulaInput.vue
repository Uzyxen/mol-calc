<template>
    <div id="functions">
        <div id="focused-cell">{{ focusedCell }}</div>
        <h5>functions</h5>
        <h2>
            <svg xmlns="http://www.w3.org/2000/svg" height="0.625em" viewBox="0 0 448 512">
                <!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
                <path d="M48 128c-17.7 0-32 14.3-32 32s14.3 32 32 32H400c17.7 0 32-14.3 32-32s-14.3-32-32-32H48zm0 192c-17.7 0-32 14.3-32 32s14.3 32 32 32H400c17.7 0 32-14.3 32-32s-14.3-32-32-32H48z"/>
            </svg>
        </h2>
        <input type="text" id="formula" autocomplete="off" v-bind:value="formula">
    </div>
</template>

<script>
    export default {
        props: ['formula', 'focusedCell']
    }
</script>

<style>
    #focused-cell{
        width: 150px;
        border: 1px solid #ddd;
        height: 20px;
        padding: 3px;
    }
    
    #functions{
        display: flex;
        align-items: center;
        padding: 0 5px;
    }

    #functions h2, #functions h5{
        margin: 0 5px;
    }

    #functions h5{
        cursor: pointer;
    }

    #functions h5:hover{
        background-color: #ddd;
    }
    
    #functions h2 svg{
        fill: #000;
        height: 20px;
        width: 20px;
    }

    #formula{
        outline: none;
        border: 1px solid #ddd;
        height: 20px;
        padding: 3px;
    }
</style>
