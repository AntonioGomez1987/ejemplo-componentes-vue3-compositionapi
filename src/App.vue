<script setup>
import { onMounted, ref } from "vue";

import PaginatePost from "./components/PaginatePost.vue"
import BlogPost from "./components/BlogPost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]);
const postporpage = 5;
const inicio = ref(0);
const fin = ref(postporpage);
const loading = ref(true);

const favorito = ref("")

const cambiarFavorito = (title) => {
  favorito.value= title
}

const next = () => {
  inicio.value = inicio.value + postporpage
  fin.value = fin.value + postporpage
}

const previus = () => {
  inicio.value = inicio.value - postporpage
  fin.value = fin.value - postporpage
}

onMounted(async() => {
  loading.value = true;
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json();
  } catch (error) {
      console.log(error);
  } finally{
      setTimeout(() => (loading.value = false), 1500);
    }
})

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then(res => res.json())
//   .then(data => {
//     posts.value = data;
//   })
//   .catch((e) => console.log(e))
//   .finally(() => {
//       //para mostrar el spinner 2 segundos no es aconsejable es para 
//       setTimeout(() =>{
//         loading.value = false
//       }, 2000)
//     })

</script>

<template>
  <LoadingSpinner v-if="loading"/>
    <div class="container" v-else="">
        <h1>Blog</h1>
        <h2>Mis Post Favoritos: {{ favorito }} </h2>


        <PaginatePost 
          @next="next" 
          @prev="previus" 
          :ini="inicio" 
          :fin="fin" 
          :maxLength="posts.length"
          class="mb-2"/>


        <BlogPost
            v-for="post in posts.slice(inicio, fin)"
            :key="post.title"
            :title="post.title"
            :id="post.id"
            :body="post.body"
            class="mb-2"
            @cambiarFavoritoNombre="cambiarFavorito"
        />
    </div>
</template>































<!-- <script>

import { ref } from 'vue';


export default {
  setup(){

    const counter = ref(0)

    const increment = () => {
      counter.value++
    }

    return{
      counter,
      increment,
    }

  }
}

</scrip> -->

<!-- <script setup></scrip> -->



<!-- export default {
  data(){
    return {
      counter: 0
    }
  },
  methods: {
    increment(){
      this.counter ++
    }
  }
} -->