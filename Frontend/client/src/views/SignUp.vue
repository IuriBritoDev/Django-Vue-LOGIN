<template>
    <div class="signup">
        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col-lg-4 col-md-8 col-sm-8">
                    <div class="card shadow">
                        <div class="card-title text-center border-bottom">
                            <h2 class="p-3">Sign Up</h2>
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
                                <div class="mb-4">
                                    <label for="password" class="form-label">Password</label>
                                    <input type="password" class="form-control" v-model="password2">
                                </div>
                                <div class="d-grid mb-4">
                                    <button class="btn btn-primary mt-3">Sign up</button>
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
    name: 'SignUp', 
    data(){
        return{
            username: '',
            password: '',
            password2: '',
            errors: [],
        }
    },
    methods:{
        submitform(){
            this.errors = []

            if(this.username === ''){
                this.errors.push('The username is missing')
            }
            if(this.password === '' || this.password2 === ''){
                this.errors.push('The password is missing')
            }
            if(this.password2 !== this.password){
                this.errors.push('The passowords dosen\'t match')
            }
            if(!this.errors.length){
                console.log('aaaaaaaaaa')
                const formData = {
                    username: this.username,
                    password: this.password
                }
                axios 
                    .post("/api/v1/users/", formData)
                    .then(response=>{
                        this.$router.push('/')
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
}
</script>

<style>

</style>