<script setup lang="ts">

import trashIcon from './icons/trashIcon.vue';

const { book, onDelete } = defineProps(["book", "onDelete"])

</script>



<template>
    <li class="container" >
        <img :src="book.picture" alt="img">
        <div class="info">
            <p class="author">{{ book.author }}</p>
            <h2 class="title">
                {{ book.title.toUpperCase() }}
            </h2>
            <p class="date">{{ book.date }}</p>
        </div>
        <button class="deleteButton" @click="onDelete(book)">
            <trashIcon width="30px" height="30px" color="#000000"/>
        </button>
    </li>
</template>



<style scoped>
    h2{
        margin: 0;
    }
    p{
        margin: 0;
    }
    .container{
        display: flex;
        flex-direction: row;
        gap: 10px;
        background-color: lightgrey;
        border-radius: 15px;
        padding: 20px 30px; 
        box-shadow: 0 0 10px gray;
        cursor: default;
    }
    img{
        width: 100px;
        height: 120px;
        border-radius: 10px;
        margin-right: 20px;
        border: 1px white solid;
        padding: 2px;
    }
    .info{
        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }
    .title{
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        padding: 10px 5px;
    }
    .author, .date{
        font-family: Arial, Helvetica, sans-serif;
        padding: 0 5px;
        color: rgb(48, 48, 48);
    }
    .date{
        font-size: 0.8em;
        font-style: italic;
        color: rgb(96, 96, 96);
    }
    .deleteButton{
        border-radius: 50%;
        width: 80px;
        height: 80px;
        margin-left: auto;
        margin-top: auto;
        margin-bottom: auto;
        border: 0;
        background-color: lightgrey;
    }
    .deleteButton:hover{
        cursor: pointer;
        background-color: rgb(174, 174, 174);
        box-shadow: 0 0 5px red;
    }
</style>