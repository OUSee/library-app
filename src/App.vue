<script setup lang="ts">

import { onMounted, ref, watch, watchEffect } from 'vue';
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
const Books = ref<Book[]>([]);
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
  fetchData();  
}

const closeModal = () => {
  isModal.value = false;
  fetchData();
}

onMounted(() => {
  fetchData();
});

watch(
  isModal,
  async () => {
    fetchData()
  },
  { immediate: true }
)
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
  <Modal v-if="isModal" @close="isModal=false" :closeModal :saveChanges :setNewBook />
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
  flex-direction: column-reverse;
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


