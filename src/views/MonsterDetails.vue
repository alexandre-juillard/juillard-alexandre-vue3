<script setup>
import {ref} from 'vue';
import {useRoute} from 'vue-router'

//stockage url
const route = useRoute();

// ref pour stocker objet selon son id
const monster = ref({});

//methode pour call api d'un seul objet dynamique selon son id
const getOneMonsterById = async (monsterId)=>{
    const url = 'https://metallo.ew.r.appspot.com/monsters/' + monsterId;
    const response = await fetch(url);
    monster.value = await response.json();
    // console.log(monster.value);
}

//appel de la methode avec id de l'objet en parametre
getOneMonsterById(route.params.id)

</script>

<template>

 <!-- About Start -->
 <div class="container-fluid py-5">
        <div class="container">
            <div class="row gx-5">
                <div class="col-lg-5 mb-5 mb-lg-0" style="min-height: 500px;">
                    <div class="position-relative h-100">
                        <img class="position-absolute w-100 h-100 rounded" :src="monster.image" style="object-fit: cover;">
                    </div>
                </div>
                <div class="col-lg-7">
                    <div class="border-start border-5 border-primary ps-5 mb-5">
                        <h6 class="text-primary text-uppercase">{{monster.category}}</h6>
                        <h1 class="display-5 text-uppercase mb-0">{{monster.name}}</h1>
                    </div>
                    <h4 class="text-body mb-4">{{monster.description}}</h4>
                 
                </div>
            </div>
        </div>
    </div>
    <!-- About End -->

</template>
<style scoped></style>

