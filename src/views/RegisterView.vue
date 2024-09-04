<template>
    <div class="container">
        <h3>Register</h3>
        <form @submit.prevent="register">
            <div class="form-group">
                <label>Name</label>
                <input type="text" class="form-control" v-model="name" required>
            </div>
            <div class="form-group">
                <label for="exampleInputEmail1">Email address</label>
                <input type="email" class="form-control" v-model="email" required>
            </div>
            <div class="form-group">
                <label for="exampleInputPassword1">Password</label>
                <input type="password" class="form-control" v-model="password" required>
            </div>
            <button type="submit" class="btn btn-primary">Register</button>
        </form>
        <div class="mt-3 mb-3">
            <p>Already have an account ?</p><router-link to="/login" class="btn btn-warning">Login</router-link>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            name: '',
            email: '',
            password: '',
        }
    },
    methods: {
        register() {
            console.log('Registering...',this.name,this.email,this.password);
            this.$router.push('/login');
        }
    },
};
</script>