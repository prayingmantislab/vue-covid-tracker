<template>
  <main v-if="!Loading"><DataTitle :text="title" :dataDate="dataDate" /></main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-grey-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" class="width-24 m-auto" alt="" />
  </main>
</template>
<script>
// @ is an alias to /src
import DataTitle from '@/components/DataTitle.vue';
export default {
  name: 'Home',
  components: {
    DataTitle,
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif'),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    debugger;
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
