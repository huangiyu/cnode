<template>
  <div class="article">
    <!--  如果正在加载就显示此div-->
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" alt="">
    </div>
    <div v-else class="">
      <div class="topic_header">
        <div class="topic_title">{{post.title}}</div>
        <ul>
          <li>•发布于：{{post.create_at | formatDate}}</li>
          <li>•作者：{{post.author.loginname}}</li>
          <li>•{{post.visit_count}}次浏览</li>
          <li>•来自：{{post | tabFormatter}}</li>
        </ul>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Article',
  data() {
    return {
      isLoading: false,
      post: {}   //当前文章页的所有内容
    }
  }
}
</script>

<style scoped>

</style>
