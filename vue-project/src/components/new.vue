<script setup>
import { ref } from 'vue';

let id = 0;

const shujutsu = ref([]);
const sosa_setsumei = ref('');
const kingaku_sosa = ref('');

const solde = ref(0);

const supprimerOperation = (id) => {
  const index = shujutsu.value.findIndex((operation) => operation.id === id);

  if (index !== -1) {
    shujutsu.value.splice(index, 1);
    solde.value -= operation.montant;
  }
};

const ajouterOperation = () => {
  const montantNumerique = parseFloat(kingaku_sosa.value);

  shujutsu.value.push({
    id: shujutsu.value.length + 1,
    description: sosa_setsumei.value,
    montant: montantNumerique,
  });

  solde.value += montantNumerique;

  sosa_setsumei.value = '';
  kingaku_sosa.value = '';
};
</script>

<template>
  <h2>Opérations récentes :</h2>
  <form @submit.prevent="ajouterOperation">
    <label for="operation-description">Description :</label>
    <input type="text" id="operation-description" v-model="sosa_setsumei" required>
    
    <label for="operation-montant">Montant : </label>
    <input type="number" id="operation-montant" v-model="kingaku_sosa" required> €
    
    <button type="submit">Ajouter Opération</button>
  </form>
  <ul>
    <li v-for="operation in shujutsu" :key="operation.id">
      {{ operation.description }}
      <span v-if="operation.montant > 0">+{{ operation.montant }} € (Crédit)</span>
      <span v-else>{{ operation.montant }} € (Débit)</span>
      <button @click="supprimerOperation(operation.id)">Effacer</button>
    </li>
  </ul>
</template>

<style scoped>
  h2 {
    color: rgb(14, 141, 42);
    background-color: rgb(31, 19, 70);
  }
  form {
    border: 10px;
    border-radius: 0px 0px 25px 25px;
    background-color: rgb(0, 182, 214);
  }
  button {
    border: 1px solid;
    border-radius: 5px;
    background-color: rgb(80, 94, 87);
    padding: 5px 1em;
    margin: 10px;
    cursor: pointer;
  }
  #solde {
    display: flex;
    align-items: center;
    display: flex;
    justify-content: space-evenly;
  }
</style>
  