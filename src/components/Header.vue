<template>
  <nav class="header">
    <div class="content">
      <img src="//static2.cnodejs.org/public/images/cnodejs_light.svg" />
      <ul>
        <li>
          <a href="#">首页</a>
        </li>
        <li>
          <a href="#">新手入门</a>
        </li>
        <li>
          <a href="#">API</a>
        </li>
        <li>
          <a href="#">关于</a>
        </li>
        <li>
          <a href="#">注册</a>
        </li>
        <li>
          <a href="#">登录</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style scoped>
.header {
  background-color: rgb(68, 68, 68);
}
.content{
    display: flex;
    max-width: 1200px;
    margin: 0 auto;
    height: 50px;
    align-items: center;
    justify-content: space-between;
}
img {
  width: 120px;
  height: 30px;
}
li {
  display: inline-block;
  text-align: center;
}
a{
    color: rgb(204, 204, 204);
    padding: 0 15px;
}
a:hover{
    color: white;
}
</style>