<template>
  <div class="home">
    <FeedNoticias></FeedNoticias>
  </div>
</template>

<script>

import { ref } from 'vue'
import axios from 'axios';
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
    async created() {
        this.noticias = ref([]);
        const response = await axios.get("http://localhost:8080/api/noticia");
        console.log(response)
        this.noticias.value = response.data;

        JSON.parse(localStorage.getItem("noticias")) || [];
        this.$watch("noticias", (newVal) => {
            localStorage.setItem("noticias", JSON.stringify(newVal.value));
        }, { deep: true });
    }
}
</script>

<style scoped>

.home{
  padding: 0 40px;
}

</style>