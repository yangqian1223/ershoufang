<template>
  <div class="indexstyle">
    <div>444</div>
    <!-- 经纪人介绍开始 -->
    <div class="jjr">
      <div class="jjr_kuang">
        <div class="top_js">
          <div class="lelf_jj">
              <h1>杨女士</h1>
              <span>综合经纪人</span>
          </div>
          <div class="right_jj">
            <image :src="img1" />
            <p>兴安府经纪人</p>
          </div>
        </div>

        <div class="youshis">
            <span>博学优秀</span>
        </div>

        <div class="pingjia">
          <ul>
            <li>
              <h2>22</h2>
              <p>服务人数</p>
            </li>
            <li>
              <h2>77</h2>
              <p>成交房源</p>
            </li>
            <li>
              <h2>4-5</h2>
              <p>从业年限</p>
            </li>
            <li>
              <h2>5.0/<span>5.0</span></h2>
              <p>客户评分</p>
            </li>
          </ul>
        </div>
         
      </div>
    </div>
    <!-- 经纪人介绍结束 -->

    <!-- 更多推荐开始 -->
    <div class="tuijian">
      <!-- 标题 -->
      <div class="tj_bt">
        <div class="bt_lelf">更多推荐</div>
        <div class="bt_right">
          <div class="fang" :class="{'fz' :tab==1}" @click="tuijian(1)">二手房</div>
          <div class="fang" :class="{'fz' :tab==2}" @click="tuijian(2)">新房</div>
          <div class="fang" :class="{'fz' :tab==3}" @click="tuijian(3)">租房</div>
        </div>
      </div>
      <!-- 内容切换开始 -->
      <div class="nr_list">
        <!-- 二手房开始 -->
        <div class="secondary" v-if="tab==1">
          
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
              <div class="youshiesf" v-for="(f, inds) in item.advantage" :key="inds">
                <div class="youshiesf1" v-if="inds<2">{{f.id}}</div>
              </div>
              <div class="clear"></div>
              <div class="m-x"><p class="money">{{item.price}}万</p><p class="money1">{{item.price1}}元/平</p></div>
            </div>
            <div class="clear"></div>
          </div>

        </div>
        <!-- 二手房结束 -->
        <!-- 新房开始 -->
        <div class="newhouse" v-else-if="tab==2">

          <div class="intention-mt" v-for="(item, index) in newslist" :key="index">
            <image :src="item.img7" class="new-image" mode="scaleToFill"/>
            <div class="intention-right">

              <div class="bt_ri">
                <h1>{{item.title}}</h1>
                <p>在售</p>
                <div class="clear"></div>
              </div>

              <div class="youshi" v-for="(f, inds) in item.advantage1" :key="inds">
                <div class="youshi2" v-if="inds<4">{{f.id}}</div>
              </div>
              <div class="clear"></div>

              <div class="m-x clear">
                <p class="money">{{item.price}}元/m²</p><p class="money1">建面{{item.price1}}元/平</p>
              </div>

            </div>
            <div class="clear"></div> 
          </div>

        </div>
        <!-- 新房结束 -->
        <!-- 租房开始 -->
        <div class="Renthouse" v-else>

          <div class="h-mt" v-for="(item, index) in house1" :key="index">
            <image :src="item.img6" class="new-image" mode="scaleToFill"/>
            <div class="r_wz">
              <div class="bt_s">{{item.title}}</div>
              <div class="jieshao" v-for="(w, ind) in item.area" :key="ind">
                <span>{{w.model}}</span>/
                <span>{{w.size}}m²</span>/
                <span>{{w.direction}}</span>/
                <span>{{w.name}}</span>
              </div>
              <div class="youshiesf" v-for="(f, inds) in item.advantage" :key="inds">
                <div class="youshiesf1" v-if="inds<2">{{f.id}}</div>
              </div>
              <div class="clear"></div>
              <div class="m-x"><p class="money">{{item.price}}万</p><p class="money1">{{item.price1}}元/平</p></div>
            </div>
            <div class="clear"></div>
          </div>

        </div>
        <!-- 租房结束 -->
      </div>
      <!-- 内容切换结束 -->

    </div>
    
    <!-- 更多推荐结束 -->

 
   
  

  </div>
</template>

<script>
export default {
  data () {
    return {
      img1: 'http://vip.yijienet.com/tt/img1.jpg',
      tab:1,
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
      newslist: [
            { 
              img7:'http://vip.yijienet.com/tt/img1.jpg', title:'城投佳境',
              advantage1: [
                { id:'别墅'},
                { id:'小户型'},
                { id:'公交直达'},
                { id:'视频看房'}
              ],
              price:555, price1:6500,
            }

      ],
      house1: [
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
   
 


    }
  },
 methods: {
  tuijian(index){
    this.tab = index;
  } 
 }


 

   

}
</script>

<style scoped>
.clear {
  clear: both;
  height: 0;
  display: block;}
.hsxian{ width: 100%; height:10px; background: #f8f8fa;}
.indexstyle{width: 100%; margin: 0 auto; background: #fff;}
 
/* 经纪人开始 */
.jjr{width: 140%; height: 500rpx; position: absolute; left: -20%; top: 0; z-index: -1; content: ''; border-radius: 0 0 50% 50%; background: linear-gradient(#3b4671, #293359); }
.jjr_kuang{ width:64%; margin-left:18%; margin-right:18%; background: linear-gradient(#fef1d9, #f2ddb5); border-radius:3%; margin-top:10%; padding-bottom:7%; }
.top_js{ width:86%; overflow: hidden; margin-left:7%; margin-right: 7%; padding-top:10%;}
.lelf_jj{ float: left; display: flex; flex-direction: row; width: 60%; margin-top:6%;}
.lelf_jj h1{ font-size:45rpx; font-weight: bold;}
.lelf_jj span{ font-size:30rpx; margin-left: 3%; margin-top: 3%;}

.right_jj{ float: right; position: relative;   }
.right_jj image{ width: 150rpx; height: 150rpx; border-radius: 50%;}
.right_jj p{ padding:3rpx 3rpx 3rpx 3rpx; text-align: center; background: linear-gradient(#fff4d9, #ffe7b1); border: 1px #deca99 solid; color: #91783d; font-size: 20rpx;border-radius:150rpx; position: absolute; top:75%; left:7%;}

.youshis{ width:86%; margin-left:7%; margin-right:7%;}
.youshis span{ font-size: 27rpx;padding:3rpx 7rpx 3rpx 7rpx; border: 1px #eadabd solid; color: #6d5c3c; }

.pingjia{ width:92%; margin-left:5%; margin-right:3%; margin-top:7%;}
.pingjia ul{ overflow: hidden;}
.pingjia ul li{ width:18%; float: left; margin-left:3%; margin-right:3%; }
.pingjia ul li h2{ font-size: 40rpx; font-weight: bold; color: #372b17;}
.pingjia ul li h2 span{ font-size: 24rpx;}
.pingjia ul li p{ font-size: 26rpx; color: #877e67; margin-top:2%;}

/* 更多推荐开始 */
.tuijian{ width: 90%; margin-left: 5%; margin-right: 5%; margin-top:85%;}
.tj_bt{ margin-top: 2%; overflow: hidden;}
.bt_lelf{ float: left; font-size: 35rpx; font-weight: bold;}
.bt_right{ float: right; font-size:30rpx; display: flex; flex-direction: row; width:45%;}
.fang{ margin-left:8%;}
.fz{ color: rgb(15, 133, 230);}

/* 内容切换开始 */
.nr_list{ width: 100%;}
/* 二手房 */
.secondary{ width: 100%;}
.h-mt{ width:100%;  margin-top:30rpx; padding-bottom: 5%; border-bottom: 1px #e9e9e9 solid;}
.h-mt image{ float: left; width: 40%; height: 180rpx; border-radius: 10rpx;}
.h-mt .r_wz{ float:right; width: 57%;}
.h-mt .r_wz .bt_s{font-size: 34rpx; font-weight: bold; margin-right:10rpx;}
.jieshao{ font-size: 26rpx; color: #000; margin-top:10rpx;}
.youshiesf1{ float: left; width:90rpx; height:40rpx; line-height: 40rpx; border-radius:3px; background: #edf0f3; color:#849aae; font-size: 25rpx; text-align: center; margin-top:10rpx; margin-right: 10rpx;}
.m-x{ margin-top: 10rpx; }
.m-x p{ float: left;}
.m-x p.money{ font-size: 34rpx; color: #fa5741; font-weight: 900; margin-right: 5rpx;}
.m-x p.money1{ font-size:26rpx; color:#a4a4a4; margin-top: 10rpx; }

/* 新房 */
.intention-mt{ padding-bottom:15px; border-bottom: 1px rgb(236, 236, 236) solid; margin-top: 15px;}
.intention-mt image{ float: left; width:30%; height:150rpx; border-radius: 5px;}
.intention-mt .intention-right{ float:right; width:67%; }
.intention-mt .intention-right .bt_ri h1{ float: left; font-size: 34rpx; font-weight: bold; margin-right:4rpx;}
.intention-mt .intention-right .bt_ri p{ float: right; width:60rpx; height:35rpx; line-height: 35rpx; background: #0a8de4; text-align: center; font-size: 24rpx;  margin-right:10rpx; color: #fff; border-radius: 3px; margin-top:1%;}
.youshi2{ float: left; padding: 3rpx 8rpx 3rpx 8rpx; border-radius:3px; border: 1px #dbdbdb solid; color:#8b8b8b; font-size: 22rpx; text-align: center; margin-top:15rpx; margin-right: 10rpx;}
.m-x{ margin-top: 15rpx; }
.m-x p{ float: left;}
.m-x p.money{ font-size: 30rpx; color:#df573d; font-weight: 900; margin-right: 5rpx;}
.m-x p.money1{ font-size:24rpx; color:rgb(187, 187, 187); margin-top: 10rpx; }



</style>
