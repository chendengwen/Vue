<template> 
  <div class="root-page-box">
    <health-record></health-record>
    <ul>
      <li id="BloodPressure"><router-link to="BloodPressure">血压</router-link></li>
      <li><router-link to="BloodSugar">血糖</router-link></li>
      <li><router-link to="Pulse">心率</router-link></li>
      <li><router-link to="Step">步数</router-link></li>
      <li><router-link to="Oxygen">血氧</router-link></li>
      <li><router-link to="VitalCapacity">肺活量</router-link></li>
      <li><router-link to="TotalCholesterol">胆固醇</router-link></li>
    </ul>
  </div>
</template>


<script>

import HealthRecord from "../../home/components/HealthRecord";

export default {
  name: 'HealthRecordNav', 
  data() {
    return {
      showBoxId: '0',
      selected: 'BloodPressure'
    }
  },
  components:{
    HealthRecord
  },
  methods: {
    // 切换
    changeBox(i) {
      this.showBoxId = i
      this.getReport(i)
    }
  }
}
</script>

<style scoped lang="stylus">
  @import '~@/assets/styles/varibles.styl'
ul
  display: flex
  height:px2rem(90)
  line-height:px2rem(90)
  &>li
    flex: 1
    font-size:px2rem(28)
    border-bottom:1px solid #e2e2e3
  .router-link-active
    border-bottom:px2rem(4) solid #008dfd  // 改变路由的状态
    color:#008dfd
    padding-bottom:px2rem(21)
</style>
