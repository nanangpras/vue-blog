<template>
    <div>
        <div class="container me-2 mb-4">
            <h3>Detail </h3>
            <div class="row">
                <div class="col">
                    <div class="card">
                        <img :src="getImageUrl(article.id)" class="card-img-top" alt="...">
                        <div class="card-body">
                            <h5 class="card-title">{{ article.title }} </h5>
                            <p class="card-text">{{ article.body }}</p>
                        </div>
                    </div>
                </div>
            </div>
            <!-- comentar -->
             <div class="mt-3">
                 <comment-section :article-id="article.id"></comment-section>
             </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import CommentSection from '../views/CommentSection.vue';


export default {
    name: 'HomeView',
    components: {
        CommentSection
    },
    data() {
        return {
            article:{},
            error:null,
        }
    },
    created() {
        const articleId = this.$route.params.id;
        // console.log(articleId);
        
        axios.get(`https://jsonplaceholder.typicode.com/posts/${articleId}`)
        .then((result) => {
            this.article = result.data;
            
        }).catch((err) => {
            this.error = err
        });
    },
    methods: {
        getImageUrl(id) {
            return `https://picsum.photos/seed/${id}/50/10`;
        }
    }
};
</script>