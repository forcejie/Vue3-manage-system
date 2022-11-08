<template>
  <div class="home1">
    <el-row :gutter="20" class="home">
      <el-col :span="8" style="margin-top: 20px">
        <el-card shadow="hover">
          <!-- 头像 -->
          <div class="user">
            <img src="../../assets/images/user.jpg" alt="">
            <div class="user-info">
              <p class="name">炸毛可乐</p>
              <p class="role">超级SVIP</p>
            </div>
          </div>
          <!-- 信息 -->
          <div class="login-info">
            <p>上次登录时间:<span>2022.11.08</span></p>
            <p>上次登录的地点:<span>平原湖</span></p>
          </div>
        </el-card>

        <!-- 下方数据 -->
        <el-card shadow="hover" style="margin-top: 20px" height="450px">
          <el-table :data="tableData">
          <el-table-column 
            v-for="(val, key) in tableLabel"
            :key="key"
            :prop="key" :label="val">
          </el-table-column>
        </el-table>
        </el-card>
      </el-col>
  </el-row>
  </div>
</template>

<script>
import { defineComponent, getCurrentInstance, onMounted, ref } from 'vue'
import axios from "axios"

export default defineComponent({
  setup() {
    // const {proxy} = getCurrentInstance()
    const tableData =  ref([]);
    const tableLabel = {
      name:"课程",
      todayBuy: "今日购买",
      monthBuy: "今月购买",
      totalBuy: "总购买"
    };

    const getTableList = async () => {
      await axios
      .get('https://www.fastmock.site/mock/466218e1cc6aa1b51fff62a0598b8b67/api/home/getTableData')
      .then((res) => {
        // tableData.value = res.data.data.tableData
        if (res.data.code == 200) {
          tableData.value = res.data.data
        }
      })

      // let res = await proxy.$api.getTableData();
    };
    onMounted(() => {
      getTableList()
    })
    
    return {
      tableData,
      tableLabel,
      getTableList
     }

  }
  
})
</script>

<style lang="less" scoped>
.home {
  .user {
    display: flex;
    align-items: center;
    padding-bottom: 20px;
    border-bottom: 1px solid #ccc;
    margin-bottom: 20px;
    img {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      margin-right: 40px;
    }
    .user-info {
      .name {
        font-size: 26px;
        color: rgb(101, 97, 97);
      }
      .role {
        padding: 10px 0;
        font-size: 16px;
        color: rgb(122, 123, 124);
      }
    }
  }
  .login-info {
    p {
      line-height: 30px;
      font-size: 14px;
      color: #999;
      span {
        color: #666;
        margin-left: 60px;
      }
    }
  }
}
</style>