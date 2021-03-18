<template>
  <div class="home">
    <button class="button1" @click="start">START 1</button>
    <button class="button2" @click="stop">STOP 1</button>
    <span>单层效果</span>
    <div id="wallpager"></div>
  </div>
</template>

<script>
export default {
  name: "Home",
  beforeRouteLeave(to, from, next) {
    console.log("beforeRouteLeave");
    this.stop();
    next();
  },
  data() {
    return {
      index_0: -1,
      index_1: -1,
      timehander: {},
      timeOut: 3 * 1000,
      sliders: [
        require("../res/000.jpg"),
        require("../res/001.jpg"),
        require("../res/002.jpg"),
        require("../res/003.jpg"),
      ],
    };
  },

  components: {},
  methods: {
    start() {
      console.log("start");
      this.updateBg();
      this.timehander = setInterval(() => {
        this.updateBg();
      }, this.timeOut);
    },
    stop() {
      console.log("stop");
      clearTimeout(this.timehander);
    },
    updateIndex() {
      if (this.index_0 == -1) {
        this.index_0 = 0;
      } else {
        this.index_0 = this.index_1;
      }
      this.index_1 = (this.index_0 + 1) % this.sliders.length;
      console.log("index_0 : " + this.index_0 + ", index_1 : " + this.index_1);
    },
    setBg() {
      console.log("setbg : " + this.sliders[this.index_0]);
      let e = document.getElementById("wallpager");
      e.setAttribute(
        "style",
        "background: center / cover url(" +
          this.sliders[this.index_0] +
          ") fixed no-repeat;"
      );
    },
    updateBg() {
      console.log("updateBg");
      this.updateIndex();
      this.setBg();
    },
  },
};
</script>

<style scoped>
span{
  position: absolute;
  left: 50%;
  top: 50%;
  font-size: 40px;
  color: red;
  z-index: 100;
}
.button1 {
  left: 20%;
  position: absolute;
  margin: auto 5px;
  z-index: 100;
}
.button2 {
  left: 30%;
  position: absolute;
  margin: auto 5px;
  z-index: 100;
}

.home {
  width: 100%;
  height: 100%;
  position: fixed;
  overflow: hidden;
  background: center / cover url(../res/bg.jpg) fixed no-repeat;
  color: #fff;
}

#wallpager {
  height: 100%;
  width: 100%;
  position: fixed;
  overflow: hidden;
  color: #fff;
  transition: all 1s linear;
}
</style>
