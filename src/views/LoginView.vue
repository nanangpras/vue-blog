<template>
    <div id="login">
        <form @submit.prevent="login">
            <div class="form-group">
                <label for="exampleInputEmail1">Email address</label>
                <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="email" required>
                <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone
                    else.</small>
            </div>
            <div class="form-group">
                <label for="exampleInputPassword1">Password</label>
                <input type="password" class="form-control" id="exampleInputPassword1" v-model="password" required>
            </div>
            <button type="submit" class="btn btn-primary mt-3">Submit</button>
        </form>
        <div class="mt-3 mb-3">
            <p>Dont have account ?</p><router-link to="/register" class="btn btn-warning">Register here</router-link>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            email:'',
            password:'',
        };
    },
    methods: {
        login() {
            if (this.email === 'email@email.com' && this.password === '12345678') {
                const userData = {
                    email: this.email,
                    token: 'xxxyz'
                };

                localStorage.setItem("user", JSON.stringify(userData));
                this.$router.push('/');
            }else{
                alert('Login failed',this.email,this.password);

            }
        },
    },
};
</script>