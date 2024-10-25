<template>
  <div class="container-fluid d-flex justify-content-center align-items-center " style="height: 80vh;">
    <div class="card shadow" style="width: 30rem; background-color: #FFFFFF;">
      <div class="card-body">
        <h5 class="card-title text-center">LOGIN</h5>
        <form action="">
          <input v-model="email" type="text" class="rounded-5 mb-5 ps-3" placeholder="Username"
            style="width:28rem; height:3rem;background-color: #FFFFFF; ">
          <input v-model="password" type="password" class="rounded-5 mb-5 ps-3" placeholder="Password"
            style="width:28rem; height:3rem;background-color: #FFFFFF; ">
          <div class="row justify-content-center">
            <button @click="handleLogin" type="button" class="btn rounded-5"
              style="width:8rem; background-color: #FFFFFF;">Login</button>
          </div>
        </form>
      </div>
    </div>
  </div>

</template>

<script setup>
definePageMeta({
  layout: '',

})
const client = useSupabaseClient()
const email = ref("");
const password = ref("");

async function handleLogin() {
  console.log(email.value)
  console.log(password.value)
  const { data, error } = await client.auth.signInWithPassword({
    email: email.value,
    password: password.value
  })
  if (error) throw error
  navigateTo('/')
}
</script>
