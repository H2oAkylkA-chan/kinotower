<script setup lang="ts">
const authStore = useAuthStore();
</script>
<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <nuxtLink to="/"  class="navbar-brand">Kinotower </nuxtLink>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
              aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse justify-content-end" id="navbarNav" v-if="!authStore.authData">
        <ul class="navbar-nav">
          <li class="nav-item " >
            <a @click.prevent="$router.push('/signin')"  href="#" class="btn btn-outline-success me-4">signin</a>
            <a @click.prevent="$router.push('/signup')"  href="#" class="btn btn-outline-success">signup</a>
          </li>
        </ul>
      </div>
      <div v-else class="collapse navbar-collapse justify-content-end">
        <a href="#"    @click.prevent="$router.push('/profile')" class="me-2" >{{authStore.authData.fio}}</a>
        <a @click.prevent="authStore.signout() , $router.push('/')"  href="#" class="btn btn-outline-success">signout</a>
      </div>
    </div>
  </nav>


  <div class="container">
    <slot/>
  </div>
  <div class="container-fluid ">
    <footer class="d-flex flex-wrap justify-content-between align-items-center py-3 my-4 border-top">
      <p class="col-md-4 mb-0 text-body-secondary">&copy; 2024 Company, Inc</p>

      <a href="/"
         class="col-md-4 d-flex align-items-center justify-content-center mb-3 mb-md-0 me-md-auto link-body-emphasis text-decoration-none">
        <svg class="bi me-2" width="40" height="32">
          <use xlink:href="#bootstrap"/>
        </svg>
      </a>

      <ul class="nav col-md-4 justify-content-end">
        <li class="nav-item"><a href="#" class="nav-link px-2 text-body-secondary">Home</a></li>
        <li class="nav-item"><a href="#" class="nav-link px-2 text-body-secondary">Features</a></li>
        <li class="nav-item"><a href="#" class="nav-link px-2 text-body-secondary">Pricing</a></li>
        <li class="nav-item"><a href="#" class="nav-link px-2 text-body-secondary">FAQs</a></li>
        <li class="nav-item"><a href="#" class="nav-link px-2 text-body-secondary">About</a></li>
      </ul>
    </footer>
  </div>
</template>
