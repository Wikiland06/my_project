<script setup>
import { ref } from 'vue';
import { my_project_backend } from 'declarations/my_project_backend/index';
let displasyChat = ref('');

async function handleSubmit(e) {
  e.preventDefault();
  const target = e.target;
  const msg = target.querySelector('#msg').value;
  await my_project_backend.save_msg(msg)
  await getChat()
}

async function getChat() {
  displasyChat.value = await my_project_backend.get_chat()
}

getMsg()
</script>

<template>
  <main class="container mx-auto flex justify-center items-center flex-col p-6 border-2 border-cyan-700 w-fit rounded-xl">
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <form action="#" @submit="handleSubmit">
      <label for="msg">Enter your msg: &nbsp;</label>
      <input id="msg" alt="msg" type="text" />
      <button type="submit">Click Me!</button>
    </form>
    <section id="displasyChat">{{ displasyChat }}</section>
  </main>
</template>