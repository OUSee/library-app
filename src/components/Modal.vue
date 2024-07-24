<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import saveIcon from "./icons/saveIcon.vue"
import leaveIcon from './icons/leaveIcon.vue'

const { closeModal, saveChanges, setNewBook, lenght } = defineProps(["book", "closeModal", "saveChanges", "setNewBook",  "lenght"])

type Book = {
    id: number;
    title: string;
    author: string;
    date: string;
    picture: string;
};

const title = ref("");
const author = ref("");
const date = ref("");
const url = ref("");
const iconColor = ref("#1f1f1f")




const changeName = (e: InputEvent) => { 
    title.value = (e.target as HTMLInputElement).value;
}
const changeAuthor = (e: InputEvent) => {
    author.value = (e.target as HTMLInputElement).value;
}
const changeDate = (e: InputEvent) => {
    date.value = (e.target as HTMLInputElement).value;
}
const changePic = (e: InputEvent) => {
    url.value = (e.target as HTMLInputElement).value;
}


const enterLeaveDelete = () => {
    if (iconColor.value === "#1f1f1f") { 
        iconColor.value = "#8dc149";
    }
    else {
        iconColor.value = "#1f1f1f";
    }
}


// onMounted(() => {
//     title.value = book.Name;
//     author.value = book.Author;
//     date.value = book.publishDate;
//     url.value = book.picture;
// })

watchEffect(() => {
 
})
</script>



<template>
    <div class="modalWindow">   
        <form id="form" action="https://38d67d2cffbadc09.mokky.dev/books" method="POST" class="bookForm">
            <input name="title" @change="changeName" type="text" placeholder="Book Title">
            <input name="author" @change="changeAuthor" type="text" placeholder="Book Author">
            <input name="date" @change="changeDate" type="text" placeholder="Book publish date">
            <input name="picture" @change="changePic" type="text" placeholder="Image URL">
            <button type="submit" @mouseenter="enterLeaveDelete" @mouseleave="enterLeaveDelete" @click="saveChanges">
                <saveIcon width="50px" height="50px" :color="iconColor" />
            </button>
        </form>
        <button type="reset" class="leaveButton" @click="closeModal">
            <leaveIcon width="50px" height="50px" :color="iconColor" />
        </button>
        <img id="url" src="https://img.recraft.ai/Z5ro2pipsNIByd-JeQYYee5tiB0fivJcO2yA95TYND8/rs:fit:1024:1434:0/q:80/g:no/plain/abs://prod/images/b9d19447-cd39-4494-904e-35e45949cb83@avif" alt="place for the image">
    </div>
</template>



<style scoped>

    #url{
        width: 100px;
        height: 130px;
        margin-left: 100px;
        margin-top: 100px;
    }
    .modalWindow{
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 700px;
        background-color: rgba(0, 0, 0, 0.5);
    }
    .bookForm{
        margin: auto;
        position: absolute;
        top: 150px;
        left: 500px;
        width: 500px;
        height: 200px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    input{
        width: 100%;
        margin-bottom: 10px;
        padding: 5px 10px;
    }



    .leaveButton{
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
        padding: 5px;
        margin: 20px;
    }
    .leaveButton:hover{
        box-shadow: 0 0 10px lightcoral;
        cursor: pointer;
    }
</style>