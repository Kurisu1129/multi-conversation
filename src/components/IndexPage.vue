<template>
    <el-container>
      <el-aside width="200px">Aside</el-aside>
      <el-main>
  <el-scrollbar height="400px">
    <p v-for="item in 20" :key="item" class="scrollbar-demo-item">{{ item }}</p>
  </el-scrollbar>
      </el-main>
    </el-container>
</template>

<script>
import avator1 from "../assets/avator1.png"
import avator2 from "../assets/avator2.png"
export default {
  name: 'IndexPage',
  props: {
    msg: String
  },
  data() {
    return {
      sender: avator1,
      receiver: avator2
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

