<template>
  <div class="container mx-auto p-4 flex justify-center items-center min-h-screen">
    <div class="grid grid-cols-4 gap-4" style="border: 1px solid gray; border-radius: 20px;">
      <div class="event-card rounded overflow-hidden shadow-lg mx-auto">
        <img class="object-cover w-full h-24" style="width: 100%; border-radius: 10px" :src="imageSrc" alt="Event image">
      </div>
      <div class="px-2 py-1 text-center">
        <div class="font-bold text-sm mb-1">{{ event.title }}</div>
        <p class="text-gray-700 text-xs">{{ formatEventDate(event.start, event.end) }}</p>
      </div>
      <div class="px-2 pt-1 pb-1 flex justify-center">
        <button class="bg-teal-500 text-white py-1 px-2 rounded text-xs" style="margin: 5px; border: none; cursor: pointer;">
          View
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    event: {
      type: Object,
      required: true
    }
  },
  computed: {
    imageSrc() {
      return require(`@/assets/${this.event.image}`);
    }
  },
  methods: {
    formatEventDate(start, end) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      const startDate = new Date(start).toLocaleDateString(undefined, options);
      const endDate = new Date(end).toLocaleDateString(undefined, options);
      return `${startDate} - ${endDate}`;
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 16vw;
}

.event-card {
  flex: 1;
  margin: 4px;
  text-align: center;
  padding: 8px;
}

.bg-teal-500 {
  background-color: #34cc98;
}

.text-white {
  color: #ffffff;
}

.font-bold {
  font-weight: bold;
}

.py-1 {
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
}

.px-2 {
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}

.rounded {
  border-radius: 0.25rem;
}

.text-xs {
  font-size: 1rem;
}
</style>
