<template>
  <div class="w-full sm:w-1/2 m-auto text-white">
    <h1 class="text-4xl text-center mt-4">Weight Converter</h1>

    <div class="mx-8 mt-16">
      <label for="units" class="block">
        Select Weight Input Unit
      </label>

      <div class="relative mt-3">
        <select name="units" v-model="unit" id="units" class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500">
          <option>-----</option>
          <option value="pounds">Pounds</option>
          <option value="kilograms">Kilograms</option>
          <option value="grams">Grams</option>
          <option value="ounces">Ounces</option>
        </select>

        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
            <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
        </div>
      </div>

      <div>
        <input type="number" v-model="number" name="number" id="" placeholder="Enter Figure" class="block appearance-none bg-gray-100 border border-gray-200 py-3 px-4 pr-8 rounded w-full mt-4 text-gray-700">
      </div>

      <div class="my-4">
        <!-- Use v-show to toggle hide or show -->
        <div id="pounds" v-show="unit === 'pounds' ? false : true" class="bg-gray-900 px-6 py-8 rounded-lg mt-2">
          <h4 class="font-bold text-2xl">Pounds</h4>
          <div class="text-xl">{{ converted.pounds }}</div>
        </div>

        <div id="kilograms" v-show="unit === 'kilograms' ? false : true" class="bg-green-700 px-6 py-8 rounded-lg mt-2">
          <h4 class="font-bold text-2xl">Kilograms</h4>
          <div class="text-xl">{{ converted.kilograms }}</div>
        </div>

        <div id="grams" v-show="unit === 'grams' ? false : true" class="bg-blue-700 px-6 py-8 rounded-lg mt-2">
          <h4 class="font-bold text-2xl">Grams</h4>
          <div class="text-xl">{{ converted.grams }}</div>
        </div>

        <div id="ounces" v-show="unit === 'ounces' ? false : true" class="bg-red-700 px-6 py-8 rounded-lg mt-2">
          <h4 class="font-bold text-2xl">Ounces</h4>
          <div class="text-xl">{{ converted.ounces }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Converter',
  data() {
    return {
      unit: '-----',
      number: 0,
      converted: {
        pounds: 0,
        kilograms: 0,
        grams: 0,
        ounces: 0
      }
    }
  },
  watch: {
    number() {
      this.calculate(this.unit, this.number)
    }
  },
  methods: {
    calculate(unit, number) {
      let kilograms;
      let grams;
      let ounces;
      let pounds;

      if (unit === 'pounds') {
          kilograms = number / 2.2046
          grams = number / 0.0022046
          ounces = number * 16

          this.converted.kilograms = kilograms
          this.converted.grams = grams
          this.converted.ounces = ounces

      } else if (unit === 'grams') {
          kilograms = number / 1000
          ounces = number / 28.35
          pounds = number / 454

          this.converted.kilograms = kilograms
          this.converted.ounces = ounces
          this.converted.pounds = pounds

      } else if (unit === 'ounces') {
          kilograms = number / 35.274
          grams = number * 28.35
          pounds = number / 16

          this.converted.kilograms = kilograms
          this.converted.grams = grams
          this.converted.pounds = pounds

      } else if (unit === 'kilograms') {
          grams = number * 1000
          ounces = number * 35.274
          pounds = number * 2.2046

          this.converted.grams = grams
          this.converted.ounces = ounces
          this.converted.pounds = pounds
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
