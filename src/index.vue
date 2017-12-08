<template>
  <div class="container" :style="{ height: height }">
    <div class="demo">
      <wxc-minibar title="快速医疗"
                   background-color="#009ff0"
                   text-color="#FFFFFF"
                   right-text="更多"
                   left-button="false"
                   @wxcMinibarLeftButtonClicked="minibarLeftButtonClick"
                   @wxcMinibarRightButtonClicked="minibarRightButtonClick"></wxc-minibar>
    </div>

    <wxc-tab-bar :tab-titles="tabTitles"
                 :tab-styles="tabStyles"
                 title-type="icon"
                 :tab-page-height="tabPageHeight"
                 @wxcTabBarCurrentTabSelected="wxcTabBarCurrentTabSelected">
      <!-- 第一个页面内容-->
      <div class="item-container" :style="contentStyle">
        <wxc-button text="拍照上传"
                    type="yellow"
                    @wxcButtonClicked="camera"></wxc-button>
        <wxc-button text="打开相册"
                    type="yellow"
                    @wxcButtonClicked="gallery"></wxc-button>
        <text>{{result}}</text>
      </div>

      <!-- 第二个页面内容-->
      <div class="item-container" :style="contentStyle"><text>特别推荐</text></div>

      <!-- 第三个页面内容-->
      <div class="item-container" :style="contentStyle"><text>消息中心</text></div>

      <!-- 第四个页面内容-->
      <div class="item-container" :style="contentStyle"><text>我的主页</text></div>
    </wxc-tab-bar>
  </div>
</template>
<style scoped>
  .item-container {
    width: 750px;
    background-color: #f2f3f4;
    align-items: center;
    justify-content: center;
  }
</style>
<script>
//    import Nat from 'natjs';
    import { WxcMinibar,WxcTabBar, Utils,WxcButton  } from 'weex-ui';
    import Config from './config'
    const modal = weex.requireModule('modal');
    var ImageCropPicker = weex.requireModule('imageCropPicker');
  var options = {
      width: 300,
      height: 300,
      includeExif: true,
      mediaType: 'photo',
      cropping: true
  };
    export default {
        components: { WxcMinibar , WxcTabBar ,WxcButton   },
        data: () => ({
            height:'100vh',
            tabTitles: Config.tabTitles,
            tabStyles: Config.tabStyles,
            imgPath:'',
            result:''
        }),
        created () {
            this.tabPageHeight = Utils.env.getPageHeight();
            const { tabPageHeight, tabStyles } = this;
            this.contentStyle = { height: (tabPageHeight - tabStyles.height) + 'px'};
        },
        methods: {
            minibarLeftButtonClick () {
            },
            minibarRightButtonClick () {
                modal.toast({ 'message': 'click rightButton!', 'duration': 1 });
            },
            wxcTabBarCurrentTabSelected (e) {
                const index = e.page;
//                console.log(index);
            },
            gallery(e) {
                ImageCropPicker.openPicker(options, (response) => {
                    // 成功返回 {code:'E_SUCCESS', data:{...}}
                    this.result = JSON.stringify(response)
                })
            },
            camera(e) {
                ImageCropPicker.openCamera(options, (response) => {
                    // 失败返回 {cdoe:'E_PERMISSION_MISSING', message:'...'}
                    this.result = JSON.stringify(response)
                })
            }
        }
    };
</script>