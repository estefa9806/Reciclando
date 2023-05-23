<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume :total-label="'Dinerciclando'" :label="label" :total-amount="totalAmount" :amount="amount">
        <template #grafica>
          <Graphi :amounts="amounts" :select="select" />
        </template>
        <template #accion>
          <Action @create="create"></Action>
        </template>
      </Resume>

    </template>
    <template #movements>
      <Movements :movimientos="movimientos" @remove="remove" />
    </template>
  </Layout>
</template>

<script>
import { computed } from 'vue';
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume/Index.vue";
import Movements from "./Movimientos/IndexMovimiento.vue";
import Action from "./Action.vue";
import Graphi from "./Resume/Graphi.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
    Action,
    Graphi,
  },
  data() {
    return {
      label: null,
      amount: null,
      movimientos: [
        {
          id: 0,
          nombreResiduo: "Pilas",
          descripcion: "Recicla en niquia tienda D1",
          amount: 10000,
          fecha: new Date("02-05-2023"),
        },
        {
          id: 1,
          nombreResiduo: "Gatos",
          descripcion: "Gasto Exito",
          amount: -5000,
          fecha: new Date("05-05-2023"),
        },
        {
          id: 2,
          nombreResiduo: "Botellas",
          descripcion: "Punto niquia",
          amount: 6000,
          fecha: new Date("10-05-2023")
        },
      ]
    }
  },

  computed: {
    amounts() {
      const lastDays = this.movimientos
        .filter(m => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return m.fecha > oldDate;
        })
        .map(m => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => {
          return suma + movement
        }, 0);
      });
    },
    totalAmount() {
      return this.movimientos.reduce((suma, m) => { return suma + m.amount }, 0)
    },
    mounted() {
    const movimientos = JSON.parse(localStorage.getItem("movimientos"));
    console.log(movimientos);
    if (Array.isArray(movimientos)) {
      this.movimientos = movimientos.map(m => {
        return { ...m, time: new Date(m.fecha) };
      });
    }
  },
  },
  methods: {
    create(movement) {
      this.movimientos.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movimientos.findIndex(m => m.id === id);
      this.movimientos.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem("movimientos", JSON.stringify(this.movimientos));
    },
    select(el) {
      console.log("mono",el);
      this.amount = el;
    }

  }
};

</script>
