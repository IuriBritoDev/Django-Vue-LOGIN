<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container">
      
      <router-link class="navbar-brand" to="/">Login System</router-link>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto">
          <template v-if="$store.state.isAuthenticated">
          <li class="nav-item mx-2">
            <router-link class="btn btn-primary" to="/">My Account</router-link>
          </li>
          </template>
          <template v-else>
            <li class="nav-item mx-2">
            <router-link class="btn btn-primary" to="/">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link class="btn btn-success" to="/Signup">SignUp</router-link>
          </li>
          </template>
          
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style scoped lang="scss">

</style>
