<template>
  <div>
    <div class="list">
      <div class="item">
        <div class="item_div borderBottom1" @click="pushPage(1)">
          <div>
            <h2>每日健康</h2>
            <p>每日三分钟<br >健康一辈子</p>
          </div>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#iconmeirijiankang"/>
          </svg>
        </div>
        <div class="item_div" @click="pushPage(4)">
          <div>
            <h2>中医体质</h2>
            <p>九种体质<br >辨识养生</p>
          </div>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#iconzhongyitizhi"/>
          </svg>
        </div>
      </div>
      <div class="item">
        <div class="item_div borderBottom1" @click="pushPage(2)">
          <div>
            <h2>症状自诊</h2>
            <p>健康问题<br >自助排查</p>
          </div>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#iconbuweizizhen"/>
          </svg>
        </div>
        <div class="item_div" @click="pushPage(5)">
          <div>
            <h2>疾病地理</h2>
            <p>居住地<br >常见病预防</p>
          </div>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#iconjibingdili"/>
          </svg>
        </div>
      </div>
      <div class="item">
        <div class="item_div borderBottom1" @click="pushPage(3)">
          <div>
            <h2>常见问题</h2>
            <p>当前年龄段<br >常见健康问题</p>
          </div>
          <img class="listImg" src="@/assets/images/home/wenti.png" />
          <!-- <svg class="icon" aria-hidden="true">
            <use xlink:href="#iconbuweizizhen"/>
          </svg> -->
        </div>
        <div class="item_div" @click="pushPage(6)">
          <div>
            <h2>全生命周期健康</h2>
            <p>了解您和家人当前<br >健康建议</p>
          </div>
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#iconshengmingzhouqi"/>
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
import { getToken_360App } from '@/utils/auth'
export default {
  name: 'ListTwo',
  methods: {
    pushPage(index) {
      var pageRoutes = {
        1: '/dailyHealth',
        2: '/selfBodyCheck',
        3: '/commonDisease',
        4: '/TCMphysique',
        5: '/diseaseDistribution',
        6: '/lifeCycle'
      }

      if(index === 2) {
        this.$root.actionToNative('gotoOuterSiteURL', '部位自诊', window.location.host+'/static/selfBodyCheck/index.html')
        // window.location.href = "static/selfBodyCheck"
      } else if(index === 3) {
          //呀！您还处于幼儿期，请预防...、...等常见疾病
          let callback = (period, dataItems) => {
              let array = dataItems.map(n => n.Name);
              let message = `呀！您还处于${period}，请预防${array.join('、')}等常见疾病`;

              this.$MessageBox({
                  title: '提示',
                  message,
                  confirmButtonText: "我知道了"
              });
          };
          this.$root.getCommonDisease(callback);
      } else if(index === 4) {
        const postData ={
          "name" : this.$store.state.user.name,
          "phone" : this.$store.state.user.phone,
          "sex" : this.$store.state.user.gender,
        };
        console.log(JSON.stringify(postData))
        
        const baseUrl = process.env.NODE_ENV === 'production' ? "http://healthrecord.kmhealthcloud.cn:8987" : "http://test-healthrecord.kmhealthcloud.cn:8987"
        axios.post(baseUrl + "/personInfo", postData,{
          headers: {
            'Token': getToken_360App()
          }
        }).then((response) => {
          return response.data;
        }).then((data) => {
            this.$root.actionToNative('gotoOuterSiteURL', '中医体质', data.data || '')
        }).catch(() => {
            console.log("请求出错");
        });
      }else{
        this.$router.push({ path: pageRoutes[index] })
      }
    }
  }
}
</script>

<style scoped lang="stylus">
  @import '~@/assets/styles/varibles.styl'
  .list
    display:flex
    height:px2rem(450)
    box-sizing:border-box
    background-color:#fff
    margin:px2rem(18) auto
    .item
      flex:1
      border:1px solid #eee
      border-left:none
      border-top:none
      &>svg
        width:px2rem(118px)
        padding-top:px2rem(50)
        height:px2rem(145px)
      &> .item_div
        display:flex
        width:100%
        box-sizing:border-box
        height:px2rem(450/2)
        padding-left:px2rem(20)
        padding-right:px2rem(20)
        align-items:center
        &>svg
          width:px2rem(65)
          height:auto
          text-align:right
          margin-top :px2rem(-30)
        &>div
          flex:1
          text-align:left
          justify-content :center
          &>h2
            margin-top :0px
            margin-bottom :px2rem(10)
        &>img.listImg{
				  width: 1.0rem;
				  height: 1.0rem;
          margin-top :px2rem(-30);
				  // padding-right: 0.2rem;
        }
    .item h2
      font-size:px2rem(28px)
      font-weight :bold
      color:#113260
      line-height:px2rem(30)
      margin-bottom:px2rem(16)
      margin-top:px2rem(32px)
    .item p
      font-size:px2rem(24px)
      color:#7b95b8
      line-height:px2rem(34px)
    .borderBottom1
      border-bottom:1px solid #eee
</style>
