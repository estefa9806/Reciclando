<template>
    <div class="movements">
        <h2 class="title">Historial</h2>
        <div class="content">
            <Movimiento v-for="{ id,nombreResiduo,descripcion,amount} in movimientos" 
            :key="id"
            :id="id"
            :nombreResiduo="nombreResiduo"
            :descripcion="descripcion"
            :amount="amount"
            @remove="remove"
            />

        </div>
    </div>
</template>



<script setup>
import { defineProps,toRefs,defineEmits } from 'vue';
import Movimiento from "./Movimiento.vue";
const props = defineProps({
    movimientos:{
        type:Array,
        default:()=>[],
    }

});
const { movimientos } = toRefs(props);
const emit = defineEmits(["remove"]);
const remove = (id) => {
  emit("remove", id);};
</script>

<style scoped>
.movements {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
}
.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}
.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>