<template>
  <div class="part-top">
    <div class="imgbox">
      <div class="timebox">
        <div class="clockbox">{{clocktime}}</div>
        <div class="datebox">{{nyydate}}</div>
      </div>
      <img src="https://lg-m1opkjhk-1256679880.cos.ap-shanghai.myqcloud.com/top_bg_01.png" alt>
    </div>
    <div class="bottomline">
      <div class="bottomline1">
        <div class="d1"></div>
        <div class="img1"></div>
        <div class="d2"></div>
      </div>
      <div class="bottomline1">
        <div class="d1"></div>
        <div class="img2"></div>
        <div class="d2"></div>
      </div>
      <div class="bottomline3">
        <div class="d1"></div>
        <div class="img3"></div>
        <div class="d3"></div>
      </div>
    </div>
  </div>
</template>

<script>
import wheather from '../components/wheather.vue'
export default {
    components: { wheather },
    props: {},
    data() {
        return {
          dsq:null,
          clocktime:"",
          nyydate:""
        }
    },
    created() {},
    mounted() {
      var that=this
        that.gettime()
        that.dsq=setInterval(function(){that.gettime()},1000)
    },
    computed: {},
    methods: {
        gettime() {
            var date = new Date()
            var year = date.getFullYear()
            var month = date.getMonth()+1
            var day = date.getDate()
            var hour = date.getHours()
            var minutes = date.getMinutes()
            var second = date.getSeconds()
            if (month < 10) {
                month = '0' + month
            }
            if (day < 10) {
                day = '0' + day
            }
            if (hour < 10) {
                hour= '0' + hour
            }
            if (minutes < 10) {
                minutes = '0' +minutes
            }
              if (second < 10) {
                second = '0' +second
            }
            this.clocktime=hour+":"+minutes+":"+second
            this.nyydate=year+"."+month+"."+day
           /*    console.log(year)
        console.log(month)
        console.log(day)
        console.log(hour)
        console.log(minutes)
        console.log(second) */
        }
    },
    watch: {},
    destroyed(){
      window.clearInterval(that.dsq)
      that.dsq=null
    }
}
</script>
<style lang="less" >
.part-top {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    height: 80px;
    background-color: #06161f;
    .imgbox {
        position: relative;
        .timebox {
            display: flex;
            flex-direction: column;
            flex-wrap: nowrap;
            align-content: center;
            width: 140px;
            height: 40px;
            /*  background-color: #60b8c6; */
            position: absolute;
            top: 18px;
            right: 482px;
            .clockbox {
                width: 100px;
                height: 26px;
                /* background-color: #60c671; */
                font: bold 20px/28px '微软雅黑';
                color: #fff;
                letter-spacing: 2px;
                text-align: end;
                margin-left: 24px;
            }
            .datebox {
                width: 100px;
                height: 16px;
                font: normal 12px/20px '微软雅黑';
                color: #cdcdcd;
                text-align: end;
                /* text-indent: 5px; */
                /* background-color: #c66090; */
                margin-left: 21px;
            }
        }
    }
}
.bottomline {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: nowrap;
    height: 3px;
    width: 100%;
}
.bottomline1 {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: nowrap;
}
.bottomline2 {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: nowrap;
}
.bottomline3 {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: nowrap;
}
.d1 {
    width: 2px;
    height: 2px;
    background-color: #60b8c6;
    margin-left: 21px;
}
.d2 {
    width: 2px;
    height: 2px;
    background-color: #60b8c6;
}
.img1 {
    width: 532px;
    height: 1px;
    background-color: #214751;

    margin-bottom: 5px;
}
.img2 {
    width: 760px;
    height: 1px;
    background-color: #214751;
    /*   margin-left: -355px; */
}
.img3 {
    width: 532px;
    height: 1px;
    background-color: #214751;
}
.d3 {
    width: 2px;
    height: 2px;
    background-color: #60b8c6;
    margin-right: 15px;
}
</style>
