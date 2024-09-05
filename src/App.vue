<template>
  <div class="container mx-auto py-4" style="padding: 60px 90px 60px 90px;">
    <div v-if="loading" class="text-center text-gray-500">Loading events...</div>
    <div v-else class="event-grid">
      <EventCard
        v-for="event in paginatedEvents"
        :key="event.id"
        :event="event"
      />
    </div>
    <div class="flex justify-center mt-4" style="padding: 20px;">
      <button
        @click="prevPage"
        :disabled="currentPage === 1"
        class="bg-gray-300 text-gray-700 py-2 px-4 rounded mr-2"
      >
        Previous
      </button>
      <button
        @click="nextPage"
        :disabled="currentPage === totalPages"
        class="bg-gray-300 text-gray-700 py-2 px-4 rounded"
      >
        Next
      </button>
    </div>
  </div>
</template>

<script>
import EventCard from './components/EventCard.vue';
import eventData from './assets/events-data.json';

export default {
  name: 'App',
  components: {
    EventCard
  },
  data() {
    return {
      events: [],
      loading: true,
      currentPage: 1,
      pageSize: 8
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.events.length / this.pageSize);
    },
    paginatedEvents() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.events.slice(start, end);
    }
  },
  methods: {
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    }
  },
  mounted() {
    // Simulate a delay to show the loading state
    setTimeout(() => {
      this.events = eventData;
      this.loading = false;
    }, 1000);
  }
}
</script>

<style>
.container {
  text-align: center;
  overflow: hidden;
}

.event-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 4px;
  justify-content: center;
  padding: 4px;
}

@media (max-width: 1024px) {
  .event-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 768px) {
  .event-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 540px) {
  .event-grid {
    grid-template-columns: 1fr;
  }
}
</style>
