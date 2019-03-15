<template>
  <div class="app">
      <img class="img" :src="logo" @touchstart="changeStat">
      <hello-world :color="color"></hello-world>
      <h1 class="txt" v-show="t%2==1">click logo::{{t}}</h1>
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
export default {
  components: {
      HelloWorld
  },
  data() {
    return {
      logo: 'https://user-images.githubusercontent.com/20720117/48262986-80e02780-e45f-11e8-8426-2872916adad9.png',
      t: 1,
      color: '#007d37'
    }
  },
  beforeCreate() {
    console.log('Page [hello] Vue beforeCreate')
    console.log('current env is', Megalo.getEnv());
    console.log('current env is wechat', Megalo.getEnv() === Megalo.ENV_TYPE.WECHAT)

    
    Megalo.request.interceptors.before.use(options => {
      options.header.b = '1';
      console.log('======before=======', options);

      return options; 
    }, err => {
      return Promise.reject(err);
    });

    Megalo.request.interceptors.after.use(resp => {
      console.log('======after======', resp)
      return resp;
    }, err => {
      return Promise.reject(err);
    });

    let source = Megalo.CancelToken.source();
    const p = Megalo.request({
      cancelToken: source.token,
      url: 'https://gw.kaola.com/gw/miniapp/kaola/popup?version=1.0',
      method: 'POST',
      header: {
        token: '12121'
      }
    }).then(res => {
      console.log('success', res)
    }, e => {
      console.log('error', e)
    });

    // source.cancel('取消本次请求');

    // Megalo.stopPullDownRefresh().then(res => {
    //   console.log(1)
    // });

    // Megalo.setStorageSync('name', '贾克斯');

    // const name = Megalo.getStorageSync('name');
    // console.log('current name', name);

    Megalo.setNavigationBarColor({
      backgroundColor: '#ff0000',
      frontColor: '#000000',
    });

    // Megalo.chooseImage().then(res => {
    //   return Promise.resolve(res.tempFilePaths[0]);
    // }).then(path => {
    //   return Megalo.getSavedFileInfo({
    //     filePath: path
    //   })
    // }).then(res => {
    //   console.log('=========', res)
    // });

    // Megalo.chooseImage().then(res => {
    //   return Promise.resolve(res.tempFilePaths[0]);
    // }).then(path => {
    //   return Megalo.saveFile({
    //     tempFilePath: path
    //   })
    // }).then(res => {
    //   console.log('=========', res)
    // });

    // Megalo.getNetworkType().then(resp => {
    //   console.log('=====resp', resp.networkType);
    // });

    // Megalo.setClipboardData({
    //   data: 'HelloWorld'
    // }).then(resp => {
    //   console.log('========setClipboardData', resp);

    //   return Megalo.getClipboardData();
    // }).then(resp => {
    //   console.log('========getClipboardData', resp.data);
    // });

    // Megalo.makePhoneCall({
    //   phoneNumber: '15858178945'
    // }).then(resp => {
    //   console.log('========', resp);
    // });

    // Megalo.scanCode({

    // }).then(resp => {
    //   console.log('========', resp);
    // });

    // Megalo.authorize({
    //   scope: 'scope.userLocation'
    // }).then(resp => {
    //   return Megalo.getLocation({
    //     type: 'gcj02'
    //   })
    // }).then(resp => {
    //   console.log('======getLocation', resp);

    //   let { latitude, longitude } = resp;
    //   return Megalo.openLocation({
    //     latitude,
    //     longitude
    //   })
    // }).then(resp => {
    //   console.log('=======openLocation', resp);
    // });

    // Megalo.setScreenBrightness({
    //   value: 0.5
    // }).then(resp => {
    //   console.log('=========', resp)
    // });

    // function setScreen() {
    //   return new Promise((resolve, reject) => {
    //     my.setScreenBrightness({
    //       brightness: 0.5,
    //       success(resp) {
    //         resolve(resp);
    //       },
    //       fail(resp) {
    //         reject(resp);
    //       }
    //     })
    //   });
    // }

    // setScreen().then(resp => {
    //   console.log('=========', resp);
    // })

    // Megalo.setStorageSync('name', '贾克斯');
    // console.log(Megalo.getStorageSync('name'));

    // Megalo.getFileInfo({
    //   filePath: 'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg'
    // }).then(resp => {
    //   console.log('=========', resp);
    // });

    // my.saveFile({
    //   apFilePath: 'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg',
    //   success(resp) {
    //     console.log('==========', resp);
    //   }
    // });

    // function save() {
    //   return new Promise((resolve, reject) => {
    //     my.saveFile({
    //       tempFilePath: 'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg',
    //       success(rep) {
    //         // console.log('========', res)
    //         resolve(rep)
    //       }
    //     })
    //   })
    // }

    // save().then(rep => {
    //   console.log('=========', rep)
    // })

    // Megalo.showModal({
    //   title: 'hello',
    //   content: '你好',
    //   cancelText: '放弃',
    //   confirmText: '领取',
    //   showCancel: false,
    // }).then(res => {
    //   console.log(res);
    // });

    // Megalo.saveImageToPhotosAlbum();

    // Megalo.showActionSheet({
    //   title: '支付宝-ActionSheet',
    //   itemList: ['A', 'B', 'C'],
    //   itemColor: '#ff0000',
    //   cancelButtonText: '取消好了',
    // });

    // Megalo.previewImage({
    //   urls: ['https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg'],
    //   current: 'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg'
    // }).then(res => {
    //   console.log('=========', res)
    // });

    // Megalo.setStorage({
    //   key: 'name',
    //   data: '贾克斯'
    // });

    // const env = Megalo.getEnvInfoSync();

    // const run = Megalo.navigateBackMiniProgram({});

    // console.log('appName', env.appName);

    // const task = Megalo.downloadFile({
    //   url: 'https://haitao.nos.netease.com/eaf5c410-0667-420f-8d2c-19e81a3235c6_80_80.jpeg'
    // }).then(res => {
    //   console.log(res)
    // });

    // task.onProgressUpdate(res => {
    //   console.log('下载进度', res.progress);
    //   console.log('已经下载的数据长度', res.totalBytesWritten);
    //   console.log('预期需要下载的数据总长度', res.totalBytesExpectedToWrite);
    // })
  },
  created() {
    console.log('Page [hello] Vue created')
    var appInstance = getApp()
    console.log(appInstance.globalData) // I am global data
  },
  beforeMount() {
    console.log('Page [hello] Vue beforeMount')
  },
  mounted() {
    console.log('Page [hello] Vue mounted')
  },
  onLoad: function(options) {
    // Do some initialize when page load.
    console.log('Page [hello] onLoad')
  },
  onReady: function() {
    // Do something when page ready.
    console.log('Page [hello] onReady')
  },
  onShow: function() {
    // Do something when page show.
    console.log('Page [hello] onShow')
  },
  onHide: function() {
    // Do something when page hide.
    console.log('Page [hello] onHide')
  },
  onUnload: function() {
    // Do something when page close.
    console.log('Page [hello] onUnload')
  },
  /**
   * for other event handlers, please check https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/page.html
   */
  methods:{
    changeStat: function(){
      this.t++
      this.color = '#'+Math.floor(Math.random()*0xffffff).toString(16)
    }
  }
}
</script>

<style lang="less" scoped>
.app{
  padding-top: 100px;
  .img {
    display: block;
    height: 120px;
    width: 138px;
    margin: 20px auto;
  }
  .txt {
      color: #567567;
      font-size: 13px;
      text-align: center;
  }
}
</style>
