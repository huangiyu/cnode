<template>
  <div>
    <!--    数据未返回时，显示加载页面-->
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" alt="">
    </div>
    <!--    帖子列表-->
    <div>
      <ul>
        <li>

        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PostList',
  data() {
    return {
      isLoading: false
    }
  },
  methods: {
    getData() {
      this.$http.get('Access-Control-Allow-Origin:https://www.v2ex.com/api/topics/hot.json',{
        page: 1,
        limit: 20
      })
        .then(res => {
          this.isLoading = false;  //加载成功，去除动画
          console.log(res)
        })
      .catch(err =>{
        console.log(err)
      })
    }
  },
  beforeMount() {
    this.isLoading = true;  //页面加载前现实加载动画
    this.getData();  //页面加载前加载数据
  }
}
</script>

<style scoped>


</style>
