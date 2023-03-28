<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text"
             placeholder="enter the name you search"
             v-model="keyWord" />&nbsp;
      <!-- 绑定key-word关键字，方便在搜索框中输入的可以接受到 -->
      <button @click="searchUsers">Search</button>
      <!-- 添加点击事件-  -->
    </div>
  </section>
</template>

<script>
import axios from "axios"; //引入第三方 axios向后台请求数据
export default {
  name: "search",
  data () {
    return {
      keyWord: "",
    };
  },
  methods: {
    searchUsers () {
      this.$bus.$emit("updateListData", {
        isFirst: false,
        isLoading: true,
        errMsg: "",
        users: [],
      });
      // https://api.github.com/
      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        (response) => {
          console.log("请求成功");
          // this.$bus.$emit('getUser',response.data.items)
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: "",
            users: response.data.items,
          });
        },
        (error) => {
          console.log("请求失败", error.message);
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: error.message,
            users: [],
          });
        }
      );
    },
  },
};
</script>
