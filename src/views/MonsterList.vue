<script setup>
//decoupage en cards individuelles
import MonsterCard from "../components/MonsterCard.vue";

import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

//ref pour la pagination
const currentPage = ref(1);
const totalPages = ref(2);
const limit = ref(40);

//ref pour stocker tableau d'objet de l'API
const monsters = ref([]);

//methode pour call API
const getAllMonsters = async () => {
  const response = await fetch(
    `https://metallo.ew.r.appspot.com/monsters?page=${currentPage.value}&limit={limit.value}`
  );
  monsters.value = await response.json();
  // console.log(monsters.value);
  router.push({ query: { page: currentPage.value } });
};

getAllMonsters();

// Fonction pour passer à la page précédente
const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
    getAllMonsters(); // Récupérer les données de la nouvelle page
  }
};

// Fonction pour passer à la page suivante
const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
    getAllMonsters(); // Récupérer les données de la nouvelle page
  }
};
</script>
<template>
  <!-- Blog Start -->
  <div class="container py-5">
    <div class="row">
      <!-- Monster list Start -->
      <div class="col">
        <div class="mb-5">
          <h3
            class="text-uppercase border-start border-5 border-primary ps-3 mb-4"
          >
            Every Monsters
          </h3>

          <MonsterCard
            v-for="monster in monsters"
            :key="monster._id"
            :id="monster._id"
            :name="monster.name"
            :image="monster.image"
          />
        </div>
      </div>
      <!-- Monster list End -->

      <!-- Pagination -->
      <div class="d-flex justify-content-around">
        <button
          @click="prevPage"
          :disabled="currentPage === 1"
          class="btn btn-secondary"
        >
          Previous
        </button>
        <span>{{ currentPage }} / {{ totalPages }}</span>
        <button
          @click="nextPage"
          :disabled="currentPage === totalPages"
          class="btn btn-secondary"
        >
          Next
        </button>
      </div>
    </div>
  </div>
  <!-- Blog End -->
</template>
<style scoped></style>
