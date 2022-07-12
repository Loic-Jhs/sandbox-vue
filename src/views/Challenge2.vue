<template>
  <input type="number" v-model="sum" />
  <br /><br />
  <button @click="addingNumber">Increment</button>
  <button @click="subtractNumber">Decrement</button>
  <button @click="clear">Clear</button>
  <button type="submit" @click="submitForm">Submit</button>
  <div class="resul">
    <h2>added numbers</h2>
    <p id="error-msg"></p>
    <!-- eslint-disable-next-line vue/require-v-for-key -->
    <li v-for="item in items">
      {{ item }}
    </li>
  </div>
</template>

<script>
/**
 * Consigne:
 * 1) input number + bouton d'ajout + bouton de clear + div de la liste. Pas de tri, pas de sécurisation sur les doublons.✅
 * 2) (optionel) ajout de la combobox qui mirror la liste de la div principale
 * 3) ajout du bouton de suppression ✅
 * 4) ajout de la sécurité sur ajout de doublon + affichage d'un message d'erreur dans la zone dédiée ✅
 * 5) ajout de la sécurité sur suppression d'élément absent + affichage du message d'erreur associé
 * 6) intégration du tri par ordre croissant à l'insertion ✅
 * 7) intégration du tri par ordre décroissant, sélection par un booléen hardcodé
 * 8) ajout des boutons radio pour passer d'un tri à l'autre.
 */
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "Challenge2",
  components: {},
  setup() {
    let items = ref([]);
    let sum = ref(0);
    let result = null;

    function addingNumber() {
      sum.value++;
    }

    function subtractNumber() {
      sum.value--;
    }

    function clear() {
      sum.value = 0;
    }

    function submitForm() {
      result = sum.value;
      // Voir comment faire avec la syntaxe VueJS (v-if/v-else)
      let errorMsg = document.getElementById("error-msg");
      if (items.value.includes(result)) {
        errorMsg.innerHTML = "This number already exists !";
      } else {
        items.value.push(result);
        // On trie le tableau pour qu'il soit dans l'ordre croissant
        // la partie (a, b) => a - b permet de faire une comparaison
        // et de trier de la bonne manière 1 & 10
        // https://medium.com/coding-at-dawn/how-to-sort-an-array-numerically-in-javascript-2b22710e3958#:~:text=In%20order%20to%20sort%20a,difference%20between%20the%20two%20numbers
        items.value.sort((a, b) => a - b);
        errorMsg.innerHTML = "";
      }
    }

    return {
      subtractNumber,
      addingNumber,
      submitForm,
      clear,

      items,
      sum,
    };
  },
});
</script>

<style lang="less" scoped>
.challenge2 {
  display: flex;
  justify-content: center;
}
</style>
