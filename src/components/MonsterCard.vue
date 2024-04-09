<script setup>
import {RouterLink} from 'vue-router';

//methode pour passer propriétés qui seront lues par chaque objet de l'API
const props = defineProps({
    name:String,
    image:String,
    id:String
});

</script>
<template>

<div class="d-flex overflow-hidden mb-3 bg-light">
                        <img class="img-fluid" :src="image" style="width: 100px; height: 100px; object-fit: cover;" :alt="name">
                        <RouterLink :to="{name: 'details', params: {id: id}}"><span class="h5 d-flex align-items-center bg-light px-3 mb-0">{{name}}</span></RouterLink>
                        
                    </div>

</template>
<style scoped></style>

