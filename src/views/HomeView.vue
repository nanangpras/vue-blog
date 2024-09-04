<template>
  <div class="container me-2 mb-4">
    <h3>Article List</h3>
    <div class="row">
      <div class="col-md-4 mb-4" v-for="item in articles" :key="item.id">
        <div class="card" style="width: 18rem;">
          <img src="https://placehold.co/150" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">{{ item.title }}</h5>
            <p class="card-text">{{ item.body.substring(0,100) }}....</p>
            <!-- <router-link :to="{ name: 'DetailArticle', params: { id: item.id } }" class="btn btn-primary">Detail</router-link> -->
            <router-link :to="`/article/${item.id}`" class="btn btn-primary">Detail</router-link>
          </div>
        </div>
      </div>
      {{ error }}
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HomeView',
  data() {
    return {
      articles: [],
      error: null
    };
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/posts?_limit=6')
      .then((result) => {
        this.articles = result.data
      }).catch((err) => {
        this.error = err
      });
  },
}
</script>
