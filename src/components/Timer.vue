<template>
  <div>
    <div class="timer">
      <span id="minutes">{{ minutes }}</span>
      <span id="middle">:</span>
      <span id="seconds">{{ seconds }}</span>
    </div>

    <div id="buttons">
      <el-button
        v-if="!timer"
        @click="startTimer"
        type="primary"
        icon="el-icon-video-play">
        Start
      </el-button>

      <el-button
        v-if="timer"
        @click="stopTimer"
        type="primary"
        icon="el-icon-video-pause">
        Pause
      </el-button>

      <el-button
        v-if="resetButton"
        @click="resetTimer"
        type="primary"
        icon="el-icon-refresh">
        Reset
      </el-button>
    </div>

    <el-row type="flex" class="row-bg" justify="center">
      <el-col :span="12">
        <el-slider
          @change="onChange( value )"
          @input="onInput( value )"
          v-model="value"
          class="slider">
        </el-slider>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'timer',

  data() {
    return {
      timer: null,
      totalTime: ( 25 * 60 ),
      resetButton: false,
      value: 0,
      lastNum: 0
    };
  },

  computed: {
    minutes() {
      const minutes = Math.floor( this.totalTime / 60 );
    
      return this.padTime( minutes );
    },

    seconds() {
      const seconds = this.totalTime - ( this.minutes * 60 );
      
      return this.padTime( seconds ); 
    }
  },

  mounted() {
    this.startTimer();
  },

  methods: {
    startTimer() {
      this.timer = setInterval( () => this.countdown(), 1000 );
      this.resetButton = true;
    },
    
    stopTimer() {
      clearInterval( this.timer );
      this.timer = null;
      this.resetButton = true;
    },
    
    resetTimer() {
      this.totalTime = ( 25 * 60 );
      clearInterval( this.timer );
      this.timer = null;
      this.resetButton = false;

      this.value = 0;
    },
    
    padTime( time ) {
      return ( time < 10 ? '0' : '' ) + time;
    },
    
    countdown() {
      if( this.totalTime >= 1 ) {
        this.totalTime--;
      } else {
        this.totalTime = 0;
        this.resetTimer();
      }
    },

    onChange( value ) {
      this.totalTime = ( parseInt( this.minutes ) + value ) * 60;
    },

    onInput( value ) {
      if ( this.lastNum < value ) {
        this.totalTime = ( parseInt( this.minutes ) + value ) * 60;
      } else {
        this.totalTime = ( parseInt( this.minutes ) - value ) * 60;
      }
      
      this.lastNum = value;
    }
  }
}
</script>

<style lang="scss">
  .timer {
    font-size: 200px;
    line-height: 1;
    margin-bottom: 40px;
  }

  .slider {
    margin-top: 2rem
  }
</style>