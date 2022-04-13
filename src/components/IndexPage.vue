<template>
    <el-container>
      <el-aside width="200px">Aside</el-aside>
      <el-main>
  <el-scrollbar height="400px">
    <p v-for="item in 20" :key="item" class="scrollbar-demo-item"><MessageWidget></MessageWidget></p>
  </el-scrollbar>
      </el-main>
    </el-container>
</template>

<script>
import MessageWidget from "./messageWidget.vue"
export default {
  components: {
    MessageWidget
  },
  name: 'IndexPage',
  props: {
    msg: String
  },
  data() {
    return {
    
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.scrollbar-demo-item {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
  margin: 10px;
  text-align: center;
  border-radius: 4px;
  background: var(--el-color-primary-light-9);
  color: var(--el-color-primary);
}
</style>

