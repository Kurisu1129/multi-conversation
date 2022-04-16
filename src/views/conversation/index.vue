<template>
  <div>
    <el-row>
      <el-col class="padding"
        ><el-card shadow="always">
          <el-row>
            <div>请选择测试方式：</div>
            <div>1.选择系统所提供的示例：点击下拉框进行选择</div>
            <div>2.外部导入txt文件：点击下拉框最后一项"..."</div>
          </el-row>
          <el-row type="flex">
            <el-col style="width: 500%">
              <el-select
                clearable
                v-model="input"
                placeholder="请选择"
                style="width: 98%"
                @change="selectChange"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
            </el-col>
            <el-col>
              <el-row>
                <el-col style="width: 50%">
                  <el-upload
                    class="upload-demo"
                    action="https://jsonplaceholder.typicode.com/posts/"
                    :before-remove="beforeRemove"
                    multiple
                    :limit="3"
                    :on-success="handleTxt"
                  >
                    <el-button type="primary"
                      ><i class="el-icon-folder-add el-icon--left"></i
                      >导入txt文件</el-button
                    >
                  </el-upload>
                </el-col>
                <el-col style="width: 50%">
                  <el-button type="primary" @click="getAnswer" v-loading.fullscreen.lock="fullscreenLoading"
                    ><i class="el-icon-cpu el-icon--left"></i
                    >生成结果</el-button
                  >
                </el-col>
              </el-row>
            </el-col>
          </el-row>
        </el-card></el-col
      >
    </el-row>
    <el-row style="height: 70vh">
      <el-col class="padding" style="width: 50%; height: 100%">
        <el-card shadow="always" body-style="height: 60vh">
          <div slot="header" class="clearfix">
            <span>输入内容</span>
          </div>
          <div>{{inputShow}}</div>
        </el-card>
      </el-col>
      <el-col class="padding" style="width: 50%">
        <el-row class="padding">
          <el-card shadow="always" body-style="height: 30vh">
            <div slot="header" class="clearfix">
              <span>模型生成答案</span>
            </div>
            <div>{{answer}}</div>
          </el-card>
        </el-row>
        <el-row class="padding">
          <el-card shadow="always" body-style="height: 19vh">
            <div slot="header" class="clearfix">
              <span>参考答案</span>
            </div>
            <div>{{target}}</div>
          </el-card>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import axios from 'axios'
export default {
  name: "Conversation",
  computed: {
    ...mapGetters(["name"]),
  },
  mounted() {
      var that = this
      axios.get(encodeURI('http://127.0.0.1:5000' + '/options/')).then(resp => {
                that.options = resp.data
                console.log(that.options)
            })
  },
  data() {
    return {
      options: [
        {
          value: "有 活动 吗 <eos> 538832022583 这个 是不是 小包 得 <eos> 啥 无妨 <eos> 528690173109 这 两个 哪个 好	纯棉 的 更加 柔软",
          label: "有 活动 吗 <eos> 538832022583 这个 是不是 小包 得 <eos> 啥 无妨 <eos> 528690173109 这 两个 哪个 好	纯棉 的 更加 柔软",
        },
        {
          value: "核桃 是 正品 吗 <eos> 可以 优惠 吗 <eos> 有 夹子 送 吗	亲亲 没有 夹 核桃 的 大 夹子 哦 我们 都 有 送 开果器 呢 我们 家 的 核桃壳 薄如纸 手 捏 即 破 哦 不用 担心 呢",
          label: "核桃 是 正品 吗 <eos> 可以 优惠 吗 <eos> 有 夹子 送 吗	亲亲 没有 夹 核桃 的 大 夹子 哦 我们 都 有 送 开果器 呢 我们 家 的 核桃壳 薄如纸 手 捏 即 破 哦 不用 担心 呢",
        },
        {
          value: "在 吗 亲 <eos> 今天 有 优惠 是 吗 买 三袋 芒果 干 199 <eos> 能 今天 发货 嘛 <eos> 就 今天 特价 是 吗 <eos> 好 的 <eos> 发 什么 快递	亲爱 哒 小 二家 默认 是 天天 ems 快递 哦 不 接受 ",
          label: "在 吗 亲 <eos> 今天 有 优惠 是 吗 买 三袋 芒果 干 199 <eos> 能 今天 发货 嘛 <eos> 就 今天 特价 是 吗 <eos> 好 的 <eos> 发 什么 快递	亲爱 哒 小 二家 默认 是 天天 ems 快递 哦 不 接受 ",
        },
        {
          value: "选项4",
          label: "龙须面",
        },
        {
          value: "选项5",
          label: "北京烤鸭",
        },
      ],
      input: "",
      inputShow:"",
      originInput: "",
      answer:"",
      target:"",
      fullscreenLoading: false
    };
  },
  methods: {
      handleTxt(response, file, fileList) {
var reader = new FileReader();
var that = this
            reader.readAsText(file.raw);

            reader.onload = function() {
                console.log(reader.result)
                that.originInput = reader.result
                var temp = reader.result.split('\t')[0]
                that.input = temp
                that.inputShow = temp

            };

      },
      getAnswer() {
          var input = this.originInput
          this.fullscreenLoading = true
        if (input !== '') {
            var that = this
            axios.get(encodeURI('http://127.0.0.1:5000' + '/result/' + input)).then(resp => {
                that.answer = resp.data.answer
                that.target = resp.data.target
                that.fullscreenLoading = false
            }).catch(() => {
                that.fullscreenLoading = false
            })
        }
      },

      selectChange() {
          this.originInput = this.input
          this.inputShow = this.input.split('\t')[0]
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
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
.padding {
  padding: 10px;
}
</style>