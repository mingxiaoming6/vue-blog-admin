<template>
  <div class="user-detail">
    <el-form label-position="left">
      <el-form-item label="姓名:" prop="user_cname">
        <span v-html="userDetail.user_cname"></span>
      </el-form-item>
      <el-form-item label="账号:" prop="user_name">
        <span v-html="userDetail.user_name"></span>
      </el-form-item>
      <el-form-item label="密码:" prop="user_password">
        <span v-html="userDetail.user_password"></span>
      </el-form-item>
      <el-form-item label="部门:" prop="user_department">
        <span v-html="userDetail.user_department"></span>
      </el-form-item>
      <el-form-item label="职位:" prop="user_role">
        <span v-html="userDetail.user_role"></span>
      </el-form-item>
      <el-form-item label="博客总数:" prop="article_count">
        <span v-html="userDetail.article_count"></span>
      </el-form-item>
      <el-form-item label="创建时间:" prop="create_time">
        <span v-html="userDetail.create_time"></span>
      </el-form-item>
      <el-form-item label="更新时间:" prop="update_time">
        <span v-html="userDetail.update_time"></span>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "user-detail",
  props: {
    userDetail: {
      type: Object,
      default: () => {}
    }
  }
};
</script>

<style lang="less">
.user-detail {
  .el-form-item__label {
    line-height: 24px;
  }
  .el-form-item__content {
    line-height: 24px;
  }
}
</style>