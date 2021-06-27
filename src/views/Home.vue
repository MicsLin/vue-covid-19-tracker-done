<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelect @get_country="getCountryData" :countries="countries" />

    <!-- v-if 一開始不存在 選了國家才存在 -->
    <button v-if="stats.Country" @click="clearCountryData" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">Clear Country</button>
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" alt="" class="w-24 m-auto" />
  </main>
</template>

<script>
import DataTitle from '../components/DataTitle.vue'
import DataBoxes from '../components/DataBoxes.vue'
import CountrySelect from '../components/CountrySelect.vue'

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data(){
    return{
      loading:true,
      title:'Global',
      dataDate:'',
      stats:{},
      countries:[],
      loadingImage:require('../assets/loadingImage.gif'),
    }
  },
  methods:{
    // 呼叫才會運行的函式
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    },
    getCountryData(country){
      this.stats = country;
      this.title = country.Country;
    },
    // 清除
    async clearCountryData(){
      this.loading =true;
      const data = await this.fetchCovidData();
      this.title ='Global';
      this.stats = data.Global;
      this.loading =false;
    }
  },
  // 進入Home頁面就會運行的函式
  async created(){
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  }
  
}
</script>
