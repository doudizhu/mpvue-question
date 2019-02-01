<template lang="pug">
    scroll-view.learn(scroll-y)
        .start_lesson
            navigator(url='../question/main')
                button 重新提交
                
        .hot_lesson
            .lesson_all 
                span 统计结果
                span.look_all 分类
            div(v-for='(item,index) in hotLessons' :key='index')
                lesson-cell(:img='item.img' :title='item.title' :level='item.level' :count='item.count' :url='item.url')
</template>

<script>
import lessonCell from '../../components/lessonCell/index'
export default {
    data(){
        return {
            hotLessons: [
                {
                    "img":"/static/imgs/lesson/avatar_1091.jpg",
                    "title":"张迪",
                    "level":"赞成",
                    "count":"九点半",
                    "url":"后端"
                },
                // {
                //     "img":"/static/imgs/lesson/avatar_1089.jpg",
                //     "title":"王剑飞",
                //     "level":"不赞成",
                //     "count":"十点半",
                //     "url":"前端"
                // },
                {
                    "img":"/static/imgs/lesson/avatar_1090.jpg",
                    "title":"刘广睿",
                    "level":"不赞成",
                    "count":"十点半",
                    "url":"数据"
                },
                {
                    "img":"/static/imgs/lesson/avatar_1092.jpg",
                    "title":"王海超",
                    "level":"赞成",
                    "count":"十点",
                    "url":"测试"
                },
                {
                    "img":"/static/imgs/lesson/avatar_1096.jpg",
                    "title":"王楠",
                    "level":"赞成",
                    "count":"十点",
                    "url":"运维"
                },
                {
                    "img":"/static/imgs/lesson/avatar_1095.jpg",
                    "title":"李鹏",
                    "level":"赞成",
                    "count":"九点半",
                    "url":"前端"
                },
                {
                    "img":"/static/imgs/lesson/avatar_1094.jpg",
                    "title":"张安东",
                    "level":"赞成",
                    "count":"十点",
                    "url":"app"
                },
                {
                    "img":"/static/imgs/lesson/avatar_1093.jpg",
                    "title":"宁杉",
                    "level":"赞成",
                    "count":"九点半",
                    "url":"app"
                }
            ],
        }
    },
    onLoad(option){
        // console.log(option)
        // console.log(this.$store.state.user)
        let item = option.lesson.split(','),
            level = item[0],
            count = item[1],
            url = item[2],

            user = this.$store.state.user,
            img = user.avatarUrl,
            title = user.nickName,

            hotlesson = {
                img,
                title,
                level,
                count,
                url,
            }
            
        this.hotLessons.unshift(hotlesson)

    },
    components:{
        lessonCell,
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


.lesson_all {
  width: 100%;
  box-sizing: border-box;
  /* padding: 10px; */
  overflow: hidden;
  line-height: 46px;
  padding: 0 10px;
}
.lesson_all .look_all {
  font-size: 12px;
  color: #aaa;
  float: right;
  
}
</style>
