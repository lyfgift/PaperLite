<template>
  <div class="information">
        <headNav headline=信息>
            <template slot="left_element">
                <Icon type="ios-arrow-back" color="#7e7e7e" size="26"
                    @click="back()"/>
            </template>
        </headNav>
        <div class="share-wrap" ref="screenshot">
            <img :src='imgUrl' class="headImg" @click="changeHeadImg()"  crossOrigin="anonymous">
        </div>
            <div  class="nickName">
                {{name}}
            </div>
        <div class="info">
            <div class="name">
            <div class="y">姓名</div>
            <div class="ch">
                {{name}}
            </div>
            </div>
            <div class="sno">
            <div class="y">学号</div>
            <div class="ch">
                {{sno}}
            </div>
            </div>
            <div class="gender">
            <div class="y">性别</div>
            <div class="ch">
                {{gender}}
            </div>
            </div>
            <div class="nickname" @click="changeNickname">
            <div class="y">昵称</div>
            <div class="ch">
                {{major}}
            </div>
            </div>
            <div class="academy">
            <div class="y">学院</div>
            <div class="ch">
                {{academy}}
            </div>
            </div>
            <div class="major">
            <div class="y">专业</div>
            <div class="ch">
                {{major}}
            </div>
            </div>
            <div class="cls">
            <div class="y">班级</div>
            <div class="ch">
                {{cls}}
            </div>
            </div>
            
            <div class="email">
            <div class="y">邮箱</div>
            <div class="ch">
                {{email}}
            </div>
            </div>
        </div>
        <div class="mask" v-show="maskShow" @click="changeHeadImg()">
        </div>
        <div class="child" v-show="maskShow">
            <cropper :uploadType="`head`" :imgWidth="`85px`" :imgHeight="`85px`" :imgUrl="imgUrl" @upload="getImgUrl"></cropper>
            <div class="noChangeImg" @click="changeHeadImg()">
                取消
            </div>
        </div>
      
      
  </div>
</template>

<script>
import headNav from '../components/headNav/HeadBar'
import cropper from "../components/cropper/cropper"
import {mapState, mapGetters } from 'vuex'
import utils from '../assets/utils'
export default {
    data () {
        return {
            maskShow: false,
            screenshotImage: ''
        }
    },
    mounted() {
        console.log(this.userinfo);
        
    },
    computed: {
        ...mapState({
            token: state => state.auth.token,
            name: state => state.auth.userInfo.name,
            major: state => state.auth.userInfo.major,
            cls: state => state.auth.userInfo.cls,
            imgUrl: state => state.auth.imgUrl,
            gender: state => {
                if(state.auth.userInfo.gender!=1){
                    return '女'
                }
                else{
                    return '男'
                }
            },
            email: state => state.auth.userInfo.email,
            sno: state => state.auth.userInfo.sno,
            photoAPI: state => state.auth.photoAPI,
        }),
        ...mapGetters([
            'photoAPI',
            'imgUrl'
        ])
    },
    components: {
        headNav,
        cropper,
    },
    methods: {
        back () {
            this.$router.go(-1)
        },
        changeNickname (){
            this.$router.push('/nickname');
        },
        changeHeadImg (){
            this.maskShow = !this.maskShow;
            console.log(this.imgUrl)
        },
        async shareHandle () {
            const opts = {
                useCORS: true
            }
            const ele = this.$refs.screenshot
            const canvas = await html2canvas(this.$refs.screenshot, opts)
            this.screenshotImage = canvas.toDataURL('image/jpg')
        }
    }
}
</script>

<style scoped>
    .info{
      position:relative;
      top:75px;
      font-size: 14px;
      color:#848484;
      background-color: #ffffff;
      
      padding-top:10px;
    }
    .mask{
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: #000;
    opacity: 0.3;
    } 
    .child{
        position:fixed;
        width: 100%;
        height: 100%;
        top: 55px;
        background: #F6F6F5;
    }
    .name,.major,.cls,.gender,.nickname,.academy,.sno{
      height:30px;
      border-bottom: 1px solid #bdbdbd;
      margin-left:20px;
      margin-top:10px;
      margin-right: 20px;
    }
    .email{
      height:30px;
      margin-left:20px;
      margin-top:10px;
      margin-right: 20px;
      border-bottom: 1px solid #bdbdbd;
    }
    .y{
      float: left;
      width: 80px;
      margin-right: 40px;
    }
    .ch{
      float: right;
      color:#4A4A48;
      font-weight: bold;
    }
    .headImg{
        position: relative;
        left:50%;
        top:65px;
        width: 60px;
        height:60px;
        margin-left:-30px;
        border-radius: 100%;
    }
    .nickName{
        position: relative;
        top:65px;
        width: 100%;
        text-align: center;
        font-size: 16px;
    }
    .information{
        background-color: #F6F6F5
    }
    .changeImg{
        font-size: 20px;
        width:100%;
        text-align:center;
        line-height:50px;
        border-bottom: 1px solid #bdbdbd;
        color:#4285f4;
    }
    .noChangeImg{
        font-size: 20px;
        width:100%;
        text-align:center;
        line-height:50px;
        color:#4285f4;
    }
</style>