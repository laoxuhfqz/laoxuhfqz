<template>
  <div>
    <!-- 顶部导航栏区 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>权限列表</el-breadcrumb-item>
    </el-breadcrumb>

    <el-table :data="rightsList" stripe border>
      <el-table-column type="index"></el-table-column>
      <el-table-column label="权限名称" prop="authName"></el-table-column>
      <el-table-column label="路径" prop="path"></el-table-column>
      <el-table-column label="权限等级" prop="level">
        <template slot-scope="scope">
          <!-- {{scope.row.level}} -->
          <el-tag v-if="scope.row.level === '0'">一级权限</el-tag>
          <el-tag v-if="scope.row.level === '1'" type="success">二级权限</el-tag>
          <el-tag v-if="scope.row.level === '2'" type="warning">三级权限</el-tag>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rightsList: []
    }
  },
  created() {
    this.getRightsList()
  },
  methods: {
    async getRightsList() {
      const { data: res } = await this.$http.get('rights/list')
      //   console.log(res.meta.status)
      if (res.meta.status !== 200) {
        return this.$message.error('获取权限列表失败')
      }
      this.rightsList = res.data
      //   console.log(this.rightsList)
    }
  }
}
</script>

<style lang="less" scoped>
</style>
