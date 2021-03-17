<template>
  <div class="home">
    <div id="wallpager_down">
      <div id="wallpager_up"></div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
  }
}
</script>

<style scoped>
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
