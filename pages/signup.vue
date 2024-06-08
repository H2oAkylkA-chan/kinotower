<script setup lang="ts">



const genderStore = useGendersStore();
const authStore = useAuthStore();
const router = useRouter()
const name = ref('')
const email = ref('')
const password = ref('')
const birthday = ref('')
const genders = ref('')
const errorMessage = ref ('')
const signup = async ()  => {
  try {
    if (name.value && email.value && password.value && birthday.value && genders.value) {
  await authStore.signup( {
    fio: name.value,
    email: email.value,
    password: password.value,
    birthday: birthday.value,
    gender_id: genders.value,
  })
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
          <h5 class="card-title">Registration</h5>


            <form @submit.prevent="signup">
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">name</label>
                <input v-model="name" type="text" class="form-control" id="name" aria-describedby="emailHelp"
                       placeholder="name">

              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Email</label>
                <input v-model="email" type="email" class="form-control" id="email" placeholder="email">
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" v-model="password" class="form-control" id="exampleInputPassword1"
                       placeholder="password">
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">birthday</label>
                <input type="date" class="form-control" v-model="birthday" id="exampleInputPassword1">
              </div>
              <div>
                <select v-model="genders" class="form-select" aria-label="Default select example">
                  <option selected>выбери свой пол</option>
                  <option v-for="gender in genderStore.genders" :key="gender.id" :value="gender.id"
                  >{{ gender.name }}
                  </option>


                </select>
              </div>
              <button type="submit" class="btn btn-primary d-block m-auto" style="padding: 10px 150px">sign up</button>
            </form>

        </div>
      </div>
    </div>
  </div>

</template>
