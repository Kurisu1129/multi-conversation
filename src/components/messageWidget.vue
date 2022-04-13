<template>
  <div class="common-layout">
    <el-container>
        <el-row>
            <el-col> 
                <el-avatar :src="sender" shape="circle"></el-avatar>
            </el-col>
    <el-col :span="12"><div class="grid-content bg-purple" /></el-col>
    <el-col :span="12"><div class="grid-content bg-purple-light" /></el-col>
    <el-col> 
                <el-avatar :src="receiver" shape="circle"></el-avatar>
            </el-col>
  </el-row>
    </el-container>
  </div>
</template>

<script>
import avator1 from "../assets/avator1.png"
import avator2 from "../assets/avator2.png"
export default {
  name: 'MessageWidget',
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
</style>

