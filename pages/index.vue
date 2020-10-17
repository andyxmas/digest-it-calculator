<template>
<div class="container p-4">

  <h1 class="text-xl mb-8">How much digest-it do I need?</h1>

  <div class="flex space-x-4">
    <div>
      <label for="cows" class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4">
        Cows 
      </label>
      <input type="number" 
        inputmode="numeric"
        name="cows"
        v-model="cows"
        class="bg-gray-200 appearance-none border-2 border-gray-200 rounded py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500 w-24"
      />
    </div>
    <div>
      <label for="calves" class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4">
        Calves 
      </label>
      <input type="number" 
        inputmode="numeric"
        name="calves"
        v-model="calves"
        class="bg-gray-200 appearance-none border-2 border-gray-200 rounded py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500 w-24"
        />
    </div>

    <div>
      <label for="required" class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4">
          Digest-it required
      </label>
      <input type="text"
      readonly 
        name="required"
        v-model="required"
        class="bg-blue-200 appearance-none border-2 border-blue-200 rounded py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500 w-24"
        />
    </div>
  </div>
</div>
</template>

<script>
export default {
  data: function() {
    return {
      cows: 0,
      calves: 0,
      cows_multiplier: 0.1,
      calves_multiplier: 0.05
    }
  },
  computed: {
    required: function() {
      let amount = this.cows * this.cows_multiplier + this.calves * this.calves_multiplier
      return Math.ceil(amount)
    }
  }
}
</script>

<style>
</style>
