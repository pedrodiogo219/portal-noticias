<template>
  <div class="home">
    <FeedNoticias></FeedNoticias>
  </div>


  <button v-on:click="chama()">add noticia</button>
</template>

<script>

import { ref } from 'vue'
import FeedNoticias from '@/components/FeedNoticias.vue'

export default {
    name: "HomeView",
    components: {
      FeedNoticias
    },
    noticias: ref([]),
    data() {
        return {
            currentPath: window.location.hash,
        };
    },
    created() {
        this.noticias = ref([]);
        this.noticias.value = JSON.parse(localStorage.getItem("noticias")) || [];
        this.$watch("noticias", (newVal) => {
            localStorage.setItem("noticias", JSON.stringify(newVal.value));
            console.log("entrou aqui");
        }, { deep: true });
    },
    methods: {
        chama: function () {
            this.noticias.value.push({
                id: 1,
                titulo: "Primeira Noticia",
                descricao: "Essa é a primeira noticia do site",
                corpo: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris sem nisi, volutpat vel libero eget, bibendum pellentesque nisi. Ut a laoreet libero. Vestibulum euismod ipsum sed dictum semper. Sed non ante non arcu interdum commodo. Morbi ultricies, elit id mattis porttitor, diam lectus rutrum lectus, non laoreet orci velit ac nisi. Sed vel diam feugiat, dictum dolor vitae, cursus orci. Quisque eget nunc porttitor, euismod libero et, pretium velit. Cras mauris est, bibendum in feugiat tincidunt, aliquet a sem. Nullam ac nisl dignissim felis maximus euismod non vel ipsum. Aliquam imperdiet interdum lacus, sit amet dictum tortor tristique sed. Fusce hendrerit mattis dui quis congue. Fusce orci orci, placerat consectetur sem id, consequat tempus ipsum. Nullam vitae risus lectus. Sed consequat aliquet velit eget semper. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae;"
            });
            console.log(this.noticias.value);
        }
    }
}
</script>
