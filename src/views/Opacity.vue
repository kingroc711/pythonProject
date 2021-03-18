<template>
  <div class="home">
    <button class="button1" @click="start">START</button>
    <button class="button2" @click="stop">STOP</button>
    <div id="wallpager_down">
      <div id="wallpager_up"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
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
    setOpacity() {
      let e = document.getElementById("wallpager_up");
      e.style.opacity = 0;
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
      this.setOpacity();
      this.updateIndex();
      this.setBg();
      this.unsetOpacity();
    },
  },
};
</script>

<style scoped>
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
  transition: all 1s linear;
}
</style>
