<template>
  <div class="container p-2">
    <h1 class="mb-4 text-green-400 text-lg font-bold">Digest-it Calculator</h1>

    <ul class="flex border-b mb-2">
      <li :class="{'-mb-px': tab == 'standard'}" class="mr-1">
        <a :class="{'border-l border-t border-r rounded-t  text-blue-700': tab == 'standard'}" class="bg-white inline-block py-2 px-4 text-blue-500 font-semibold" href="#" @click="setTab('standard')">Standard</a>
      </li>
      <li :class="{'-mb-px': tab == 'circular'}" class="mr-1">
        <a :class="{'border-l border-t border-r rounded-t': tab == 'circular'}" class="bg-white inline-block py-2 px-4 text-blue-500 hover:text-blue-800 font-semibold" href="#" @click="setTab('circular')">Circular</a>
      </li>
      <li :class="{'-mb-px': tab == 'herd'}" class="mr-1">
        <a :class="{'border-l border-t border-r rounded-t': tab == 'herd'}" class="bg-white inline-block py-2 px-4 text-blue-500 hover:text-blue-800 font-semibold" href="#" @click="setTab('herd')">Herd</a>
      </li>
    </ul>



    <div v-if="tab != 'herd'">
      <div class="flex space-x-2">
        <div v-if="tab == 'standard'">
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
        <div v-if="tab == 'standard'">
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
        <div v-if="tab == 'circular'">
          <label
            for="diameter"
            class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4"
          >
            Diameter
          </label>
          <input
            type="number"
            inputmode="numeric"
            name="diameter"
            v-model="diameter"
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


<h2 class="block text-gray-500 font-bold mb-1 pr-4 mt-8">Slurry volume</h2>
<div class="flex space-x-2">
  

    <p class="w-full"><strong>Gallons</strong> {{ gallons| dp }}</p>
    <p class="w-full"><strong>M<sup>3</sup></strong> {{ m3 | dp }}</p>

</div>

<h2 class="block text-gray-500 font-bold mb-1 pr-4 mt-8">Digest-it required</h2>
<p class="text-xl">{{ required}} </p>
  </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      tab: 'standard',
      length: 45,
      width: 45,
      height: 8,
      diameter: 10,
      unit: 'ft',
      per_m_divisor: 22.73,
      ft_to_m: 0.3048
    }
  },
  methods: {
    setTab: function(tab) {
      this.tab = tab
    }
  },
  computed: {
    gallons: function() {
      if(this.tab == 'standard') {
        if (this.unit == 'm') {
          return (this.length * this.width * this.height) * 219.969
        } else if (this.unit == 'ft') {
          return ( (this.length * this.ft_to_m) * (this.width * this.ft_to_m)  * (this.height * this.ft_to_m) ) * 219.969
        }
      }
      else if(this.tab='circular') {
        return this.m3 * 219.9692
      }

    },
    m3: function () {
      if(this.tab == 'standard') {
        return this.gallons/1000 * 4.5
      } else if(this.tab='circular') {
        // =IF(M18="m",(((3.14159265359*(E18/2)^2)*I18)),((((E18/2)*0.3048)^2)*3.14159265359)*(I18*0.3048))
        if (this.unit == 'm') {
          return 3.14159265359 * ((this.diameter / 2) **2) * this.height
        }
        else if(this.unit == 'ft') {
          return 3.14159265359 * ((this.diameter / 2 * 0.3048) **2) * (this.height * 0.3048)
        }

      }
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

<style>

.container {
  max-width: 360px;
  margin: 0 auto;
  min-height: 100vh;
}
</style>
