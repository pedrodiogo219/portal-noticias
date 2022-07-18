<template>
  <div class="home">
    <FeedNoticias></FeedNoticias>
  </div>
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
        }, { deep: true });
    }
}
</script>

<style scoped>

.home{
  padding: 0 40px;
}

</style>