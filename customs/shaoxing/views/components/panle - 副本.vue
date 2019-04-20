<template>
    <div class="panle">
        <div class="panle-body">
            <div class="panle-title">
                <span>{{title}}</span>
            </div>
            <div class="panle-content">
                <slot></slot>
            </div>
            
        </div>
    </div>
</template>
<script>
export default {
    props: {
        title: String
    },
    data() {
        return {}
    }
}
</script>
<style lang="less" scoped>
@blue: #01cef6;
.panle {
    position: relative;
    background-color: #06161f;
    /*   background-color: #1b90d4!important; */
   background-image: url('../../../../static/images/right_bg.png');
   background-repeat: no-repeat;
  background-position: 240px 58px;
    // margin: 10px 0;
    padding: 10px;
    z-index: 3;
    .panle-body {
        .panle-title {
            padding-left: 20px;
            /*   background: linear-gradient(to right, #063943 , rgba(0,0,0,0.1)); */
            line-height: 22px;
            margin-bottom: 10px;
            span {
                font-size: 12px;
                color: #fff;
                font-weight: bold;
                text-shadow: -2px 2px 30px #eff;
                    margin-left: -10px;
            }
        }
        .panle-content {
            // width: 90%;
            // height: 65%;
            // margin-left: 4.5%;
            // margin-top: 1.8%;
            // position: relative;
            // padding: 5px;
        }
    }
}
</style>
