<script>
export default {
  name: "PublicationCard",
  props:{
    id: number,
    entrepreneurId: number,
    nameActivity: string,
    description: string,
    timeDuration: string,
    image: string,
    cantPeople: string,
    cost: string,
    averageRating: string
  }
}

</script>

<template>
  <div class="card">
    <img :src="publication.image" alt="Imagen de publicación" class="card-img" />
    <h3>{{ publication.nameActivity }}</h3>
    <p>{{ publication.description }}</p>
    <p><strong>Duración:</strong> {{ publication.timeDuration }} hrs</p>
    <p><strong>Capacidad:</strong> {{ publication.cantPeople }} personas</p>
    <p><strong>Precio:</strong> S/. {{ publication.cost }}</p>
    <p><strong>Rating:</strong> ⭐ {{ publication.averageRating }}</p>
  </div>
</template>

<style scoped>
.card {
  border: 1px solid #d9c4aa;
  border-radius: 10px;
  padding: 1rem;
  background-color: #f9e0b5;
  width: 100%;
}

.card-img {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 1rem;
}
</style>