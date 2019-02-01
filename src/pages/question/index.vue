<template lang="pug">
.question
    img.bg(src='/static/imgs/test.jpg')
    .qs_content(v-if='questions.length > 0')
        div(v-if='!startqs')
            p.title 温馨提示
            .warn_tag 为了更好对的制定工作计划，提高大家的协作效率，请回答以下问题
        div(v-else)
            p.title {{questions[currentIndex].title}}
            .response(
                v-for="(item,index) in questions[currentIndex].option" 
                :key='index'
                @click="selectAnswer(index)"
                )
                img(v-if='item.select' src='/static/imgs/selected.jpg')
                img(v-else src='/static/imgs/unselect.jpg')
                span {{item.label}}

            div(v-if='plus_show' style="margin-top:20px;") 有什么好的建议或想法？
                textarea(placeholder='选填' style='border:1px solid #ccc;height:90px;')
    button.qs_btn(
        @click='btn_click'
        :disabled="disabled"
    ) {{btn_title}}
</template>

<script>
export default {
    data() {
        return {
            questions: [],
            startqs: false, // 是否显示问题列表
            currentIndex: 0, // 记录当前回答到第几道题
            btn_title: '开始问答', // 按钮的title
            lesson: '', // 记录提交的问题

            plus_show: true,// 补充说明
        }
    },
    onLoad() {
        this.getData();
    },
    onShow() {
        // 理解mpvue的生命周期
        // https://www.cnblogs.com/imgss/p/9164924.html
        // 重新进入页面后，需重置
        this.startqs = false
        this.currentIndex = 0
        this.btn_title = '开始问答'
        this.lesson = ''

        this.plus_show = true
    },
    computed: {
        disabled() {
            if (!this.startqs) return false
            else {
                const option = this.questions[this.currentIndex].option
                let select = false

                option.forEach(item => {
                    if (item.select) select = true
                })

                return !select
            }
        }
    },
    methods: {
        getData() {
            this.questions = [{
                    "title": "是否赞成召开技术晨会？",
                    "option": [{
                            "label": "赞成",
                            "select": false
                        },
                        {
                            "label": "不赞成",
                            "select": false
                        }
                    ]
                },
                {
                    "title": "晨会建议开始的时间？",
                    "option": [{
                            "label": "九点半",
                            "select": false
                        },
                        {
                            "label": "十点",
                            "select": false
                        },
                        {
                            "label": "十点半",
                            "select": false
                        }
                    ]
                },
                {
                    "title": "所属技术开发组",
                    "option": [{
                            "label": "前端",
                            "select": false
                        },
                        {
                            "label": "后端",
                            "select": false
                        },
                        {
                            "label": "app",
                            "select": false
                        },
                        {
                            "label": "测试",
                            "select": false
                        },
                        {
                            "label": "运维",
                            "select": false
                        }
                    ]
                },
                {
                    "title": "是否匿名？",
                    "option": [{
                            "label": "是",
                            "select": false
                        },
                        {
                            "label": "否",
                            "select": false
                        }
                    ]
                }
            ]
        },
        btn_click() {
            // 开始答题
            if (!this.startqs) {
                this.startqs = true
                this.btn_title = '下一题'
            }
            // 答题中
            else {
                this.lesson += this.getSelectOption()
                if (this.currentIndex < this.questions.length - 1) {
                    this.currentIndex++
                    this.lesson += ','
                    // 最后一题
                    if (this.currentIndex == this.questions.length - 1) {
                        this.btn_title = '完成'
                    }
                } else {
                    // console.log(this.lesson)
                    // 完成
                    this.sendQuestions()
                }

                if(this.currentIndex > 0){
                    this.plus_show = false
                }
            }
        },
        selectAnswer(index) {
            const option = this.questions[this.currentIndex].option
            // 将列表中的是否选项都置为未选中
            option.forEach(item => {
                item.select = false
            });
            // 将点击的选项选中
            option[index].select = !option[index].select
        },
        getSelectOption() {
            const option = this.questions[this.currentIndex].option
            let label = ''
            option.forEach(item => {
                if (item.select) label = item.label
            })
            return label
        },
        sendQuestions() {
            // console.log(this.lesson)
            // 存储对应成员答题情况，

            // 跳转结果展示页面
            wx.navigateTo({
                url: `../result/main?lesson=${this.lesson}`,
            })
        }
    }
}
</script>

<style scoped>
.question {
    width: 100%;
    height: 100%;
    overflow: hidden;
    position: relative;
}

.question .bg {
    width: 100%;
    height: 100%;
}

.qs_content {
    position: absolute;
    width: 80%;
    height: 50%;
    background: #fff;
    top: 36%;
    left: 10%;
    border-radius: 5px;
    box-sizing: border-box;
    padding: 10px;
    color: rgb(13, 28, 51);
}

.qs_btn {
    position: absolute;
    top: 90%;
    left: 10%;
    width: 80%;
    background-color: #009eef;
    color: white;
}

.title {
    font-weight: bold;
    margin-bottom: 20px;
    word-break: break-all;
}

.warn_tag {
    padding: 40px 10px;
}

.response {
    padding: 10px;
}

.response img {
    width: 20px;
    height: 20px;
    margin-right: 10px;
}
</style>
