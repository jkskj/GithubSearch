<template>
  <div class="row">
    <div v-show="info.users.length"
         class="card"
         v-for="user in info.users"
         :key="user.login">
      <a :href="user.html_url"
         target="_blank">
        <img :src="user.avatar_url"
             style="width: 100px" />
      </a>
      <p class="card-text">{{ user.login }}</p>
    </div>
    <!-- 展示欢迎词 -->
    <h1 v-show="info.isFirst">欢迎使用</h1>
    <!-- 展示加载中 -->
    <h1 v-show="info.isLoading">加载中......</h1>
    <!-- 展示错误信息 -->
    <h1 v-show="info.errMsg">{{ info.errMsg }}</h1>
  </div>
</template>

<script>
export default {
  name: "List",
  data () {
    return {
      info: {
        isFirst: true,
        isLoading: false,
        errMsg: "",
        users: [],
      },
    };
  },
  mounted () {
    this.$bus.$on("updateListData", (dataObj) => {
      console.log("我是List组件,收到了数据", dataObj);
      // this.users =user
      // this.users =dataObj.users
      // this.isFirst=dataObj.isFirst,
      // this.isLoading=dataObj.isLoading,
      // this.errMsg=dataObj.errMsg
      this.info = { ...this.info, ...dataObj };
    });
  },
};
</script>

<style scoped>
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}
#h1 {
  margin-right: 2rem;
}
.card {
  float: left;
  width: 33.333%;
  padding: 0.75rem;
  margin-bottom: 2rem;
  border: 1px solid #e80909;
  text-align: center;
  background-color: #08dceb;
}

.card > img {
  margin-bottom: 0.75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}
</style>
