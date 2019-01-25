<template lang="pug">
    scroll-view.learn(scroll-y)
        .start_lesson
            navigator(url='../question/main')
                button 重新提交
        
</template>

<script>
export default {
    onLoad(option){
        console.log(option)
        this.url = option.lesson
    },
}
</script>

<style scoped>
.learn {
  height: 100%;
  box-sizing: border-box;
}
.learn_info {
  padding: 10px;
  display: flex;
  flex-direction: row;
  background-color: #fff;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  border: 1px solid #ebeef5;
}
.learn_info img {
  width: 85px;
  height: 85px;
}
.info_text {
  padding: 10px;
}
.info_text h4 {
  font-weight: bold;
}
.info_text h4 span {
  color: #009eef;
}
.info_text p {
  color: #ccc;
  font-size: 14px;
  margin-top: 10px;
}
.info_text p span {
  color: #85c646;
}

.my_lesson .hot_lesson {
  width: 100%;
  margin-top: 16px;
  background-color: #fff;
  border: 1px solid #ebeef5;
}

.lesson_wrap {
  width: 100%;
  overflow-x: auto;
}
.lesson_scroll {
  max-width: 200%;
  min-width: 100%;
  display: flex;
  flex-direction: row;
}
.lesson_card {
  display: flex;
  flex-direction: column;
  min-width: 120px;
  padding: 10px 5px;
}
.lesson_card img {
  width: 100%;
  height: 100px;
  border-radius: 5px;
}
.lesson_card span {
  font-size: 14px;
  color: #333;
}
::-webkit-scrollbar {
  display: none;
}
.start_lesson {
  padding: 20px 0;
  box-sizing: border-box;
  text-align: center;
}
.start_lesson button {
  background-color: #fff;
  color: #009eef;
  width: 150px;
  border-radius: 30px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
.start_lesson button::after {
  border: none;
}

/* 修复样式 */
.my_lesson,
.start_lesson{
  background-color: #fff;
}
.my_lesson{
  margin-top: 16px;
  border-top: 1px solid #ebeef5;
}
.start_lesson{
  border-bottom: 1px solid #ebeef5;
}

.hot_lesson {
  width: 100%;
  margin-top: 16px;
  background-color: #fff;
  border: 1px solid #ebeef5;
}
</style>
