<template>
  <div>
    <el-table :data="bannerList" border style="width: 100%">
      <el-table-column prop="id" label="编号"> </el-table-column> 
      <el-table-column prop="title" label="轮播图标题"> </el-table-column>
      <el-table-column label="图片">
        <template slot-scope="item">
          <div>
            <img
              class="img"
              :src="
                item.row.img
                  ? $imgUrl + item.row.img
                  : 'https://dss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3363295869,2467511306&fm=26&gp=0.jpg'
              "
              alt=""
            />
          </div>
        </template>
      </el-table-column>

      <el-table-column label="状态">
        <template slot-scope="item">
          <div>
            <el-tag v-if="item.row.status == 1" type="success">启用</el-tag>
            <el-tag v-else type="danger">禁用</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="item">
          <div>
            <!-- {{ item.row.id }} -->
            <el-button type="primary" @click="edit(item.row.id)" size="mini"
              >编辑</el-button
            >
            <el-button type="danger" @click="del(item.row.id)" size="mini"
              >删除</el-button
            >
          </div>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
// 接口文档引入
import { getBannerDelete } from "../../util/axios";
export default {
  data() {
    return {};
  },
  computed: {
    ...mapGetters({
      bannerList: "banner/getBannerList"
    })
  },
  mounted() {
    this.getBannerList();
  },
  methods: {
    ...mapActions({
      getBannerList: "banner/getBannerListAction"
    }),
    // 删除事件
    del(id) {
      this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          getBannerDelete({ id }).then(res => {
            // console.log(res);
            if (res.data.code === 200) {
              this.$message.success(res.data.msg);
              this.getBannerList();
            } else {
              this.$message.error(res.data.msg);
            }
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    },
    // 编辑
    edit(id) {
      // 传递父组件，传值并打开弹框
      this.$emit("edit", id);
    }
  }
};
</script>

<style lang="" scoped>
.img {
  width: 100px;
  height: 100px;
}
</style>
