<template lang='pug'>
    .container
      .login
        img(src='/static/imgs/guide_bg.jpg')
      .learn
        button(
          open-type="getUserInfo"
          @getuserinfo="getUserInfo"
        ) 调查问卷
</template>

<script>
export default {
  methods: {
    getUserInfo(e) {
      // 判断授权是否成功
      if(e.mp.detail.userInfo){
        // console.log(e.mp.detail.userInfo)
        // 存储到vuex
        this.$store.dispatch('setIsAuthenticated',true)
        this.$store.dispatch('setUser', e.mp.detail.userInfo)
      }  
    },
  },
}
</script>

<style scoped lang='scss'>
.container {
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.login {
  width: 100%;
  height: 100%;
  position: relative;
}
.login img {
  display: inline-block;
  width: 100%;
  height: 100%;
}
.login .learn {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  top: 0;
  left: 0;
}
.learn button {
  position: absolute;
  top: 90%;
  left: 10%;
  width: 80%;
  background-color: #009eef;
  color: white;
}
</style>
