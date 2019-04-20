    <template>
  <div class="part-center">
    <!-- <my-map></my-map> -->
    <!-- 扫描 -->
    <div
      style="  width:100%; height:100%;position: absolute; margin:0 auto;
               z-index:2; overflow:hidden;"
    >
      <div id="myDiv" style="width: 60%;height:0px;z-index:3;position: absolute;top:200px"></div>
    <!--   <div
        class="beijing01"
        style=" width: 60%; height:278px; margin:0 auto; background:url(../static/images/saomiao/扫描01.png);background-repeat:repeat-x;
               z-index:3;"
      ></div> -->
    </div>
 <!--     <div
      style="  width:100%; height:100%;position: absolute; margin:0 auto; background:url(../static/images/saomiao/wangge03.png);background-repeat:repeat;
               z-index:2; overflow:hidden;"
    >
      <div id="myDiv" style="background-color: lightblue;width: 60%;height:0px;z-index:3;position: absolute;top:200px"></div>
    <div
        class="beijing01"
        style="  width:1036px; height:278px; margin:0 auto; background:url(../static/images/saomiao/扫描01.png);background-repeat:repeat-x;
               z-index:3;"
      ></div>
    </div> -->
    <!-- 扫描 -->

    <div style="height:100%;position:relative;">
      <div
        class="map-switch"
        v-if="theme == 'check'||theme == 'applypump'"
        :style="{top:theme=='applypump'?'-4px':'171px'}"
      >
        <div class="box">
          <div
            class="listbox"
            v-for="(item,index) in tabsParam"
            :key="item.tabsParam"
            @click="toggleTabs(index)"
            :class="{active:index===nowIndex}"
          >{{item}}</div>
        </div>
        <!--  <span class="map-click" id="map_1" :class="{'active':selectId==1}">
                  <a @click="switchMap(1)">管网压力变化</a>
                </span>
                <span class="map-click" id="map_2" :class="{'active':selectId==2}">
                  <a @click="switchMap(2)">管网流量分布</a>
        </span>-->
        <!--   <span class="map-click" id="map_3" :class="{'active':selectId==3}">
                  <a @click="switchMap(3)">管网事件分布</a>
        </span>-->
      </div>

      <!-- <iframe src="http://121.40.242.176:8091/#/pressuremap" width="100%" height="100%;" style="border-width: 0px!important;" id="m_map"></iframe> -->
    </div>
    <div class="map-warp">
      <img
        src="https://lg-m1opkjhk-1256679880.cos.ap-shanghai.myqcloud.com/1g.gif"
        v-show="nowIndex===0"
        alt
        name="m_map1"
        :style="{zIndex:selectId==2?10:1}"
        width="100%"
        height="100%;"
        style="border-width: 0px!important;position:absolute;z-index:10;"
        id="m_map1"
      >
      <img
        src="https://lg-m1opkjhk-1256679880.cos.ap-shanghai.myqcloud.com/background.jpg"
        v-show="nowIndex===1"
        alt
        name="m_map2"
        :style="{zIndex:selectId==1?10:1}"
        width="100%"
        height="100%;"
        style="border-width: 0px!important;position:absolute;z-index:20;"
        id="m_map2"
      >
      <!--   <iframe  name="m_map1" :style="{zIndex:selectId==2?10:1}" src="../../../../static/images/1.jpg" width="100%" height="100%;" style="border-width: 0px!important;position:absolute;z-index:10;" id="m_map1"></iframe>
      <iframe name="m_map2"  :style="{zIndex:selectId==1?10:1}" src="../../../../static/images/background.jpg" width="100%" height="100%;" style="border-width: 0px!important;position:absolute;z-index:20;" id="m_map2"></iframe>-->
      <!--  <iframe name="m_map2"  :style="{zIndex:selectId==1?10:1}" src="../../../../static/images/background.jpg" width="100%" height="100%;" style="border-width: 0px!important;position:absolute;z-index:20;" id="m_map2"></iframe> -->
      <!-- <iframe name="m_map1" :style="{zIndex:selectId==2?10:1}" src="http://121.40.242.176:8091/#/flowmap" width="100%" height="100%;" style="border-width: 0px!important;position:absolute;z-index:10;" id="m_map1"></iframe>

      <iframe name="m_map3" :style="{zIndex:selectId==3?10:1}" src="http://121.40.242.176:8091/#/eventmap" width="100%" height="100%;" style="border-width: 0px!important;position:absolute;z-index:30;" id="m_map3"></iframe>-->
    </div>
  </div>
</template>

    <script>
import partRight from './right.vue'
import partTop from './top.vue'
import { setInterval } from 'timers'
// import MyMap from '../components/myMap.vue'

export default {
    props: {
        theme: String
    },
    data() {
        return {
            selectId: 1,
            tabsParam: ['管网压力变化', '水龄分析'],
            nowIndex: 0,
            timer: '',
            timer2:''
        }
    },
    created() {},
    computed: {},
    beforeDestroy() {
        window.clearInterval(this.timer)
        this.timer = null
    },
    mounted(){
         let that = this
           that.nowIndex = 1
         that.saomao()
        that.timer = setInterval(function() {
            if (that.nowIndex == 0) {
                that.nowIndex = 1
              /*   that.timer2=null
                that.saomao() */
            } else if (that.nowIndex == 1) {
                that.nowIndex = 0
           /*  that.timer2=null
                that.saomao() */
            }
        }, 36000)

    },
    /*  mounted() {
        let that = this
        that.nowIndex = 1
        that.timer = setInterval(function() {
            if (that.nowIndex == 0) {
                that.nowIndex = 1
            } else if (that.nowIndex == 1) {
                that.nowIndex = 0
            }
        }, 1000)
    }, */
    methods: {
        //切换tab项
        toggleTabs(index) {
            this.nowIndex = index
        },
        saomao() {
            let that = this
             myDiv.style.height = "0";
            cancelAnimationFrame(that.timer2)
            that.timer2 = requestAnimationFrame(function fn() {
                if (parseInt(myDiv.style.height) < 720) {
                    myDiv.style.height = parseInt(myDiv.style.height) + 1 + 'px'
                    var FPS = 100
                    setTimeout(function() {
                        requestAnimationFrame(fn)
                    }, 3000 / FPS)
                } else {
                    cancelAnimationFrame(that.timer2)
                    myDiv.style.height = '0'
                    setTimeout(function() {
                        requestAnimationFrame(fn)
                    }, 1800 / FPS)
                }
            })
        }
    },
    /*   methods: {
        switchMap(key) {
            this.selectId = key
        }
    }, */
    watch: {},
    components: {
        partRight,
        partTop
        //   MyMap
    }
}
</script>
    <style lang="less" >
#map_1 {
    display: inline-block;
    width: 100px;
    height: 30px;
    text-align: center;
    line-height: 30px;
    /*  border-radius: 2px;
              border: 1px solid #1d81b3;
              margin-bottom: 10px; */
}
.part-center {
    float: left;
    width: 54%;
    height: 100%;
    box-sizing: border-box;
    // position: relative;
    .map-switch {
        z-index: 2000;
        width: 100%;
        height: 40px;
        box-sizing: border-box;
        position: absolute;
        background-color: #06161f;
        /*  border: solid 2px rgba(89, 90, 90, 0.8); */
        font-family: MicrosoftYaHei-Bold;
        font-size: 12px;
        /*   font-weight: 600; */
        line-height: 29px;
        color: #747474;
        position: relative;
        .box {
            display: -webkit-box;
            display: -webkit-flex;
            display: -ms-flexbox;
            display: flex;
            flex-direction: row;
            flex-wrap: nowrap;
            justify-content: flex-start;
            align-items: center;
            /*  width: 400px; */
            height: 40px;
            /*   border: 1px #e4e4ec solid; */
            border-right: none;
            top: -5px;
        }
        .listbox {
            width: 120px;
            height: 40px;
            text-align: center;
            line-height: 40px;
            /*   border-right: 1px #e4e4ec solid; */
            font-size: 14px;
            font-family: '微软雅黑';
            font-weight: bold;
            cursor: pointer;
            color: #6d6d6e;
            border-bottom: 2px rgba(255, 255, 255, 0) solid;
            /* background-color: #f5f5f6; */
        }

        .active {
            color: #01cef6;
            border-bottom: 2px #01cef6 solid;
            /*   background-color: #01cef6; */
        }
        .list {
            display: -webkit-box;
            display: -webkit-flex;
            display: -ms-flexbox;
            display: flex;
            flex-direction: column;
            flex-wrap: nowrap;
            justify-content: space-between;
            width: 100%;
        }
        .map-click {
            margin-left: 9px;
            margin-right: 30px;
            a {
                cursor: pointer;
            }
            &.active {
                /*   display: inline-block; */
                color: #d2d6d9;
                /*  background-color: rgba(13,54,75,0.8); */
                display: inline-block;
                width: 100px;
                height: 30px;
                text-align: center;
                line-height: 30px;
                border-radius: 2px;
                border-bottom: 1px solid #1d81b3;
                margin-bottom: 10px;
            }
        }
    }
    .map-warp {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: transparent;
        top: 0;
        left: 0;
        z-index: 0;
        iframe {
            background-color: transparent;
        }
    }
}
#myDiv{
      background: -webkit-linear-gradient(	rgba(1,206,246,0), rgba(1,206,246,0.2)); /* Safari 5.1 - 6.0 */
    background: -o-linear-gradient(rgba(1,206,246,0), rgba(1,206,246,0.2)); /* Opera 11.1 - 12.0 */
    background: -moz-linear-gradient(rgba(1,206,246,0), rgba(1,206,246,0.2)); /* Firefox 3.6 - 15 */
    background: linear-gradient(rgba(1,206,246,0), rgba(1,206,246,0.2)); /* 标准的语法（必须放在最后） */
    border-bottom: 2px solid #00d5ff ;
    box-shadow: 0px 2px 1px  #01cef6 inset;
}
/* .beijing01 {
    position: absolute;
    animation: mymove 10s infinite;
    -webkit-animation: mymove 10s infinite;

}

@keyframes mymove {
    0% {
        top: -60px;
    }
    100% {
        top: 700px;
    }
}

@-webkit-keyframes mymove
 {
    0% {
        top: -60px;
    }
    100% {
        top: 700px;
    }
} */
</style>
