<script>
import { onMounted, ref } from 'vue';
import axios from 'axios';
import PublicationCard from '@/domains/statisticsManagement/entrepreneur/components/publication-card.component.vue';
import { Publication } from '@/domains/statisticsManagement/entrepreneur/models/Publication.entity.js';
import { EntrepreneurProfile } from '@/domains/statisticsManagement/entrepreneur/models/Publication.entity.js';

export default {
  name: "statistics.component",
}

const publications = ref([])

const fetchPublications = async () => {
  try {
    // 1. Obtener perfil para conseguir el ID
    const profileResponse = await axios.get('/api/v1/profiles/entrepreneur');
    const profile = new EntrepreneurProfile(profileResponse.data[0]);

    // 2. Obtener publicaciones por rating
    const pubResponse = await axios.get(`/api/v1/publication/order-by-rating/${profile.id}`);
    publications.value = pubResponse.data.map(pub => new Publication(pub));
  } catch (error) {
    console.error('Error al obtener publicaciones:', error);
  }
}
onMounted(() => {
  fetchPublications();
});

</script>

<template>
  <div class="statistics-view">
    <h2>Estadísticas</h2>
    <div class="filter">
      <button>Mis publicaciones ⌄</button>
    </div>
    <div class="card-grid">
      <PublicationCard
          v-for="publication in publications"
          :key="publication.id"
          :publication="publication"
      />
    </div>
  </div>
</template>

<style scoped>
.statistics-view {
  padding: 2rem;
  background-color: #fff;
  min-height: 100vh;
}

h2 {
  text-align: center;
  color: #a57c52;
  margin-bottom: 1.5rem;
}

.filter {
  text-align: right;
  margin-bottom: 1rem;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}
</style>