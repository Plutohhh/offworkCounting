<script setup>
import HelloWorld from './components/HelloWorld.vue'
import offwork from './components/offwork.vue'
import Black from './components/Black.vue'
import temp from './components/temp.vue'
</script>

<template>
  <div class="container">
    <!-- <offwork /> -->
    <el-carousel direction="vertical" :autoplay="false">
      <el-carousel-item>
        <Black />
      </el-carousel-item>
      <el-carousel-item>
        <offwork />
      </el-carousel-item>
      <el-carousel-item>
        <temp />
      </el-carousel-item>
    </el-carousel>
  </div>
</template>

<style scoped lang="scss">
.container {
  // font-size: calc(100vw / 1080);
  position: absolute;
  /* background-color: black; */
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  // border: 1px solid #ee0808;
  overflow: hidden;
  box-sizing: border-box;
  .el-carousel {
    position: relative;
    height: 100%;
    // border: 2px solid #00eeff;
    :deep(.el-carousel__container) {
      // border: 2px solid #00eeff;
      height: 100% !important;
      .el-carousel__item {
        // border: 2px solid #55ff07;
        height: 100%;
        overflow: hidden;
        box-sizing: border-box;
      }
    }
  }
}
</style>
