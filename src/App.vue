<template>
  <div class="title">
    <h1>Joe Zhang 餐點統計工具📝</h1>
  </div>

  <Order />
</template>

<script lang="ts" setup>
import Order from "./components/Order.vue";
</script>

<style>
body,
html {
  margin: 0;
  user-select: none;
}

h1,
h2,
h3,
h4,
h5 {
  margin: 0;
}

h1 {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #799a79;
  color: white;
  padding: 5px;
}

input {
  background: none;
  outline: none;
  border: 2px solid #99c199;
  margin: 10px 0 0 5px;
  width: 15rem;
  height: 2.5rem;
  border-radius: 10px;
  padding-left: 1rem;
  color: #405240;
  font-weight: 600;
  font-size: 1rem;
}
input:hover {
  background-color: rgba(180, 229, 180, 0.5);
}
input:focus {
  background-color: rgba(180, 229, 180, 0.2);
}

button {
  outline: none;
  margin: 20px 0 0 0;
  padding: 0.7rem 1.2rem;
  border-radius: 10px;
  outline: none;
  border: 1px solid white;
  background-color: #799a79;
  font-size: 1.1rem;
  font-weight: 600;
  color: white;
  transition: 1s;
  cursor: pointer;
}
button:hover {
  background-color: #5f7b5f;
  transition: 0s;
}
button:active {
  transform: scale(0.97);
}
</style>
