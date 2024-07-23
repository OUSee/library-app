<script setup>
import booksIcon from './icons/booksIcon.vue';
import plusIcon from './icons/plusIcon.vue';

const { openModal }  = defineProps(["openModal"])

</script>


<template>
    <header class="containerHeader">
        <div class="logo">
            <booksIcon width="40px" height="40px" color="#000000" />
        </div>
        <h1 class="title">Library</h1>
        <button @click="openModal" >
            <plusIcon width="25px" height="25px" color="#000000" />
        </button>
    </header>
</template>


<style scoped>
button{
    margin: 0;
    padding: 10px;
    width: fit-content;
    height: fit-content;
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    border-radius: 50%;
    background-color: lightgray;
    box-shadow: 0 0 5px;
}
button:hover{
    background-color: white;
    cursor: pointer;
    box-shadow: 0 0 10px grey;
}
.containerHeader{
    cursor: default;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}
.title{
    font-family: Arial, Helvetica, sans-serif;
}
</style>
