<template>
  <div class="about">
    <h1>This is about page</h1>
    <el-button @click="handleOnClick" type="primary" style="margin-left: 16px;">
      点我打开
    </el-button>
    <el-drawer
      title="我是标题"
      :visible.sync="drawer"
      :direction="direction"
      :before-close="handleClose">
      <div id="micro">
      </div>
    </el-drawer>
  </div>
</template>

<script>
import { loadMicroApp } from '../../../../es'
  export default {
    data() {
      return {
        drawer: false,
        direction: 'rtl',
      };
    },
    methods: {
      handleClose(done) {
        this.drawer = false
        // 实例不销毁，二次进入会报错
        // https://single-spa.js.org/error/?code=31&arg=mount&arg=parcel&arg=vue3_1629377228110_822&arg=3000
        // this.micro.unmount && this.micro.unmount()
      },
      handleOnClick () {
        this.drawer = true
        this.loadVueMicroApp()
      },
      loadVueMicroApp () {
        this.micro = loadMicroApp({
          name: 'vue3',
          entry: '//localhost:7105',
          container: '#micro',
        })
      }
    }
  };
</script>

<style scoped>
  .about {
    color: #7265e6;
  }
</style>
