<script setup>
const pokemon = defineProps
([ "name", "xp", "height", "weight", "img", "loading", "type", "moves" ])

</script>

<template>
    <div 
    class="card selected-card"
    :class="loading ? '' : 'animate__animated animate__fadeInRight'"
    >
        <img 
        v-if="pokemon.name"
        :src="pokemon.img" 
        class="card-img-top pt-2"
        :alt="pokemon.name"
        >
        <img 
        v-else
        src="../assets/poke-favicon.png"
        class="card-img-top pt-2"
        alt="???"
        >

        <div class="card-body">
            <h5 class="card-title text-center">{{ pokemon.name || '???' }}</h5>
            <hr>
            <div class="row text-center">
                <section class="col">
                    <strong>Peso: </strong>
                    <span>{{ pokemon.weight }}</span>
                </section>
                <section class="col">
                    <strong>Altura: </strong>
                    <span>{{ pokemon.height }}</span>
                </section>
            </div>
            <div class="row text-center">
                <section class="col">
                    <strong>XP: </strong>
                    <span>{{ pokemon.xp }}</span>
                </section>
                <section class="col">
                    <strong>Tipo: </strong>
                    <span>{{ pokemon.type }}</span>
                </section>
            </div>
            <div class="row text-center">
                <section class="col">
                    <strong>Ataques: </strong>
                    <span>{{ pokemon.moves }}</span>
                </section>
            </div>
        </div>
    </div>
</template>


<style scoped>

.selected-card{
    height: 75vh;
    background: linear-gradient(126deg, rgba(2,0,36,1) 0%, rgba(236,0,0,1) 45%, rgba(255,235,0,1) 100%);
    border: 2px solid black;
}
.selected-card img{
    height: 250px;
}

.card-body {
    color: #dfdfdf;
}

div img {
    width: 50%;
    margin: auto;
}

@media (max-width: 768px) {
    .selected-card {
        height: 30vh;
        width: 80%;
        margin: 0 auto 10px auto;
    }
    .selected-card img{
        height: 100px;
    }
}
</style>