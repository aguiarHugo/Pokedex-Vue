<script setup>
const pokemon = defineProps(["name", "baseSvgUrl"])

</script>

<template>
    <div class="col-4 col-md-6 col-xl-3">
        <div class="card p-2 mb-3 card-list">
            <img 
            :src="baseSvgUrl" class="card-img-top mt-2" 
            alt="..."
            height="80"
            />
            <p class="text-center">{{ pokemon.name }}</p>
        </div>
    </div>
</template>

<style scoped>
.card-list {
    background: linear-gradient(126deg, rgba(2,0,36,1) 0%, rgba(236,0,0,1) 45%, rgba(255,235,0,1) 100%);
    border: 2px solid black;
    transition: .4s;
}

.card-list:hover{
    transform: scale(1.1);
}

.card-list p {
    font-weight: bold;
    color: #DFDFDF;
}

@media (max-width: 768px) {
    .card-list {
        max-height: 140px;
        font-size: 14px;
    }
}

</style>