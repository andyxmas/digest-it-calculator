<template>
  <div class="container p-2">
    <h1 class="text-xl mb-8">Standard Tank Slurry Calculator</h1>

    <div class="flex space-x-2">
      <div>
        <label
          for="length"
          class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4"
        >
          Length
        </label>
        <input
          type="number"
          inputmode="numeric"
          name="length"
          v-model="length"
          class="bg-gray-200 appearance-none border-2 border-gray-200 rounded py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500 w-20"
        />
      </div>
      <div>
        <label
          for="width"
          class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4"
        >
          Width
        </label>
        <input
          type="number"
          inputmode="numeric"
          name="width"
          v-model="width"
          class="bg-gray-200 appearance-none border-2 border-gray-200 rounded py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500 w-20"
        />
      </div>
      <div>
        <label
          for="height"
          class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4"
        >
          Height
        </label>
        <input
          type="number"
          inputmode="numeric"
          name="height"
          v-model="height"
          class="bg-gray-200 appearance-none border-2 border-gray-200 rounded py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500 w-20"
        />
      </div>

    <div>

      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="unit">Unit</label>
      <div class="w-full">
        <input type="radio" value="ft" name="unit" v-model="unit" />
        <label for="ft">Feet</label>
      </div>

      <div class="w-full">
        <input type="radio" value="m" name="unit" v-model="unit" />
        <label for="m">Meters</label>
      </div>

    </div>
    
    </div>

<h2 class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4 mt-8">Slurry volume</h2>
<div class="flex space-x-2">
  

    <p class="w-full"><strong>g</strong>: {{ g | dp }}</p>
    <p class="w-full"><strong>M3</strong>: {{ m3 | dp }}</p>

</div>

<h2 class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4 mt-8">Digest-it required</h2>
<p class="text-xl">{{ required}} </p>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      length: 45,
      width: 45,
      height: 8,
      unit: 'ft',
      per_m_divisor: 22.73,
      ft_to_m: 0.3048
    }
  },
  computed: {
    g: function() {
      if (this.unit == 'm') {
        return (this.length * this.width * this.height) * 219.969
      } else if (this.unit == 'ft') {
        return ( (this.length * this.ft_to_m) * (this.width * this.ft_to_m)  * (this.height * this.ft_to_m) ) * 219.969
      }
    },
    m3: function () {
      return this.g/1000 * 4.5
    },
    required: function () {
      let amount = this.m3 / this.per_m_divisor
      return amount.toFixed(1)
    },
  },
  filters: {
  dp: function (number) {
    return number.toFixed(0)
  }
}
}
</script>

<style></style>
