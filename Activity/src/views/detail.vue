<template>
  <div id="main">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1,minimum-scale=1,user-scalable=no">
    <div class="change">
      <headNav headline=详情>
        <template slot="left_element">
            <Icon type="ios-arrow-back" color="#7e7e7e" size="26"
                @click="back()"/>
        </template>
      </headNav>
      <func :info="information"></func>
      <div class="choose">
        <div class="choice">
            评论
        </div>
      </div>
      <comment v-for="item in comments" 
      :name="item.name"
      :time="item.time"
      :content="item.content"
      :likeCount="item.likeCount"
      ></comment>
      <bottom v-on:getContent="getCont"></bottom>
      <div id="foot"></div>
    </div>
  </div>
</template>

<script>
import utils from '../assets/utils'
import headNav from '../components/headNav/HeadBar'
import bottom from '../components/contentBlock/bottom.vue'
import func from '../components/contentBlock/function.vue'
import comment from '../components/comment/'
export default {
    data: function () {
        return {
            route: null,
            information: null,
            detailAPI: 'http://118.89.48.63:8001/activity/',
            comments: [
                {
                    name: 'CR7',
                    time: '12:02',
                    content: '说来也不难，flex 的核心的概念就是容器和轴。容器包括外层的父容器也一样也一样',
                    likeCount: 15,
                },
                {
                    name: 'CR7',
                    time: '12:03',
                    content: 'C罗最帅',
                    likeCount: 16,
                }
            ]
        }
    },
    components: {
      bottom,
      func,
      comment,
      headNav
    },
    created () {
        this.route = this.$route.params.projectID;
        console.log(this.route)
        this.detailAPI += this.route
        console.log(this.detailAPI);
        // if (this.route == '/')
        // this.route = '/home'
        // // 验证token
        let token = utils.getCookie('token')
        if (token != '') {
            this.$http.get(
            this.detailAPI, {
            headers: {
            Authorization: 'JWT ' + token
            }
            }).then((response) => {
                this.information = response.data.info
                console.log(this.information)
                // let data = response.data
                // if (data.code == 200) {
                // utils.setCookie('userInfo', data.user_info)
                // utils.setCookie('token', data.token)
                // utils.setCookie('expires', data.expires)
                // this.loginSuccess(data.user_info)
                // }
            })
        }
        // if (!this.login){
        // this.$router.push('/login')
        // return
        // }
        // console.log(this.route);
        // this.$router.push(this.route)
    },
    methods: {
        back () {
            this.$router.go(-1)
        },
        getCont: function(cont,t){
            if(cont.length != 0){
                this.$data.comments.push(
                {
                        name: 'CR7',
                        time: t,
                        content: cont,
                        likeCount: 0,
                }
                )
            }
        document.querySelector("#foot").scrollIntoView(true);
        }
    }
}
</script>

<style scoped>
    .choice{
      margin-left:5px;
      margin-top:5px;
      margin-bottom:5px;
    }
    .change{
        margin-bottom:50px;
    }
    .choose{
      border-top: 5px solid #efefef;
      border-bottom: 1px solid #e0e0e0;
    }
    #foot{
        height:65px;
        width: 100%;
    }
</style>