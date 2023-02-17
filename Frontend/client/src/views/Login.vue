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
                            <form action="">
                                <div class="mb-4">
                                    <label for="username" class="form-label">Username</label>
                                    <input type="text" class="form-control">
                                </div>
                                <div class="mb-4">
                                    <label for="password" class="form-label">Password</label>
                                    <input type="password" class="form-control">
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
    }
}
</script>

<style>

</style>