<template>
  <main v-if="!loading">
    <DataInfo 
    :text="title" 
    :fetchDate="fetchDate" />

    <CountryData 
    @getCountry="fetchCountry" 
    :countries="countries" />
    
    <button 
    v-if="stats.Country" 
    @click="clear"
    class="bg-indigo-300 text-white rounded p-3 mb-10 focus:outline-none hover:bg-indigo-400">Clear Selection</button>
    
    <Display :stats="stats"/>
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-800 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
  </main>
</template>

<script>
import DataInfo from '@/components/DataInfo'
import Display from '@/components/Display'
import CountryData from '@/components/CountryData'

export default {
  name: 'Home',
  components: {
    DataInfo,
    Display,
    CountryData
  },
  data() {
    return {
      loading: true,
      title: 'Global Case',
      fetchDate: '',
      stats: {},
      countries: [],
      // loading
    }
  },
  methods: {
    async fetchData() {
      const response = await fetch('https://api.covid19api.com/summary')
      const data = await response.json()
      return data
    },
    fetchCountry(country) {
      this.stats = country
      this.title = country.Country
    },
    async clear() {
      this.loading = true
      const data = await this.fetchData()
      this.title = 'Global Case'
      this.stats = data.Global
      this.loading= false
    }
  },
  async created() {
    const data = await this.fetchData()
    this.fetchDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  }
}
</script>
