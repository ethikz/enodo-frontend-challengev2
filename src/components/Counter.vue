<template>
  <div>
    <h2>Counter</h2>
    <p>Build a component containing a label or read-only input and a button. The initial value of the label/input should be `0` and every button click should increase that value by `1`</p>

    <h2 class="title">
      {{ counter }}
    </h2>

    <!-- Here I could have used the el-input-number component but decided to do a custom one for sake of the exercise -->
    
    <el-button @click="decrementCounter">
      Count Down
    </el-button>
    
    <el-button @click="incrementCounter">
      Count Up
    </el-button>
  </div>
</template>

<script>
export default {
  name: 'counter',

  data() {
    return {
      counter: 0,
      num: 1
    }
  },

  methods: {
    handleChange( value ) {
      console.log( value );
    },

    incrementCounter() {
      this.counter++;
    },

    decrementCounter() {
      this.counter--;
    }
  }
}
</script>

<style lang="scss">
  form {
    margin: 2em auto;
  }
  
  input {
    margin-left: 1em;
    border: 0;
  }
</style>