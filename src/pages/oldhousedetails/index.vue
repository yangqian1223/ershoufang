<template>
  <div class="indexstyle">


    <!-- 图片轮播 -->
    <div class="lunbo">
      <swiper class="swiper" @change="djimg" >
        <block v-for="(item, index) in movies" :key="index">
          <swiper-item>
            <image :src="item.img1" class="slide-image" mode="scaleToFill"/>
          </swiper-item>
        </block>
      </swiper>
      <div class="imageCount">{{current+1}}/{{movies.length}}</div>
    </div>
    <!-- 图片轮播 -->




    <!-- 二手房信息开始 -->
    <div class="ershou">
      <div>
        <div class="features"  v-for="(dada, inds) in secondary" :key="inds">
            <p v-if="inds<3">{{dada.id}}</p>
        </div>
        <div class="moredj">点击进入</div>
      </div>
      <div class="biaoti">{{title}}</div> 
      <div class="mianji">
          <div class="lelf_mj">
            <h1>{{price}}万</h1>
            <p>售价</p>
          </div>
          <div class="center_mj">
            <h1>{{room}}</h1>
            <p>房型</p>
          </div>
          <div class="right_mj">
            <h1>{{areas}}m²</h1>
            <p>建筑面积</p>
          </div>
      </div>
      <div class="xinxi">
          <ul>
            <li>单价：<span>{{price1}}元/平</span></li>
            <li>挂牌：<span>{{listed}}</span></li>
            <li>朝向：<span>{{toward}}</span></li>
            <li>楼层：<span>{{floor}}</span></li>
            <li>楼型：<span>{{Floortype}}</span></li>
            <li>电梯：<span>{{elevator}}</span></li>
            <li>装修：<span>{{decorate}}</span></li>
            <li>年代：<span>{{sniandai}}</span></li>
            <li>用途：<span>{{usey}}</span></li>
            <li>权属：<span>{{ownership}}</span></li>
          </ul>
          <div><p>小区：<span>{{community}}</span></p><image :src="rootImg1" class="slide-image" mode="scaleToFill"/></div>
          <div><p>其他：<span>{{other}}</span></p><image :src="rootImg1" class="slide-image" mode="scaleToFill"/></div>
          <div><p>首付预算：<span>{{budget}}</span></p><image :src="rootImg1" class="slide-image" mode="scaleToFill"/></div>
          <div><p>风险提示：<span>{{warning}}</span></p><image :src="rootImg1" class="slide-image" mode="scaleToFill"/></div>
      </div>

    </div>
    <!-- 二手房信息结束 -->

    <!-- 评价分类开始 -->
    <div class="pingjia">
      <div class="hx_bt">
        <p>房源评价</p>
      </div>

      <div class="anniu">
          <scroll-view scroll-x class="top">
              <div class="an_qh" :class="{'tabbar-bottom':currentTab==index}" v-for="(item,index) in tabBar" :key="index" @click="clickTab(index)" >
                  <div v-if="currentTab==index"><image :src="item.img2" class="slide-image" mode="scaleToFill"/></div>
                  <div v-else><image :src="item.img1" class="slide-image" mode="scaleToFill"/></div>
                  <p>{{item.title}}</p>
              </div>
          </scroll-view>
          <swiper :current="currentTab" @change="changeTab">
            <swiper-item>
            <div class="neir">核心卖点核心卖点核心卖点核心卖点核心卖点核心卖点</div>
            </swiper-item>
            <swiper-item>
            <div class="neir">核心卖点核心卖点核心卖点核心卖点核心卖点核心卖点</div>
            </swiper-item>
          </swiper>

      </div>

    </div>
    <!-- 评价分类结束 -->


    <!-- 推荐经纪人开始 -->
    <div class="jingjiren">
      <div class="hx_bt">
        <p>推荐经纪人</p>
        <span>查看更多</span>
      </div>

      <div class="guwen">

          <div class="guwen_list" v-for="(item, index) in guwenlists" :key="index">
            <div class="left_g">
              <image :src="item.img8" class="slide-image" mode="scaleToFill"/>
              <div class="neirong">
                <div>
                  <h1>{{item.name}}</h1>
                  <span>满意度{{item.fraction}}分</span>
                  <div class="clear"></div>
                </div>
                <p>{{item.neirong}}</p>
              </div>
            </div>
            <div class="right_g">
              <p><image :src="item.img9" class="slide-image" mode="scaleToFill" /></p>
              <p><image :src="item.img10" class="slide-image" mode="scaleToFill" /></p>
            </div>
          </div>

        </div>

    </div>
    <!-- 推荐经纪人结束 -->


    <!-- 猜你喜欢开始 -->
    <div class="jingjiren">
      <div class="hx_bt">
        <p>猜你喜欢</p>
        <span>查看更多</span>
      </div>

      <div class="xihuan">
        <scroll-view scroll-x="true" style="width: 100%" class="image-group">
          <div class="likelist" v-for="(item, cai) in likes" :key="cai">
            <div class="tupian_l">
              <image :src="item.img5" mode="scaleToFill"/>
              <div class="guanzhu">{{item.num}}人关注</div>
            </div>
            <div class="wenzi_r">
              <h1>{{item.title}}</h1>
              <div class="ys_kuai" v-for="(f, inds) in item.tese" :key="inds">
                <p>{{f.id}}</p>
              </div><div class="clear"></div>
              <div class="jiaqian"><span class="jq1">{{item.wan}}万</span><span class="jq2">{{item.wan1}}元/平</span></div>
            </div>
          </div>
              
        </scroll-view>
      </div>
 

    </div>
    <!-- 猜你喜欢结束 -->


    <!-- 位置及周边配套开始 -->
    <div class="jingjiren">
      <div class="hx_bt">
        <p>位置及周边配套</p>
      </div>
      <div class="map_img">
          <map id="map" :longitude="longitude" :latitude="latitude" :scale="14" :controls="controls" 
          bindcontroltap="controltap" :markers="markers" :bindmarkertap="markertap" :polyline="polyline"
          :bindregionchange="regionchange" show-location style="width: 100%; height: 220px;"
          :enable-scroll="false" :enable-zoom="false" @click="clickAdress"></map>
      </div>

    </div>
    <!-- 位置及周边配套结束 -->


    <!-- 小区项目信息开始 -->
    <div class="Projectks">
      <div class="k1">
          <div class="hx_bt">
            <p>小区项目信息</p>
            <span>小区详情</span>
          </div>
          <div class="xiangmu">
            <div class="l_xiangmu">
              <h1>参考均价：<span>{{reference}}元/平</span></h1>
              <p>建筑年代：{{years}}年建</p>
              <p>房栋总数：{{building}}栋</p>
              <p>房屋总数：{{housing}}户</p>
            </div>
            <div class="r_xiangmu">
              <image :src="img11" class="slide-image" />
            </div>
          </div>
      </div>

      <div class="k2">
          <div class="hx_bt1">
            <p>同小区成交（{{cj_num}}）</p>
            <span>更多成交</span>
          </div>
          <div class="chengjiao_list">
            <ul>
              <li v-for="(item, cj) in chengjiao" :key="cj">
                <div class="cj_le">
                  <h2><span>{{item.chengj1}}</span>/<span>{{item.chengj2}}平米</span>/<span>{{item.chengj3}}</span></h2>
                  <p><span>单价{{item.chengj4}}元/平</span>，<span>{{item.chengj5}}成交</span></p>
                </div>
                <div class="cj_ri">{{item.chengj6}}万</div>
              </li>
            </ul>
          </div>
      </div>


      <div class="k2">
          <div class="hx_bt1">
            <p>同小区房源</p>
            <span>查看更多</span>
          </div>
          <div class="fangyuan_list">
            <scroll-view scroll-x="true" style="width: 100%" class="image-group">
              <div class="fang_list" v-for="(item, fy) in fangyuan" :key="fy">
                <image :src="img11" class="slide-image" />
                <h3><span>{{item.fangy1}}</span>/<span>{{item.fangy2}}m²</span>/<span>{{item.fangy3}}</span></h3>
                <p><span class="dj1">{{item.fangy4}}万元</span><span class="dj2">{{item.fangy5}}元/平</span></p>
              </div>
            </scroll-view>
          </div>
      </div>

     </div>
    <!-- 小区项目信息结束 -->


    <!-- 推荐房源开始 -->
    <div class="jingjiren">
      <div class="hx_bt">
        <p>推荐房源</p>
      </div>

      <div class="nr-house">

        <div class="h-mt" v-for="(item, index) in house" :key="index">
          <image :src="item.img6" class="new-image" mode="scaleToFill"/>
          <div class="r_wz">
            <div class="bt_s">{{item.title}}</div>
            <div class="jieshao" v-for="(w, ind) in item.area" :key="ind">
              <span>{{w.model}}</span>/
              <span>{{w.size}}m²</span>/
              <span>{{w.direction}}</span>/
              <span>{{w.name}}</span>
            </div>
            <div class="youshi" v-for="(f, inds) in item.advantage" :key="inds">
              <div class="youshi1" v-if="inds<2">{{f.id}}</div>
            </div>
            <div class="clear"></div>
            <div class="m-x"><p class="money">{{item.price}}万</p><p class="money1">{{item.price1}}元/平</p></div>
          </div>
          <div class="clear"></div>

        </div>

      </div>
 

    </div>
    <!-- 推荐房源结束 -->



    <!-- 底部按钮开始 -->
    <div class="footer">
      <div class="left_foot">

        <div class="guanzhus">
          <button class="gzdianji" @click="gz_dj" v-if="gztu_img==0" ><image :src="img10" /></button>
          <button class="gzxianshi" @click="gz_dj" v-else ><image :src="img12" /></button>
          <p>关注</p>          
        </div>

        <button open-type="share" class="fenxiangs">
          <image :src="img13" class="slide-image" />
          <p>分享</p>
        </button>
        <button class="fenxiangs">
          <image :src="img14" class="slide-image" />
          <p>预约</p>
        </button>
      </div>
      <div class="right_foot">
        <div class="Report">打电话</div>
        <div class="Telephone">加微信</div>
      </div>
    </div>
    <!-- 底部按钮开始 -->









  </div>
</template>

<script>
export default {
  data () {
    return {
      secondary: [
        { id:'满五年'},
        { id:'VR看房'},
        { id:'随时看房'}
      ],
      title:"城投佳境随时看房 双阳台 高层楼采光好",
      price:150,
      room:"二室一厅",
      areas:99.5,
      price1:6200.5,
      listed:"2020-12-1",
      toward:"西北",
      floor:20,
      Floortype:"塔楼",
      elevator:"有电梯",
      decorate:"简装",
      sniandai:"2004年",
      usey:"普通住宅",
      ownership:"商品房",
      community:"长兴小区",
      other:"产权年限",
      budget:"",
      warning:"请您请注意保障自身权益",
      rootImg1: "/static/images/jt1.jpg",
      guwenlists: [
            {
              img8:'http://vip.yijienet.com/tt/img1.jpg',name:'王先生',fraction:5,neirong:'我带看过本房，清楚本房特色',img9:'/static/images/wx.png',img10:'/static/images/dh.png',
            }
      ],
      likes: [
        {
          img5:'http://vip.yijienet.com/tt/img1.jpg',num:15,title:'城投佳境随时看房 双阳台',wan:150,wan1:6587,
          tese: [
            { id:'满五年'},
            { id:'有电梯'},
            { id:'简装'}
          ]
        },
        {
          img5:'http://vip.yijienet.com/tt/img1.jpg',num:15,title:'城投佳境随时看房 双阳台',wan:150,wan1:6587,
          tese: [
            { id:'满五年'},
            { id:'有电梯'},
            { id:'简装'}
          ]
        },
        {
          img5:'http://vip.yijienet.com/tt/img1.jpg',num:15,title:'城投佳境随时看房 双阳台',wan:150,wan1:6587,
          tese: [
            { id:'满五年'},
            { id:'有电梯'},
            { id:'简装'}
          ]
        }
      ],
      tabBar: [
          {img1:'/static/images/an1.png',img2:'/static/images/an1s.png',title:'核心卖点'},
          {img1:'/static/images/an1.png',img2:'/static/images/an1s.png',title:'小区介绍'},
          {img1:'/static/images/an1.png',img2:'/static/images/an1s.png',title:'适宜人群'},
          {img1:'/static/images/an1.png',img2:'/static/images/an1s.png',title:'周边配套'},
          {img1:'/static/images/an1.png',img2:'/static/images/an1s.png',title:'费用介绍'},
          {img1:'/static/images/an1.png',img2:'/static/images/an1s.png',title:'交通出行'},
      ],
      currentTab: 0,
      movies: [
        {img1: 'http://vip.yijienet.com/tt/img1.jpg'},
        {img1: 'http://vip.yijienet.com/tt/img1.jpg'},
        {img1: 'http://vip.yijienet.com/tt/img1.jpg'},
        {img1: 'http://vip.yijienet.com/tt/img1.jpg'}
      ],
      current: 0,
      reference:1280,
      years:20,
      building:180,
      housing:8900,
      img11:'http://vip.yijienet.com/tt/img1.jpg',
      chengjiao:[
        {chengj1:'2室一厅',chengj2:80.5,chengj3:'北',chengj4:8900,chengj6:77}
      ],
      fangyuan:[
        {fangy1:'2室一厅',fangy2:80.5,fangy3:'北',fangy4:130,fangy5:6500.5},
        {fangy1:'2室一厅',fangy2:80.5,fangy3:'北',fangy4:130,fangy5:6500.5},
        {fangy1:'2室一厅',fangy2:80.5,fangy3:'北',fangy4:130,fangy5:6500.5}
      ],
      house: [
        { 
          img6:'http://vip.yijienet.com/tt/img1.jpg', title:'城投佳境',
          area: [
            { model:'2室1厅', size:90, direction:'西北', name:'城投佳境'}
          ],
          advantage: [
            { id:'满五年'},
            { id:'满五年'},
            { id:'满五年'}
          ],
          price:555, price1:6500,


        }
      ],
      img10: "/static/images/gz.png",
      img12: "/static/images/xin.png",
      img13: "/static/images/fx.png",
      img14: "/static/images/yy.png",
      gztu_img:0,
      



 





    }
  },
  methods: {
        clickTab(e) {
             this.currentTab = e;
             
        },
        changeTab(e) {
             this.currentTab = e.mp.detail.current;
         },
         djimg(e) {
           this.current = e.target.current;
         },
         gz_dj(){
          if(this.gztu_img==1){
            this.gztu_img=0;
          }else{
            this.gztu_img=1;
          }
         }

 
  }



}
</script>

<style scoped>
.clear {
  clear: both;
  height: 0;
  display: block;}
.fl{ float: left;}
.fr{ float: right;}
.hsxian{ width: 100%; height:10px; background: #f8f8fa;}
.indexstyle{width: 100%; margin: 0 auto; background: #fff;}


.lunbo{ width: 100%; height: 500rpx;}
.swiper{ width: 100%; height: 100%;}
.lunbo image{ width: 100%; height: 100%;}
.imageCount {
  width:100rpx;
  height:45rpx;
  background-color: rgba(0, 0, 0, 0.4);
  border-radius:40rpx;
  line-height:50rpx;
  color:#fff;
  text-align:center;
  font-size:24rpx;
  position:relative;
  left:42%;
  bottom:70rpx;
}







.ershou{ width: 90%; padding-left: 5%; padding-right: 5%; margin-top: 5%; border-bottom: 10px #efefef solid;}
.ershou div{overflow: hidden;}
.features{ float: left;}
.features p{float: left; font-size: 24rpx; padding: 2rpx 10rpx 2rpx 10rpx; background: #edf0f3; color: #849aae; margin-right: 3px; border-radius: 3px;}
.moredj{float: right;font-size: 24rpx;}
.biaoti{ font-size:43rpx; font-weight: bold; margin-top: 3%; }
.mianji{ overflow: hidden; margin-top:3%; }
.lelf_mj{ float: left; width: 29%; border-right: 1px rgb(235, 235, 235) solid;}
.center_mj{ float: left; width:30%; border-right: 1px rgb(235, 235, 235)  solid; margin-left:4%;}
.right_mj{ float: right; width: 32%; margin-left:4%;}
.lelf_mj h1,.center_mj h1,.right_mj h1{ color: #fa5741; font-size: 38rpx; font-weight: bold; }
.lelf_mj p,.center_mj p,.right_mj p{ color: #a7a7a7; font-size: 26rpx;}

.xinxi{ margin-top: 3%;}
.xinxi ul{ overflow: hidden; margin-bottom: 15rpx; }
.xinxi ul li{ float: left; width: 50%; font-size:30rpx; color: rgb(160, 160, 160); line-height:65rpx;}
.xinxi ul li span{ color: #000;}
.xinxi div{ font-size:30rpx; color: rgb(160, 160, 160); line-height:40rpx; width: 100% !important; overflow: hidden;}
.xinxi div P{ float: left; width: 70%;}
.xinxi div span{ color: #000;}
.xinxi div image{ float: right; width: 9px; height: 15px; position: relative; top: -18px;}


.pingjia{width: 90%; padding-left: 5%; padding-right: 5%; margin-top: 5%; padding-bottom: 5%; border-bottom: 10px #efefef solid;}
.hx_bt{ width:100%; overflow: hidden;}
.hx_bt p{ float: left; font-size:35rpx; font-weight: bold;}
.hx_bt span{ float: right; font-size:25rpx;}



.jingjiren{width: 90%; padding-left: 5%; padding-right: 5%; margin-top: 5%; padding-bottom: 5%; border-bottom: 10px #efefef solid;}
.guwen{ width:100%; margin-top:5%;}
.guwen_list{ width: 100%; margin-top:2%; overflow: hidden;}

.left_g{ float: left; width:75%;}
.left_g image{ float: left; width:55px; height:55px; border-radius: 50%; margin-right: 2%;}
.neirong{ float: left; width:70%; margin-top: 2%; }
.neirong div h1{float: left; font-size:32rpx; font-weight: bold; margin-right: 5px; }
.neirong div span{ float: left; font-size: 22rpx; padding:1rpx 2rpx 1rpx 2rpx; border: 1px #f86577 solid; color: #f86577; text-align: center; border-radius: 3px; }
.neirong p{ font-size: 27rpx; color: #969ca8; margin-top:2%;}

.right_g{ float: right; margin-top:10px; width: 25%; }
.right_g p{ float: left;margin-left:10%;}
.right_g image{ width:30px; height:30px;}



 
.image-group {
  display: flex;
  white-space: nowrap;
  margin-top:10rpx;
}
.likelist{ overflow: hidden; margin-top: 5%;margin-right:6%; width:80%; height:80px;display: inline-block;}
.tupian_l{ float: left;width:30%;}
.tupian_l image{ width:100%; height: 150rpx;}
.tupian_l .guanzhu{ width: 100%; height:40rpx; background:rgba(20, 20, 20, 0.616); text-align: center; line-height:40rpx; position: relative; top: -20px; color: #fff; font-size: 24rpx;}
.wenzi_r{ float: right; width: 65%;}
.wenzi_r h1{ font-size:32rpx; font-weight: bold;}
.ys_kuai{ width:100%; margin-top: 3%; }
.ys_kuai p{font-size: 24rpx; padding: 2rpx 5rpx 2rpx 5rpx;  background: #edf0f3; color: #849aae; margin-right: 3px; border-radius: 3px; margin-right: 3px; float: left;}
.wenzi_r .jiaqian{ margin-top: 3%;}
.wenzi_r .jiaqian span.jq1{ font-size: 32rpx; color: #fa5741; margin-right: 10px; font-weight: bold;}
.wenzi_r .jiaqian span.jq2{ font-size:26rpx; color: #9e9e9e; }



.map{background: rgba(255,255,255,0.8);padding: 20rpx;margin-top: 25rpx;
    box-sizing: border-box;border-radius: 10rpx;position: relative;top: -50rpx;}
.map_img{width:100%; margin-bottom: 50rpx; margin-top: 3%;}
.map_img>image{width: 100%;height: 100%; margin-top: 3%;}



.anniu{ width: 100%; margin-top: 10px;}
.top {width: 100%; line-height: 42px;white-space: nowrap;position: relative;background: #fff; overflow: hidden; }
.an_qh{ width:90px; height: 80px; background: rgb(231, 231, 231);color: #000; display: inline-block; margin-right: 10px; border-radius:5px;}
.an_qh image{width:25px; height:25px; margin: 0 auto; display: block; margin-top:18%;}
.an_qh p{font-size:26rpx; line-height: 30px; text-align: center;}
.tabbar-bottom { width:90px; height:80px; background:#2e72f1;color: #fff;}
.neir{ font-size: 26rpx; margin-top: 10px; height: 150px; overflow: hidden;}
.anniu swiper{ height:80rpx !important;} 


.Projectks{width: 90%; padding-left: 5%; padding-right: 5%; margin-top: 5%; padding-bottom: 5%; border-bottom: 10px #efefef solid;}
.k1{padding-bottom: 15px; border-bottom: 1px rgb(235, 235, 235) solid; }
.xiangmu{ margin-top:5%; overflow: hidden; }
.l_xiangmu{ float: left; width:60%;}
.l_xiangmu h1{ font-size: 32rpx; font-weight: bold; margin-bottom: 5%;}
.l_xiangmu h1 span{ color: rgb(218, 0, 0);}
.l_xiangmu p{ line-height:20px; color: rgb(124, 124, 124); font-size: 26rpx;}
.r_xiangmu{ width: 40%; float: right;}
.r_xiangmu image{ width: 100%; height:200rpx;}

.k2{padding-bottom: 15px;margin-top: 5%; border-bottom: 1px rgb(235, 235, 235) solid; }
.hx_bt1{ width:100%; overflow: hidden;}
.hx_bt1 p{ float: left; font-size:32rpx; }
.hx_bt1 span{ float: right; font-size:24rpx;}
.chengjiao_list{ width: 100%; margin-top: 5%;}
.chengjiao_list ul li{ overflow: hidden;}
.chengjiao_list ul li .cj_le{ width: 60%; float: left;}
.chengjiao_list ul li .cj_le h2{ font-size: 30rpx;}
.chengjiao_list ul li .cj_le p{ font-size: 24rpx; color: #ccc;}
.cj_ri{ float: right; font-size: 32rpx; font-weight: bold; color: rgb(233, 39, 39);}



.k3{ margin-top: 5%;}
.fangyuan_list{ width: 100%; margin-top: 5%;}
.fang_list{ overflow: hidden; margin-right:6%; width:58%; margin-right: 5%; height:380rpx;display: inline-block;}
.fang_list image{ width: 100%; height: 260rpx;}
.fang_list h3{ font-size: 30rpx; margin-top: 3%;}
.fang_list p{ font-size: 26rpx; margin-top: 3%;}
.fang_list p span.dj1{ font-size: 30rpx; font-weight: bold; color: rgb(253, 27, 27); margin-right: 2%;}
.fang_list p span.dj2{ font-size: 27rpx; color: rgb(146, 146, 146);}


/* 推荐房源 */
.house-s{width:100%; background: #fff; margin: 0 auto; height:190px; padding-top: 20px; margin-bottom:10px;}
.nr-house{ width:100%;  margin-top:15px;}
.nr-house image{ float: left; width: 40%; height: 180rpx;}
.nr-house .r_wz{ float:right; width: 57%;}
.nr-house .r_wz .bt_s{font-size: 34rpx; font-weight: bold; margin-right:10rpx;}
.jieshao{ font-size: 26rpx; color: #000; margin-top:10rpx;}
.youshi1{ float: left; width:90rpx; height:40rpx; line-height: 40rpx; border-radius:3px; background: #edf0f3; color:#849aae; font-size: 25rpx; text-align: center; margin-top:10rpx; margin-right: 10rpx;}
.m-x{ margin-top: 10rpx; }
.m-x p{ float: left;}
.m-x p.money{ font-size: 34rpx; color: rgb(192, 0, 0); font-weight: 900; margin-right: 5rpx;}
.m-x p.money1{ font-size:26rpx; color:#ccc; margin-top: 10rpx; }



.footer{ width: 100%; height: 120rpx; background: #fff;position: fixed;bottom: 0;}
.left_foot{ float: left; width:39%;height: 120rpx; margin-right:3%; margin-left: 3%;}

.left_foot .guanzhus{ float: left; width:33.3%; margin: 0 auto; background: #fff;overflow: inherit;border: none; padding: 0 !important;}
.left_foot .guanzhus image{ width:18px; height:18px;}
.left_foot .guanzhus p{ font-size: 26rpx; color: #000; position: relative; top:-12px; left:22%;}
 


.left_foot .fenxiangs{ float: left; width:33.3%; height: 25px; margin: 0 auto; background: #fff;overflow: inherit;border: none; padding: 0 !important;}
.left_foot button{border: none; padding: 0 !important; padding-left: 0 !important; padding-right: 0 !important;}
.left_foot button::after{border: none; padding: 0 !important;}
.left_foot .fenxiangs image{ width:18px; height:18px;}
.left_foot .fenxiangs p{ font-size: 26rpx; color: #000; position: relative; top: -20px;}




.right_foot{ float: right; width:55%; margin-top:7px;}
.Report{ float: left; width: 45%; background: #3dc28e; font-size: 28rpx; height:90rpx; line-height:90rpx; text-align: center; border-radius: 5px; color: #fff; margin-right: 5%;}
.Telephone{ float: right; width: 45%; background: #2e72f1; font-size: 28rpx; height:90rpx; line-height:90rpx; text-align: center; border-radius: 5px; color: #fff; margin-right: 5%;}




 </style>
