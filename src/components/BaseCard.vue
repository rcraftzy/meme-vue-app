<script setup>
import { ref } from "vue";
import HeartIcon from "../components/HeartIcon.vue";

defineProps({
  meme: {
    type: Object,
    default: () => ({}),
  },
});

const favs = ref([]);

const toggleFav = (memeId) => {
  const index = favs.value.indexOf(memeId);
  if (index > -1) {
    favs.value.splice(index, 1);
  } else {
    favs.value.push(memeId);
  }
};

</script>
<template>
  <div class="card card-compact w-76 bg-base-100 shadow-xl">
    <figure><img :src="meme.url" alt="Shoes" class="h-full w-full object-cover object-center" /></figure>
    <div class="flex flex-1 items-end justify-between text-sm">
      <h2 class="card-title">{{ meme.name }}</h2>
      <div class="card-actions justify-end">
        <HeartIcon
          class="iHeart"
          :class="{ selected: favs.includes(meme.id) }"
          @click="toggleFav(meme.id)"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.iHeart{
  width: 30px;
  color: #000;
}
.iHeart.selected{
  color: #a222ae;
}
</style>
