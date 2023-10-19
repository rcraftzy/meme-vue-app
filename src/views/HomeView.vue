<script setup>
import BaseCard from "../components/BaseCard.vue";
import { ref } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";

const router = useRouter();

const memes = ref([]);
let allMemes = [];

const loadData = async () => {
  const response = await fetch("https://api.imgflip.com/get_memes");
  const { data } = await response.json();

  memes.value = data.memes;
  allMemes = data.memes;
};

const searchMeme = (event) => {
  const value = event.target.value;
  memes.value = allMemes.filter((meme) =>
    meme.name.toLowerCase().includes(value.toLowerCase())
  );
};

loadData();

// Get session
const mounted = async () => {
  const url = "http://localhost:9090/api/user";
  await axios
    .get(url, {
      withCredentials: true,
    })
    .then((res) => {
      if (res.status === 200) {
        console.log(res.data);
      }
    });
};
mounted();
</script>

<template>
  <h1>Meme Search</h1>
  <input
    class="input input-bordered w-full max-w-xs"
    type="text"
    placeholder="Buscar meme"
    @input="searchMeme"
  />
  <div class="mt-6 space-y-12 lg:grid lg:grid-cols-4 lg:gap-6 lg:space-y-0">
    <BaseCard v-for="meme in memes" :key="meme.id" :meme="meme" />
  </div>
</template>
