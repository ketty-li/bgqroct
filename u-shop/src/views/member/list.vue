<template>
  <div>
    <el-table
      :data="memberList"
      border
      style="width: 100%"
          
    >
     <el-table-column prop="id" label="用户编号" width="180">
      </el-table-column>
      <el-table-column prop="nickname" label="昵称" width="180">
      </el-table-column>
      <el-table-column prop="phone" label="手机号" width="180">
      </el-table-column>
     
      <el-table-column label="状态">
        <template slot-scope="item">
          <div>
            <el-tag v-if="item.row.status == 1" type="success">启用</el-tag>
            <!-- <el-tag v-else type="danger">禁用</el-tag> -->
          </div>
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="item">
          <div>
            <!-- {{ item.row.id }} -->
            <el-button type="primary" @click="edit(item.row.uid)" size="mini"
              >编辑</el-button
            >
            <!-- <el-button type="danger" @click="del(item.row.id)" size="mini"
              >删除</el-button
            > -->
          </div>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
// 接口文档引入
// import { deleteMenu } from "../../util/axios";
export default {
  data() {
    return {};
  },
  computed: {
    ...mapGetters({
      memberList: "member/getMemberList"
    })
  },
  mounted() {
    this.getMemberAction();
  },
  methods: {
    ...mapActions({
      getMemberAction: "member/getMemberListAction"
    }),
    // 删除事件
    // del(id) {
    //   this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
    //     confirmButtonText: "确定",
    //     cancelButtonText: "取消",
    //     type: "warning"
    //   })
    //     .then(() => {
    //       deleteMenu({ id }).then(res => {
    //         // console.log(res);
    //         if (res.data.code === 200) {
    //           this.$message.success(res.data.msg);
    //           this.getMenuList();
    //         } else {
    //           this.$message.error(res.data.msg);
    //         }
    //       });
    //     })
  
    //     .catch(() => {
    //       this.$message({
    //         type: "info",
    //         message: "已取消删除"
    //       });
    //     });
    // },
    // 编辑
    edit(id) {
      // console.log(id);
      this.$emit("edit", id);
    }
  }
};
</script>

<style lang="" scoped></style>
