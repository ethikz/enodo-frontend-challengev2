<template>
  <div>
    <h2>Tempature Converter</h2>
    <el-alert type="info">
      Celsius to Fahrenheit (And back again) <strong>C = (F - 32) * (5/9)</strong> // <strong>F = C * (9/5) + 32</strong>
    </el-alert>
    <p>
      The formula for converting a temperature from celsius to fahrenheit is <strong>C = (F - 32) * (5/9)</strong> and the reverse is <strong>F = C * (9/5) + 32.</strong>
    </p>

    <div>
      <label for="celsius">Celsius</label>
      <el-input
        id="celsius"
        :placeholder="c"
        v-model="c"
        @change="convertC()"
        @input="convertC()"
        type="number">
      </el-input>
    </div>
    
    <div>
      <label for="fahrenheit">Fahrenheit</label>
      <el-input
        id="fahrenheit"
        :placeholder="f"
        v-model="f"
        @change="convertF()"
        @input="convertF()"
        type="number">
      </el-input>
    </div>
  </div>
</template>

<script>
export default {
  name: 'tempature-converter',

  data() {
    return {
      c: 0,
      f: 0
    }
  },

  methods: {
    convertC() {
      this.f = Math.round( ( this.c * 9 / 5 ) + 32 );
    },

    convertF() {
      this.c = Math.round( ( this.f - 32 ) * 5 / 9 );
    }
  }
}
</script>

<style>
</style>