<template>
  <div id="star">
  	<div class="evaluat-content">
      <div class="cardTitle">{{cardTitle}}</div>
      <div class="thread"></div>
      <div class="star-content common-padding">
        <div class="title">{{actTitle}}</div><!-- 星级评价 -->
          <img :src="starCount >= 1 ? imgStar:imgStarInvert" @click="starClick(1)">
          <img :src="starCount >= 2 ? imgStar:imgStarInvert" @click="starClick(2)">
          <img :src="starCount >= 3 ? imgStar:imgStarInvert" @click="starClick(3)">
          <img :src="starCount >= 4 ? imgStar:imgStarInvert" @click="starClick(4)">
          <img :src="starCount >= 5 ? imgStar:imgStarInvert" @click="starClick(5)">       
      </div>
      <div class="evaluat-tab"><!-- 标签选择 -->
	      <div class="tab-item" v-bind:key="qus.quskey" v-for="qus in questionList[starCount]" @click="tagClick">
	      	<div class="qusName" choosed="false">{{ qus.name }}</div>
	      </div>
	    </div>
	    <div class="comment">  <!-- 自己的评价 -->
  	    <textarea  class="textComment" rows="5" cols="20" placeholder="可在此留下你的评价" maxlength="100" v-model="text"></textarea>
        <span class="textlength">{{ textLen }}</span>
      </div>
      <div class="submit"><!-- 提交按钮 -->
        <input type="button" value="匿名提交" @click="submit()">
      </div>
  	</div>
  </div>
</template>

<script>
import imgStar from './star.png'
import imgStarInvert from './star-invert.png'
import {mapState, mapGetters } from 'vuex'

export default {
  data () { // 组件内部数据
    return {
      cardTitle:'评价',
    	imgStar,
    	imgStarInvert,
			starCount: 0,
			text:'',
      textLen: 100
    }
	},
	props: ['actTitle','questionList', 'actID'],
	computed: {

  },
  methods: { // 内部方法
  	starClick (val) {
  		this.starCount = val
  	},
  	tagClick(e) {
  		let el = e.target
  		if (el.getAttribute('choosed') === 'false') {
        el.setAttribute('choosed', 'true')
        el.style.color = '#4A4A48'
        el.style.border = '1px solid rgba(74, 74, 72, 1)'
      } else if (el.getAttribute('choosed') === 'true') {
        el.setAttribute('choosed', 'false')
        el.style.color = '#bdbdbd'
        el.style.border = '1px solid #bdbdbd'
      } else {
      }
    },
    submit(){
		
    }
  }
}
</script>
<style scoped>
.evaluat-content {
    padding-left: 20px;
    padding-right:20PX;
    background: #FFFFFF;
    text-align: center;
  }
  .cardTitle{
    height: 20px;
    color: rgba(16, 16, 16, 1);
    font-size: 18px;
    text-align: center;
    font-family: PingFangSC-regular; 
    margin-top: 10px;
  }
  .thread{
    border-bottom: 1px solid rgba(187, 187, 187, 1);
    margin-top:10px;
    margin-bottom: 20px;
  }
  .star-content {
		padding-left:20px;
    height: 100px;
    text-align: center;
  }
  .title{
    width: auto;
    height: 20px;
    color: rgba(74, 74, 72, 1);
    font-size: 16px;
    text-align: center;
    font-family: PingFangSC-bold;
    margin-bottom: 20px;
  } 
  img {
    margin-right: 20px;
    width: 28px;
    vertical-align: middle;
  }
  .evaluat-tab {
		padding-left:20px;
    height:120px;
    width: auto;
  }
  .evaluat-tab .tab-item {
    width: 50%;
    height:auto;
    float: left;
    text-align: center;
  }
  .qusName{
  	margin: 5px 5px 5px 5px;
    border-radius: 10px;
    border :1px solid rgba(74, 74, 72, 1);
    vertical-align: middle;
    font-size: 12px; 
    width: 120px;
    height:40px;
    color:#4A4A48 100%;
    background-color: #FFFFFF;
    position: relative;
  }
  .comment {
	  margin-bottom: 10px;
  }
  .textComment {
    width: 90%;
    margin-top:10px;
    font-size: 13px;
    letter-spacing: 1px;
    background-color: rgba(246, 246, 245, 1);
    border: 1px solid rgba(255, 255, 255, 0);
    border-radius: 10px;
    margin-bottom: 20px;
  }
  .textlength {
    font-size: 13px;
    margin-left: 245px;
    margin-top: -42px;
    display: block;
    height: 20px;
  }
  .submit input[type='button']{  
    width: 90px;
    height: 29px;
    background-color:#4A4A48 100%;
    color: #FFFFFF 100%;
    border-radius: 3px;
    font-size: 14px;
    text-align: center;
    font-family: Arial;
  }
</style>