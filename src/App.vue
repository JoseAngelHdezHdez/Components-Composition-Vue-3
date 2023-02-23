<script setup>
import { onMounted, ref } from 'vue';
//Components
import BlogPost from './components/BlogPost.vue';
import PaginatorPost from './components/PaginatorPost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue'

const posts = ref([])

const fav = ref("");

const postXPage = 10;
const inicio = ref(0);
const fin = ref(postXPage);
const loading = ref(true);

const cambiarFavorito = (post) => { 
  fav.value = post;
}

const next = () => {
    inicio.value+=postXPage;
    fin.value+=postXPage;
}

const prev = () => {
    inicio.value-=postXPage;
    fin.value-=postXPage;
}

onMounted(async() => {
  try {
    const rest = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await rest.json();
  } catch (error) {
    console.log(error)
  }  finally {
    loading.value = false;
  }
})

/* 
fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => {
    posts.value = data;
  })
  .catch((er) => console.log(er))
  .finally(() => loading.value = false)
 */
</script>

<template>
  <LoadingSpinner
    v-if="loading"
  />

  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{ fav }}</h2>

    <PaginatorPost 
      class="mb-2"
       @next="next"
       @prev="prev"
       :inicio="inicio"
       :fin="fin"
       :maxLength="posts.length"
    ></PaginatorPost>
    
    <BlogPost
      v-for="post in posts.slice(inicio, fin)" 
      :key="post.id" 
      :id=post.id   
      :title=post.title 
      :body=post.body 
      @cambiarFavoritoNombre="cambiarFavorito"
      class="mb-2"
    ></BlogPost>
  </div>
</template>