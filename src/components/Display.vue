<template>
  <div class="grid md:grid-cols-2 gap-4">
    <div class="shadow-md bg-indigo-300 p-10 text-center rounded">
      <h3 class="text-3xl text-indigo-900 font-bold mb-4">Cases</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Active:</span>
        {{commas(stats.NewConfirmed)}}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{commas(stats.TotalConfirmed)}}
      </div>
    </div>
    <div class="shadow-md bg-indigo-500 p-10 text-center rounded">
      <h3 class="text-3xl text-indigo-900 font-bold mb-4">Deaths</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{commas(stats.NewDeaths)}}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{commas(stats.TotalDeaths)}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Display',
  props: ['stats'],
  methods: {
    commas(x){
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
    }
  }
}
</script>

<style>

</style>