<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const data = ref({
  user_name: "",
  email: "",
  password: "",
});

const router = useRouter();

const submit = async (e) => {
  e.preventDefault();

  const res = await fetch("http://localhost:9090/api/register", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      user_name,
      email,
      password,
    }),
  });
  
  const status = res.status
  if(status == 200) {
    console.log("Logged in")
  }else{
    console.log("No out")
  }

  console.log(data.value);
};
</script>
<template>
  <div>
    <form @submit.prevent="">
      <div>
        <input
          type="text"
          name="first_name"
          id="first_name"
          placeholder="first name"
          v-model="data.first_name"
        />
        <input
          type="text"
          name="last_name"
          id="last_name"
          placeholder="last name"
          v-model="data.last_name"
        />
        <input
          type="text"
          name="user_name"
          id="user_name"
          placeholder="user name"
          v-model="data.user_name"
        />
        <input
          type="email"
          name="email"
          id="email"
          placeholder="email"
          v-model="data.email"
        />
        <input
          type="password"
          name="password"
          id="password"
          placeholder="password"
          v-model="data.password"
        />
      </div>
      <div>
        <button @click="submit">Register</button>
      </div>
    </form>
  </div>
</template>
