<template>
  <div class="common-layout">
    <el-container>
        <el-row>
    <el-col :span="12"><div class="grid-content bg-purple" /></el-col>
    <el-col :span="12"><div class="grid-content bg-purple-light" /></el-col>
  </el-row>
    </el-container>
  </div>
</template>

<script>
export default {
  name: 'Message',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

