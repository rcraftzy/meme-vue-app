<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const data = ref({
  email: "",
  password: "",
});

const router = useRouter();

const submit = async (e) => {
  e.preventDefault();

  const res = await fetch("http://localhost:9090/api/login", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    credentials: "include",
    body: JSON.stringify({
      email: data.value.email,
      password: data.value.password,
    }),
  });
  const status = res.status;
  if (status == 200) {
    router.push('/')
  } else {
    alert('Email o contraseña incorrecta')
  }
};
</script>
<template>
  <div>
    <form @submit.prevent="">
      <div>
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
        <button @click="submit">Login</button>
      </div>
    </form>
  </div>
</template>
