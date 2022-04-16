<template>
  <div>
    <el-row>
      <el-col style="width: 60%">
        <div style="width: 100%;
    height: 100%;
    object-fit:cover;">
        <el-image 
      fit="fill"
    :src="modelPngUrl" 
    :preview-src-list="modelPngList">
  </el-image></div></el-col>
      <el-col style="width: 40%">
        <el-card>本系统所采用的改进Seq2seq模型的总体架构如左图所示，包括编码器层（Encoder）、注意力机制层、解码器层（Decoder）、集束搜索语句生成层4个模块。其中，C为语义向量，即词向量从编码层输出到解码层输入之间的中间向量；α为全局注意力机制中分配给当前词的权重；h为隐藏状态量；C_t，α_t和h_t分别为第t个词嵌入经过处理后所对应的语义向量，全局注意力权重和隐藏状态量。S为机器生成候选答案的分数，即集束搜索步骤的依据.
编码器层将给定的批次长度的输入语句单词索引转换为词嵌入（Word Embedding），通过双向循环神经网络（Bidirectional Recurrent Neural Network, BiRNN）进行编码，将输入语句通过非线性变换转化为中间语义表示。注意力机制层提供一个类似于相似性度量的机制，它可以根据当前输出单词为下一个单词的中间语义表示赋予不同的注意力权重，从而提高模型的性能。经过注意力机制层的处理后，将输出向量传入解码器层，通过门控循环单元（Gated Recurrent Unit, GRU）进行前向传播，将编码向量结合全局注意力机制的所得结果进行输出。最后，通过集束搜索策略，在候选列表中选择得分最高的输出序列作为最终输出的回复语句。
</el-card>
      </el-col>
      </el-row>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "ModelShow",
  computed: {
    ...mapGetters(["name"]),
  },
  data() {
    return {
      modelPngUrl: require("../../assets/model.png"),
      modelPngList: [require("../../assets/model.png")]
    }
  }
};
</script>

<style lang="scss" scoped>
.el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
    height: 100vh;
  }
  .bg-purple-light {
    background: #e5e9f2;
    height: 100vh;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
  .el-image {
    width: 100%;
    height: 100%;
    object-fit:cover;
  }
</style>