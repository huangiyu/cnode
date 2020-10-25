<template>
  <div class="PostList">
    <!--    数据未返回时，显示加载页面-->
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" alt="">
    </div>
    <!--    帖子列表-->
    <div class="posts">
      <ul>
        <li>
          <div class="topbar">
            <span>全部</span>
            <span>精华</span>
            <span>分享</span>
            <span>问答</span>
            <span>招聘</span>
          </div>
        </li>
        <li v-for="post in posts">
          <!--          头像-->
          <img :src="post.author.avatar_url" alt="">
          <!--          回复量和浏览量-->
          <span class="allcount">
            <span class="reply_count">{{ post.reply_count }}</span>/{{ post.visit_count }}
          </span>
          <!--          帖子的分类-->
          <span :class="[{put_good:(post.good == true),put_top:(post.top == true),
          'topiclist-tab':(post.top != true && post.good != true)}]">
          <span>
            {{ post | tabFormatter }}
          </span>
          </span>
          <!--          标题-->
          <router-link :to="{
            name:'post_content',
            params:{
              id:post.id
            }
          }">
          <span>
            {{ post.title }}
          </span>
          </router-link>
          <!--          最终回复时间-->
          <span class="last_reply">
            {{ post.last_reply_at | formatDate }}
          </span>
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
      isLoading: false,
      posts: [],
    }
  },
  methods: {
    getData() {
      this.$http.get('https://52.197.183.123/api/v1/topics', {page: 1, limit: 20})
        .then(res => {
          this.isLoading = false;  //加载成功，去除动画
          console.log(res)
          this.posts = res.data.data
        })
        .catch(err => {
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
.PostList {
  background-color: #e1e1e1;
}

/*.posts {*/
/*  margin-top: 10px;*/
/*}*/

.PostList img {
  width: 30px;
  height: 30px;
  vertical-align: middle;
}

ul {
  padding-left: 0px; /*ul有40px的默认的padding-left*/
  list-style: none;
  width: 100%;
  max-width: 1300px;
  margin: 0 auto;
}

ul > li:not(:first-child) {
  padding: 9px;
  color: #333;
  background-color: white;
  border-bottom: 1px solid #f0f0f0;
  font-size: 15px;
}


li:not(:first-child):hover {
  background: #f5f5f5;
}

li:last-child:hover {
  background: white;
}

li span {
  line-height: 30px;
}

.allcount {
  width: 70px;
  display: inline-block;
  text-align: center;
  font-size: 12px;
}

.reply_count {
  color: #9e78c0;
  font-size: 12px;
}

.put_good, .put_top {
  background: #80bd01;
  padding: 2px 4px;
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -o-border-radius: 3px;
  color: #fff;
  font-size: 12px;
  margin-right: 10px;
}

.topiclist-tab {
  background-color: #e5e5e5;
  color: #999;
  padding: 2px 4px;
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -o-border-radius: 3px;
  font-size: 12px;
  margin-right: 10px;
}


.last_reply {
  text-align: right;
  min-width: 50px;
  display: inline-block;
  white-space: nowrap;
  float: right;
  color: #778087;
  font-size: 12px;
}

.topbar {
  height: 40px;
  background-color: #f5f5f5;
}

.topbar span {
  color: #80bd01;
  font-size: 14px;
  line-height: 40px;
  margin: 0 9px;
  cursor: pointer; /*鼠标悬浮的样式（手型）*/
}


</style>
