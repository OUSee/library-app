<script setup lang="ts">

import { onMounted, ref, watchEffect } from 'vue';
import Head from './components/Head.vue';
import Modal from './components/Modal.vue';
import Book from './components/Book.vue';
import type { Ref } from 'vue';

type Book = {
  id: number;
  title: string;
  author: string;
  date: string;
  picture: string;
};


const isLoading = ref(true);
const isModal = ref(false);
const Books = ref<Book[]>();
const newBook = ref<Book>({id:1, title:"", author:"", date:"", picture:""  });


async function fetchData() {
  const resp = await fetch('https://38d67d2cffbadc09.mokky.dev/books');
  const data = await resp.json();

  if (!resp.ok) {
    throw new Error(data.message || 'Something went wrong');
  }

  Books.value = data;

  Books.value = data;
  console.log(Books.value)
  isLoading.value = false
}

const onDelete = async (book:Book) => {
  const req = new Request("https://38d67d2cffbadc09.mokky.dev/books/" + book.id, { method: 'DELETE' });
  const res = await fetch(req);
  if (res.ok) {
    alert("book deleted: " + book.title.toUpperCase())
    fetchData()
  }
  else {
    alert("error deleting book")
  }
}

const setNewBook = (book: Book) => {
  newBook.value = book;
}

 function openModal() {
  isModal.value = true;
  console.log("tried to open modal", isModal);
}

const saveChanges = async () => {

  Books.value?.push(newBook.value)

  

  const request = new Request("https://38d67d2cffbadc09.mokky.dev/books", {
    method: "PATCH",
    body: JSON.stringify(Books.value),
  });
  const response = await fetch(request);
  if (response.ok) {
    alert("book saved")
  }
  else {
    alert("something went wrong, try again later"+ response.status)
  }
}


const closeModal = () => {
  isModal.value = false;
  console.log("tried to close modal", isModal.value)
}

onMounted(() => {
  fetchData();
});

watchEffect(() => { fetchData() })
</script>



<template>
  <div class="loader" v-if="isLoading">
    <img src="./assets/200w.gif" alt="Racoon">
    <p>...Loading</p>
  </div>
  <div class="containerMain" v-else>

    <Head :openModal="openModal" />
    <ul class="list">
      <Book v-for="book in Books" :book="book" :onDelete/>
    </ul>
  </div>
  <Modal v-if="isModal" @close="isModal=false" :lenght="Books?.length" :closeModal :saveChanges :setNewBook />
</template>



<style scoped>
.containerMain{
  display: flex;
  flex-direction: column;
  margin: 10px 50px;
  gap: 20px;
}
.list{
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 15px;
}
.loader{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 700px;
}
img{
  border-radius: 50%;
  width: 500px;
  height: 500px;
}
</style>


