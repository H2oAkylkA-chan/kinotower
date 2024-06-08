<script setup lang="ts">
const authStore = useAuthStore();
const router = useRouter()
const email = ref('')
const password = ref('')
const errorMessage = ref('')
const signin = async ()  => {
  try {
    if (email.value && password.value ) {
      await authStore.signin( {
        email: email.value,
        password: password.value,

      });
      router.push('/')
    }
  } catch (e:any) {
    errorMessage.value = e.message
  }
}
</script>

<template>
  <div class="row">
    <div class="col">
      <div class="card m-auto" style="width: 45rem;">
        <div class="card-body">
          <div v-if="errorMessage" class="alert alert-danger" role="alert">
            {{errorMessage}}
          </div>
          <h5 class="card-title text-center">authorization</h5>
          <form action="" >
            <form  @submit.prevent="signin">
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Email</label>
                <input type="email" v-model="email" class="form-control" id="email"placeholder="email">
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input v-model="password" type="password" class="form-control" id="exampleInputPassword1"placeholder="password">
              </div>

              <button type="submit" class="btn btn-primary d-block m-auto" style="padding: 10px 150px" >sign in</button>
            </form>
          </form>
        </div>
      </div>
    </div>
  </div>

</template>
