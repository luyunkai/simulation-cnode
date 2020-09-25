<template>
  <div>
    <div class="loading" v-if="isLoading">
      <img src="@/assets/loading.png" />
    </div>
    <div class="content" v-else>
      <ul class="nav">
        <li>全部</li>
        <li>精华</li>
        <li>分享</li>
        <li>问答</li>
        <li>招聘</li>
        <li>客户端测试</li>
      </ul>
      <ul class="postPlate">
        <li v-for="(post,index) in posts" :key="index">
          <!-- 头像 -->
          <img :src="post.author.avatar_url" />
          <!-- 回复和浏览量 -->
          <span class="count">
            <span class="reply_count">{{post.reply_count}}</span>
            <span class="separator">/</span>
            <span class="visit_count">{{post.visit_count}}</span>
          </span>
          <!-- 帖子分类 -->

          <span :class="post.good || post.top ? 'good-top' : 'other' ">{{post | formatTopicType}}</span>
          <!-- 标题 -->
          <a href="#" class="title">{{post.title}}</a>
          <!-- 最近回复时间 -->
          <span class="last_reply_at">{{post.last_reply_at | formatDate}}</span>
        </li>
        <!-- 分页 -->
        <li class="lastLi">
          <Pagination @handleList="renderList" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Pagination from "@/components/Pagination.vue";
export default {
  data() {
    return {
      posts: [],
      postpage: 1,
      isLoading: true,
    };
  },
  components: {
    Pagination,
  },
  methods: {
    renderList(value) {
      this.postpage = value;
      this.getData();
    },
    getData() {
      this.$http
        .get("https://cnodejs.org/api/v1/topics", {
          params: {
            page: this.postpage,
            limit: 20,
          },
        })
        .then((res) => {
          this.posts = res.data.data;
          this.isLoading = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  beforeMount() {
    this.getData();
  },
};
</script>

<style scoped>
.loading {
  display: inline-block;
  position: absolute;
  left: 48%;
  top: 48%;
  transform: translate(-50px,-50px);
  animation: name 1s linear infinite;
}
@keyframes name {
  0% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(90deg);
  }
  50% {
    transform: rotate(180deg);
  }
  75% {
    transform: rotate(270deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.loading > img {
  width: 80px;
  height: 80px;
}
.lastLi {
  height: 50px;
}
.nav {
  display: flex;
  height: 40px;
  align-items: center;
  padding: 10px;
  background-color: rgb(246, 246, 246);
}
.nav > li {
  font-size: 14px;
  color: #80bd01;
  margin: 0 10px;
  cursor: pointer;
}
.nav > li:hover {
  background-color: #80bd01;
  color: white;
  border-radius: 4px;
  padding: 3px 5px;
}

.title {
  color: #333;
}
.content {
  max-width: 1200px;
  margin: 0 auto;
  background-color: white;
  margin-top: 15px;
}
img {
  width: 30px;
  height: 30px;
}
.reply_count {
  font-size: 14px;
  color: #9e78c0;
}
.visit_count {
  font-size: 10px;
  color: #b4b4b4;
}
.separator {
  font-size: 12px;
  color: #333;
}
.postPlate > li {
  padding: 10px;
  box-shadow: 0 0 1px #999;
  display: flex;
  align-items: center;
}
.postPlate > li:hover {
  background-color: rgb(245, 245, 245);
}
.count {
  width: 70px;
  display: inline-block;
  text-align: center;
}
.last_reply_at {
  font-size: 12px;
  color: #778087;
  flex: 1;
  text-align: right;
}
.good-top {
  width: 32px;
  height: 18px;
  font-size: 12px;
  background-color: #80bd01;
  text-align: center;
  line-height: 18px;
  border-radius: 3px;
  color: white;
  margin-right: 5px;
}
.other {
  margin-right: 5px;
  border-radius: 3px;
  line-height: 18px;
  width: 32px;
  height: 18px;
  font-size: 12px;
  color: #999;
  text-align: center;
  background-color: rgb(229, 229, 229);
}
</style>