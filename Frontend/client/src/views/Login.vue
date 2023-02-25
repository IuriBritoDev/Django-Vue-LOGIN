<template>
    <div class="signup">
        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col-lg-4 col-md-8 col-sm-8">
                    <div class="card shadow">
                        <div class="card-title text-center border-bottom">
                            <h2 class="p-3">Login</h2>
                        </div>
                        <div class="card-body">
                            <form @submit.prevent="submitform">
                                <div class="mb-4">
                                    <label for="username" class="form-label">Username</label>
                                    <input type="text" class="form-control" v-model="username">
                                </div>
                                <div class="mb-4">
                                    <label for="password" class="form-label">Password</label>
                                    <input type="password" class="form-control" v-model="password">
                                </div>
                                <div class="d-grid mb-4">
                                    <button class="btn btn-primary mt-3">Login</button>
                                </div>
                                <div class="alert alert-danger" role="alert" v-if="errors.length">
                                    <p v-for="error in errors" :key="error">{{ error }}</p>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Login',
    data(){
        return{
            username: '',
            password: '',
            errors: [],
        }
    },
    mounted(){
        document.title = 'Login'
    },
    methods:{
        async submitform(){
            axios.defaults.headers.common["Authorization"] = ""

            localStorage.removeItem("token")
            const formData = {
                username: this.username,
                password: this.password,
            }
            await axios
                    .post("/api/v1/token/login", formData)
                    .then(response=>{
                        const token = response.data.auth_token

                        this.$store.commit('setToken', token)
                        axios.defaults.headers.common["Authorization"] = "Token" + token
                        localStorage.setItem("token", token)
                        const toPath = this.$route.query.to || '/home'

                        this.$router.push(toPath)
                    })
                    .catch(error=>{
                        if(error.response){
                            for(const property in error.response.data){
                                this.errors.push(`${property}: ${error.response.data[property]}`)
                            }
                        }
                        else if(error.message){
                            this.errors.push('something went wrong, please try again')
                        }
                    })

        }
    }
}
</script>

<style>

</style>