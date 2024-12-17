<template>
  <div class="container-fluid d-flex justify-content-center align-items-center " style="height: 80vh;">
    <div class="card shadow" style="width: 30rem; background-color: #FFFFFF;">
      <div class="card-body">
        <h5 class="card-title text-center">LOGIN</h5>
        <form @submit.prevent="handleLogin">
          <input v-model="email" type="text" class="rounded-5 mb-5 ps-3" placeholder="Username"
            style="width:28rem; height:3rem;background-color: #FFFFFF; ">
          <input v-model="password" type="password" class="rounded-5 mb-5 ps-3" placeholder="Password"
            style="width:28rem; height:3rem;background-color: #FFFFFF; ">
          <div class="row justify-content-center">
            <input type="submit" class="btn rounded-5"
              style="width:8rem; background-color: #FFFFFF;" value="Login">
          </div>
          <!-- <i @click="togglepasswordvisibility" :class="ispasswordvisible ? 'bi bi-eye-fill' : 'bi  bi-eye-slash-fill'"
            class="position-absolute top-50 end-0 translate-middle-y me-3" style="cursor: pointer;"></i> -->
        </form>
      </div>
    </div>
  </div>

</template>

<script setup>
const client = useSupabaseClient()
const email = ref("");
const password = ref("");
// const ispasswordvisible = ref(false)
const errorMessage = ref("")

// function togglepasswordvisibility() {
//   ispasswordvisible.value = !ispasswordvisible.value
// }

async function handleLogin() {
  const { data, error } = await client.auth.signInWithPassword({
    email: email.value,
    password: password.value
  })

  if (error) {
    if (error.message.includes("invalid email")) {
      errorMessage.value = "Email yang anda masukan salah"
    } else if (error.message.includes("incorrect password"))
      errorMessage.value = "Password yang anda masukan salah"
  } else {
    errorMessage.value = "Periksa lebih teliti !!!"
  }
  setTimeout(() => {
    errorMessage.value = ""
  }, 1000)

  if (error) throw error
  navigateTo('/menu')
}



</script>
