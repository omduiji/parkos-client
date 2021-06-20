<template>
  <div class="container mx-auto px-3">
    <h1 class="text-8xl text-blue-700 my-8">Shiphol NL Parking</h1>
    <form>
      <fieldset
        class=" flex justify-between	items-center border border-gray-900 px-5 py-2"
      >
        <legend>Find Parkings</legend>
        <div class="flex flex-col">
          <label for="start-date">From</label>
          <input
            type="date"
            v-model="startDate"
            name="start-date"
            class="p-2 border border-gray-900"
          />
        </div>
        <div class="flex flex-col">
          <label for="start-date">To</label>
          <input
            type="date"
            v-model="endDate"
            name="end-date"
            class="p-2 border border-gray-900"
          />
        </div>
        <button
          @click.prevent="search"
          class="border rounded-full	border-blue-700 text-base w-35 py-2 px-2 bg-blue-700 text-gray-100 shadow-md	hover:bg-blue-900 transition delay-200	ease-in	hover:border-blue-900 focus:outline-none disabled:opacity-50"
        >
          Search Parkings
        </button>
      </fieldset>
    </form>
    <article
      class="flex justify-between	items-center border border-blue-50 px-4 py-2 my-4 bg-blue-700 shadow rounded-3xl text-gray-50"
      v-for="(slot, index) in Slots"
      :key="index"
    >
      <h2>{{ slot.name.toUpperCase() }}</h2>
      <span>{{ slot.data.currency }} {{ slot.data.price }}</span>
    </article>
  </div>
</template>
<script>
export default {
  data() {
    return {
      startDate: "",
      endDate: "",
      Slots: []
    };
  },
  methods: {
    async search() {
      let queries = new URLSearchParams();
      queries.append("location", "parkeren-schiphol");
      queries.append("arrival", this.startDate);
      queries.append("arrivalTime", "12%3A00");
      queries.append("departure", this.endDate);
      queries.append("departureTime", "12%3A00");
      queries.append("sort_f", "price");
      queries.append("sort_w", "asc");

      let url = new URL(`http://localhost:8080/`);
      url.search = queries;
      let res = await fetch(url);
      let finalRes = await res.json();
      let availableParkings = [];

      this.Slots = Object.entries(finalRes.available).map(item => {
        return {
          name: item[0],
          data: item[1]
        };
      });
    }
  }
};
</script>
<style scoped></style>
