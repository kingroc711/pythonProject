<template>
  <div id="app">
    <div class="box">
      <span>多张图片切换显示 ： </span>

      <router-link class="router" to="/doublelay">
        <button >效果好消耗高</button>
      </router-link>

      <router-link class="router" to="/onelay">
        <button>效果差消耗低</button>
      </router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.box{
  margin: 1px;
}

.router{
  margin: auto 10px;
}

</style>
