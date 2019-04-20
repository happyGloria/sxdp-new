<template>
  <div class="views-overview">

    <part-top></part-top>

    <div class="overview-center">
      <div class="line1"></div>
       <div class="line2"></div>
      <template v-show="theme=='check' ||theme=='applypump' ">
        <part-middle :theme="theme"></part-middle>

        <front-top :theme="theme"></front-top>
        <front-bottom :theme="theme"></front-bottom>
      </template>

      <template v-if="theme=='introduce' ||theme=='intelligence'|| theme=='science'  ">
        <theme-introduce :theme="theme" style="z-index:99999"></theme-introduce>
      </template>

    </div>
   <!--  <div style="padding-bottom:8px;">
        <part-bottom @change-theme="changeTheme"></part-bottom>
    </div>
    -->

  </div>

</template>

<script>
import partTop from './part/top.vue'
import partMiddle from './part/middle.vue'
import frontTop from './part/front/top'
import frontBottom from './part/front/bottom'
import partBottom from './part/bottom.vue'
import themeIntroduce from './components/introduce'
export default {
    props: {},
    data() {
        return {
            theme: 'check'
            // theme: 'applypump'
        }
    },
    created() {},
    mounted() {},
    computed: {},
    methods: {
        changeTheme: function(theme) {
            let self = this
            self.theme = theme
        }
    },
    watch: {},
    components: {
        partTop,
        partMiddle,
        partBottom,
        themeIntroduce,
        frontTop,
        frontBottom

    }
}
</script>
<style lang="less" >
.views-overview {
    background-color: #06161f;
    margin: 0;
    padding: 0;
    height: 100%;
    .overview-center{
        position: relative;
      width: 100%;
      height: 927px;
      .line1{
        height: 978px;
        width: 1px;
        background-color: #1c3e48;
        position: absolute;
        left:22.94%;
        top: -3px;
        z-index: 999999
      }
       .line2{
        height: 978px;
        width: 1px;
        background-color: #1c3e48;
        position: absolute;
        right: 22.99%;
        top: -3px;
        z-index: 999999
      }
    }
}
</style>
