<template>
  <div class="phone-verification">
    <div class="right-img"><img src="../assets/img/right.gif" height="63" width="63"/></div>
    <h5>绑定成功!</h5>
    <p class="prompt">即将跳转 <span v-html="time"></span></p>
    <input type="submit" value="完成" class="phone-number-btn" v-on:click="completeBing"/>
  </div>
</template>

<script>
  import globalMixin from "../mixins/global";
    export default {
      name: "BingSucces",
      mixins: [globalMixin],
      data() {
        return {
          number: null,
          time: "4秒",
        }
      },
      computed: {
      },
      watch: {
      },
      beforeCreate() {
      },
      created() {
      },
      mounted() {
        this.setTime(4);
      },
      methods: {
        completeBing() {
          this.$router.replace({name: 'report'});
        }
      }
    }
</script>

<style scoped>

</style>
