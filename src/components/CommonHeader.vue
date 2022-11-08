<template>
  <div class="header">
    <el-header>
      <div class="l-content">
        <!-- 图标的展示 -->
        <el-button size="small" plain @click="handleCollapse">
            <el-icon :size="20"><Menu /></el-icon>
        </el-button>
        <h3>首页</h3>
      </div>
      <div class="r-content">
        <el-dropdown>
          <span class="el-dropdown-link">
            <img class="user" :src="imgSrc" alt="">
          </span>
          <template #dropdown>
            <el-dropdown-menu>
              <el-dropdown-item>个人中心</el-dropdown-item>
              <el-dropdown-item>退出</el-dropdown-item>
            </el-dropdown-menu>
          </template>
        </el-dropdown>
      </div>
    </el-header>
    
  </div>
</template>

<script>
import { useStore } from 'vuex'
export default {
  setup() {
    const store = useStore()
    // 动态使用图片
    const imgSrc = require("../assets/images/user.jpg");
    const handleCollapse = () => {
      // 调用vuex中的mutations
      store.commit("updateIsCollapse")
    }
    return {
      imgSrc,
      handleCollapse
    }
  }
}
</script>

<style lang="less" scoped>
.header {
  width: 100%;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  background: #333;
}
.r-content {
  .user {
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
}
.l-content {
  display: flex;
  align-items: center;
  .el-button {
    margin-right: 20px;
  }
  h3 {
    color: #fff;
  }
}
</style>