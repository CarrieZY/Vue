<template>
  <div id="app">
    <!--我的路由的代码加载一次之后  后面直接调数据-->
    <keep-alive exclude="Detail">
      <router-view/>
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
</style>
