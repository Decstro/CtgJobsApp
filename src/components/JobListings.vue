<script setup>
import { RouterLink } from 'vue-router';
import JobListing from './JobListing.vue';
import LateralModal from './LateralModal.vue';
import { reactive, onMounted, ref } from 'vue';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
import axios from 'axios';

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});

const state = reactive({
  jobs: [],
  isLoading: true,
});

const isModalOpen = ref(false);

const openModal = () => {
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

onMounted(async () => {
  try {
    const response = await axios.get('/api/jobs');
    state.jobs = response.data;
  } catch (error) {
    console.error('Error fetching jobs', error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <section class="bg-indigo-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-indigo-700 mb-6 text-center">
        Browse Jobs
      </h2>
      <!-- Show loading spinner while loading is true -->
      <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
        <PulseLoader />
      </div>

      <!-- Shoe job listing when done loading -->
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing
          v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>

  <section v-if="showButton" class="m-auto max-w-4xl my-10 px-6">
    <div class="flex gap-4 flex-col sm:flex-row">
      <RouterLink
        to="/jobs"
        class="flex-1 bg-indigo-950 text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700 transition-colors"
        >View All Jobs</RouterLink
      >
      <button
        @click="openModal"
        class="flex-1 bg-[#5C0CB8] text-white text-center py-4 px-6 rounded-xl hover:bg-[#4A0A96] transition-colors font-medium"
      >
        Action Items
      </button>
    </div>
  </section>

  <!-- Lateral Modal -->
  <LateralModal :isOpen="isModalOpen" @close="closeModal" />
</template>
