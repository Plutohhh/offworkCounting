<script setup>
import HelloWorld from './components/HelloWorld.vue'
import offwork from './components/offwork.vue'
import Black from './components/Black.vue'
import temp from './components/temp.vue'
import Father from './view/Father.vue'
</script>

<template>
  <div class="container">
    <!-- <el-tabs tab-position="right" style="height: 200px" class="demo-tabs">
      <el-tab-pane label="User">User</el-tab-pane>
      <el-tab-pane label="Config">Config</el-tab-pane>
      <el-tab-pane label="Role">Role</el-tab-pane>
      <el-tab-pane label="Task">Task</el-tab-pane>
    </el-tabs> -->
    <el-carousel direction="vertical" :autoplay="false">
      <el-carousel-item>
        <Black />
      </el-carousel-item>
      <el-carousel-item>
        <Father />
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
  // overflow: hidden;
  // overflow-y: scroll;
  box-sizing: border-box;
  .el-carousel {
    position: relative;
    height: 100%;
    //页面内容铺满
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
    :deep(.el-carousel__indicators) {
      // height: 50%;
      // border: 2px solid #00eeff;
      .el-carousel__button {
        height: 40px;
        margin-bottom: 20px;
        margin-right: 10px;
        background-color: #000;
      }
      .is-active {
        .el-carousel__button {
          background-color: #ffd32a;
        }
      }
    }
  }
}
</style>
