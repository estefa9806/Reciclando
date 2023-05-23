<template>
   <div>
   <Header></Header>
    <form @submit.prevent="submit">
        <div class="field">
          <label>Usuario</label>
          <input type="text" v-model="usuario" />
        </div>
        <div class="field">
          <label>Clave</label>
          <input type="password" v-model="clave" />
        </div>
        <div class="action">
          <button>Loguearse</button>
        </div>
      </form>
     
   </div>
</template>

<script setup>
import Header from "../Header.vue";
import { ref, } from "vue";
const clave = ref("");
const usuario = ref("");
</script>

<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}
</style>
