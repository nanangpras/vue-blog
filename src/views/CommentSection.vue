<template>
    <div>
        <div v-if="userLoggedIn">
            <div class="form-floating">
                <textarea class="form-control" placeholder="Leave a comment here" id="floatingTextarea2"
                    style="height: 100px" v-model="newComment"></textarea>
                <label for="floatingTextarea2">Comments</label>
                <button @click="submitComment" class="btn btn-primary mt-3 mb-3">Comment</button>
            </div>
        </div>
        <div v-else>
            <p>Login ->>></p><router-link to="/login" class="btn btn-warning">Login here</router-link>
        </div>
        <ul class="list-group">
            Comment
            <li class="list-group-item" v-for="comment in listComment" :key="comment.id">{{ comment.body }}</li>
        </ul>
    </div>
</template>

<script>

export default {
    props: ['articleId'],
    data() {
        return {
            listComment : [
                {id:1,body: 'comment ke satu ya'},
                {id:2,body: 'comment ke dua ya'},
                {id:3,body: 'comment ke tiga ya'},
            ],
            newComment:'',
            userLoggedIn: false
        }
    },
    created() {
        this.checkLoginStatus();
    },
    methods: {
        submitComment() {
            if (this.newComment.trim() === '') return;

            const newComment = {
                id: this.listComment.length + 1,
                body: this.newComment
            };

            this.listComment.push(newComment);
            this.newComment = '';
        },
        checkLoginStatus() {
            const userLogin = JSON.parse(localStorage.getItem('user'));
            if (userLogin && userLogin.token) {
                this.userLoggedIn = true;
            } else {
                this.userLoggedIn = false;
            }
        }
    },
};
</script>