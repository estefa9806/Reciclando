<template>
  <button @click="showModal = true">Agregar movimiento</button>
  <teleport to="#app">
    <Modal v-show="showModal" @close="showModal = false">
      <form @submit.prevent="submit">
        <div class="field">
          <label>Nombre del reciclaje:</label>
          <select  v-model="nombreResiduo">
            <option disabled value="">Seleccione uno</option>
            <option value="aceite">Aceite usado</option>
            <option value="pilas">Baterias</option>
            <option value="botellas">Botellas/plastico</option>
            <option value="botellasEco">Botellas Ecologicas</option>
            <option value="vidrio">Vidrio</option>
            <option value="latas">Latas</option>
            <option value="carton">Papel y cartón</option>
          </select>
          <!--<input type="text" v-model="nombreResiduo" />-->
        </div>
        <div class="field">
          <label>Monto</label>
          <input type="number" v-model="amount" />
        </div>
        <div class="field">
          <label>Descripción</label>
          <textarea rows="4" v-model="descripcion"></textarea>
        </div>
        <div class="action">
          <button>Agregar movimiento</button>
        </div>
      </form>
    </Modal>
  </teleport>
</template>

<script setup>
import { ref, defineEmits } from "vue";
import Modal from "./Modal.vue";

const showModal = ref(false);
const nombreResiduo = ref("");
const amount = ref(0);
const descripcion = ref("");

const emit = defineEmits(["create"]);

const submit = () => {
  showModal.value = !showModal.value;
  emit("create", {
    id: new Date(),
    nombreResiduo: nombreResiduo.value,
    descripcion: descripcion,
    amount: amount.value,
    time: new Date(),

  });
  nombreResiduo.value = "";
  descripcion.value = "";
  amount.value = "";

};
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

input,select,
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
