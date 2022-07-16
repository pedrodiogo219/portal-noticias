<template>

  <a href="#/">/</a> |
  <a href="#/noticia">noticia</a> |
  <a href="#/non-existent-path">Broken Link</a>
  <component :is="currentView"/>


  <button v-on:click="chama()">add noticia</button>
</template>

<script>
import NoticiaCompleta from './components/NoticiaCompleta.vue'
import NotFound from './components/NotFound.vue'
import FeedNoticias from './components/FeedNoticias.vue'

import { ref } from 'vue'


const routes = {
  '/': FeedNoticias,
  '/noticia': NoticiaCompleta
}

export default{
  name: 'App',
  noticias: ref([]),
  components: {
    NoticiaCompleta
  },
  data(){
    return {
      currentPath: window.location.hash,
    }
  },

  created(){
    this.noticias = ref([])
    this.noticias.value = JSON.parse(localStorage.getItem('noticias')) || []

    this.$watch('noticias', (newVal) => {
      localStorage.setItem('noticias', JSON.stringify(newVal.value))
      console.log('entrou aqui')
    }, {deep: true})
  },
  
  computed: {
    currentView() {
      console.log(this.currentPath)
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
		})

    
  },
  methods: {
    chama: function(){
      this.noticias.value.push({
        id: 1,
        titulo: 'Primeira Noticia',
        descricao: 'Essa é a primeira noticia do site',
        corpo: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris sem nisi, volutpat vel libero eget, bibendum pellentesque nisi. Ut a laoreet libero. Vestibulum euismod ipsum sed dictum semper. Sed non ante non arcu interdum commodo. Morbi ultricies, elit id mattis porttitor, diam lectus rutrum lectus, non laoreet orci velit ac nisi. Sed vel diam feugiat, dictum dolor vitae, cursus orci. Quisque eget nunc porttitor, euismod libero et, pretium velit. Cras mauris est, bibendum in feugiat tincidunt, aliquet a sem. Nullam ac nisl dignissim felis maximus euismod non vel ipsum. Aliquam imperdiet interdum lacus, sit amet dictum tortor tristique sed. Fusce hendrerit mattis dui quis congue. Fusce orci orci, placerat consectetur sem id, consequat tempus ipsum. Nullam vitae risus lectus. Sed consequat aliquet velit eget semper. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae;'
      })
      console.log(this.noticias.value)
    }
  },
  
  
};

// watch(noticias , (newVal) => {
//   localStorage.setItem('noticias', JSON.stringify(newVal))
//   console.log('entrou aqui')
// }, {deep: true})

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
