<template>
  <div>
    <!--    头部-->
    <div style="width: 100%; height: 60px; line-height: 60px; background-color: orangered ">
      <el-row >
        <el-col :span="4">
          <div style="font-size: 20px; font-weight: bold; text-align: center">校园二手交易平台</div>
        </el-col>
        <el-col :span="10" >

            <el-menu class="side-menu" :default-active="$route.path" background-color="#ff4500" @select="handleMenuSelect" mode="horizontal" text-color="#000000">
              <el-menu-item index="/front/home">
                首页
              </el-menu-item>
              <el-menu-item index="/front/cart">
                购物车
              </el-menu-item>
              <el-menu-item index="/front/order">
                我的订单
              </el-menu-item>
              <el-menu-item index="/front/collect">
                收藏夹
              </el-menu-item>
              <el-menu-item index="/front/person">
                个人中心
              </el-menu-item>
              <el-menu-item index="/front/address">
                收货地址
              </el-menu-item>
            </el-menu>

        </el-col>
        <el-col :span="6">
          <div v-if="!$route.path.includes('/search')">
            <el-input style="width: 80%" placeholder="请输入商品名称搜索商品" v-model="searchText"></el-input>
            <el-button style="margin-left: 5px" @click="search">搜索</el-button>
          </div>
          <div v-else>
            <div style="width: 100px;height: 20px"></div>
          </div>
        </el-col>
        <el-col :span="4">
          <div style="text-align: right; padding-right: 10px" v-if="user.id">
            <el-dropdown style="float: right;" @command="handleCommand" size="large">
              <span class="el-dropdown-link" style="cursor: pointer">
                欢迎你！{{ user.username }}<i class="el-icon-arrow-down el-icon--right"></i>
              </span>
              <el-dropdown-menu slot="dropdown" >
                <el-dropdown-item command="person">个人信息</el-dropdown-item>
                <el-dropdown-item command="loginOut">退出登录</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </div>
          <div style="text-align: right; padding-right: 10px" v-else>
            <el-button @click="$router.replace('/login')">登录</el-button>
            <el-button @click="$router.replace('/register')">注册</el-button>
          </div>

        </el-col>
      </el-row>
    </div>

    <!-- 主体 -->
    <el-row>
      <el-col :span="16" :offset="4" style="margin-bottom: 80px">
        <router-view />
      </el-col>
    </el-row>

<!--    底部-->
    <div style="height: 60px; width: 100%; background-color: white; padding: 10px 0; position: fixed; bottom: 0">
      <div style="text-align: center">
        企业级应用开发
      </div>
      <div style="text-align: center; padding: 5px 0">
        武汉理工大学  <span style="margin-left: 20px">计算机研225 周莹静</span>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: "Front",
  data() {
    return {
      searchText: '',
      user: {}
    }
  },
  created() {
    this.user = sessionStorage.getItem("user") ? JSON.parse(sessionStorage.getItem("user")) : {}
  },
  methods: {
    search() {
      this.$router.replace({path: '/front/search', query: {searchText: this.searchText}})
    },
    handleCommand(command) {
      if (command === 'person') {
        this.$router.push('/front/person');
      }
      if (command === 'loginOut') {
        sessionStorage.removeItem("user")
        this.$router.replace('/login');

      }
    },
    handleMenuSelect(index) {
      console.log(index)
      this.$router.push(index);
    },
  }
}
</script>

<style scoped>

</style>
