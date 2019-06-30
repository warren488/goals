<template>
  <div class="task">
    <header>
      <h1>{{name}}</h1>
    </header>
    <div class="data">
      <ul>
        <li>todo: {{format(todo)}}</li>
        <li>done: {{format(done)}}</li>
        <li>left: {{format(left, 'left')}}</li>
        <li></li>
      </ul>
      <button @click="start">start</button>
      <button @click="stop">stop</button>
    </div>
    <div class="progress">
      <div :style="{ width: percleft + '%'}" class="state"></div>
    </div>
  </div>
</template>
<script lang="ts">
import Vue from "vue";
import moment from "moment";
export default Vue.extend({
  data() {
    return {
      name: "TaskName",
      done: 0,
      todo: 1000 * 60 * 60,
      int: null
    };
  },
  methods: {
    moment,
    start() {
      this.int = setInterval(() => {
        this.done += 50;
      }, 50);
    },
    stop() {
      clearInterval(this.int);
    },
    format(time, type) {
      let minutes, remainder, seconds;
      if (type && type === "left") {
        //   the remainder will be the seconds
        remainder = (time / 1000) % 60;
        seconds = Math.ceil(remainder);
      } else {
        //   the remainder will be the seconds
        remainder = (time / 1000) % 60;
        seconds = Math.floor(remainder);
      }
      minutes = Math.floor(time / 1000 / 60);
      return `${minutes}:${seconds}`;
    }
  },
  computed: {
    left() {
      return this.todo - this.done;
    },
    percleft() {
      return ((this.done / this.todo) * 100) % 100;
    }
    // formatted() {}
  }
});
</script>

<style lang="scss" scoped>
.task {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.data {
  width: 40%;
  //   justify-content: center;
  li {
    display: flex;
    padding: 10px;
    background-color: lightgray;
    margin: 10px;
    border-radius: 5px;
  }
}

.progress {
  width: 100%;
}
.state {
  transition: all ease-in-out 0.1s;
  background-color: aqua;
  height: 10px;
  border-radius: 5px;
}
</style>
