<template>
  <div>
    <v-Bread></v-Bread>

    <el-button type="primary" plain size="small" @click="openInfo"
      >添加</el-button
    >
    <!-- 表格 -->
    <vTable @edit="edit"></vTable>
    <!-- 弹框 -->
    <vaddinfo ref="vAdd" :addInfo="addInfo" @cancel="cancel"></vaddinfo>
  </div>
</template>

<script>
import vTable from "./list";
import vaddinfo from "./addInfo";
export default {
  data() {
    return {
      addInfo: {
        isShow: false, //控制弹框显示隐藏
        isAdd: true //控制是添加或者编辑 true添加 false 编辑
      }
    };
  },
  components: {
    vTable,
    vaddinfo
  },
  methods: {
    openInfo() {
      this.addInfo.isShow = true;
      this.addInfo.isAdd = true;
      // console.log(this.addInfo.isShow);
    },
    cancel(e) {
      console.log(e,"wwwwwwwwwws");
      this.addInfo.isShow = e;
    },
    edit(e) {
      //e=id
      // console.log(this.$refs.vAdd);
      this.addInfo.isShow = true;
      this.addInfo.isAdd = false;
      this.$refs.vAdd.lookUp(e);
    }
  }
};
</script>

<style lang="stylus" scoped>
.el-button
  margin 10px 0
</style>
