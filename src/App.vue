<template>
  <div id="app">
    <Header />
    <PostList />
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import PostList from "@/components/PostList.vue";
export default {
  components: {
    Header,
    PostList,
  },
};
</script>
<style>
*{
 margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-size: 16px;
 
  background-color: rgb(225, 225, 225);
}
ul,
ol {
  list-style: none;
  margin: 0;
  padding: 0;
}
a {
  text-decoration: none;
  color: #333;
}
</style>
