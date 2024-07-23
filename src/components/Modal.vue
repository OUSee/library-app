<script setup lang="ts">
import { ref } from 'vue';
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

const update = () => {
    const book: Book = {
        id: lenght.value++,
        title: title.value,
        author: author.value,
        date: date.value,
        picture: url.value
    }
    setNewBook(book)
   

    alert(book.id + " : " + book.title)
    saveChanges()
}

// onMounted(() => {
//     title.value = book.Name;
//     author.value = book.Author;
//     date.value = book.publishDate;
//     url.value = book.picture;
// })
</script>



<template>
    <div class="modalWindow">
        <form action="submit" class="bookForm">
            <input @change="changeName"  type="text" placeholder="Book Title">
            <input @change="changeAuthor" type="text" placeholder="Book Author">
            <input @change="changeDate"  type="text" placeholder="Book publish date">
            <input @change="changePic"  type="text" placeholder="Image URL">
            <button @mouseenter="enterLeaveDelete" @mouseleave="enterLeaveDelete" @click="update">
                <saveIcon width="50px" height="50px" :color="iconColor" />
            </button>
        </form>
        <button class="leaveButton" @click="closeModal">
            <leaveIcon width="50px" height="50px" :color="iconColor" />
        </button>
        <img v-modal="url" alt="place for the image">
    </div>
</template>



<style scoped>
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