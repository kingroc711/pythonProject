<template>
  <div class="home">
    <button class="button1" @click="start">START 0</button>
    <button class="button2" @click="stop">STOP 0</button>
    <span>双层效果</span>
    <div id="wallpager_down">
      <div id="wallpager_up"></div>
    </div>
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
      opttimehander: {},
      optTime: 10,
      timeOut: 3 * 1000,
      optTimeOut: 100,
      sliders: [
        require("../res/000.jpg"),
        require("../res/001.jpg"),
        require("../res/002.jpg"),
        require("../res/003.jpg"),
      ],
    };
  },
  methods: {
    fetchData() {
      console.log("aaaaaaaa");
    },
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
      clearTimeout(this.opttimehander);
    },
    setOpacity() {
      console.log("optTime : " + this.optTime);
      if (this.optTime > 0) {
        this.optTime--;
        let e = document.getElementById("wallpager_up");
        e.style.opacity = 0.1 * this.optTime;
      } else {
        clearTimeout(this.opttimehander);
        this.optTime = 10;
        this.setBg();
        this.unsetOpacity();
      }
    },
    unsetOpacity() {
      let e = document.getElementById("wallpager_up");
      e.style.opacity = 1;
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
      this.updateIndex();
      let e = document.getElementById("wallpager_up");
      e.setAttribute(
        "style",
        "background: center / cover url(" +
          this.sliders[this.index_0] +
          ") fixed no-repeat;"
      );

      e = document.getElementById("wallpager_down");
      e.setAttribute(
        "style",
        "background: center / cover url(" +
          this.sliders[this.index_1] +
          ") fixed no-repeat;"
      );
    },
    updateBg() {
      console.log("updateBg");
      if (this.index_0 == -1) {
        this.setBg();
      } else {
        this.opttimehander = setInterval(this.setOpacity, this.optTimeOut);
      }
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
  z-index: 100;
  color: red;
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

#wallpager_down {
  height: 100%;
  width: 100%;
  position: fixed;
  overflow: hidden;
  color: #fff;
}

#wallpager_up {
  height: 100%;
  width: 100%;
  position: fixed;
  overflow: hidden;
  color: #fff;
}
</style>
