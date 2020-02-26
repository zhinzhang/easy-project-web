<template>
  <div id="app">
    <div id="nav">
      <div>
        <button @click="clickSetStorage">本地存储</button>
      </div>
      <div>
        <button @click="clickGetStorage">获取本地存储值</button>
        <span>{{name}}</span>
      </div>
      <div>
        <button @click="clickShowAlert">Alert显示</button>
      </div>
      <div>
        <button @click="clickShowHudMessage">HUD显示消息</button>
      </div>
      <div>
        <button @click="clickShowHudload">HUD加载中</button>
      </div>
      <div>
        <button @click="clickHideHud">HUD隐藏</button>
      </div>
      <div>
        <button @click="clickDownload">下载文件</button>
      </div>
      <div>
        <button @click="clickScan">扫描二维码</button>
      </div>
      <div>
        <button @click="clickCopy">复制内容</button>
      </div>
      <div>
        <button @click="clickGetCopy">获取复制内容</button>
      </div>
      <div>
        <button @click="clickCall">打电话</button>
      </div>
      <div>
        <button @click="clcikGetAppInfo">获取APP详细信息</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: ""
    };
  },
  methods: {
    clickSetStorage() {
      let data = {
        method: "setAppStorage",
        param: {
          key: "student",
          value: {
            id: "js001",
            name: "ming"
          }
        }
      };
      this.postMessageFunction(data);
    },
    clickGetStorage() {
      let data = {
        method: "getAppstorage",
        param: {
          key: "student"
        }
      };
      this.postMessageFunction(data);
    },
    clickShowAlert() {
      let data = {
        method: "showAlertView",
        param: {
          title: "提示", //弹窗标题
          message: "", //消息内容
          actions: [
            //弹窗数组 一个为alert样式,两个及以上为actionsheet样式
            {
              title: "按钮1", //弹窗标题
              type: "0", //
              is_default: "Y" // Y为UIAlertActionStyleDefault/N为UIAlertActionStyleDestructive
            },
            {
              title: "按钮2",
              type: "1",
              is_default: "Y"
            },
            {
              title: "删除",
              type: "2",
              is_default: "N"
            },
            {
              title: "确认",
              type: "cancle",
              is_default: "Y"
            }
          ]
        }
      };
      this.postMessageFunction(data);
    },
    clickShowHudMessage() {
      let data = {
        method: "performLoading",
        param: {
          type: "message",
          message: "你好"
        }
      };
      this.postMessageFunction(data);
    },
    clickShowHudload() {
      let data = {
        method: "performLoading",
        param: {
          type: "load",
          message: "你好",
          canClick: "N"
        }
      };
      this.postMessageFunction(data);
    },
    clickHideHud() {
      let data = {
        method: "performLoading",
        param: {
          type: "hide"
        }
      };
      this.postMessageFunction(data);
    },
    clickDownload() {
      let data = {
        method: "downloadFile",
        param: {
          message: "视频下载中",
          file_url:
            "http://dsn-prod.oss-cn-shenzhen.aliyuncs.com/material_videos/5d5519cd5c82620c10a02c75/5d5519cd5c82620c10a02c75-1581148080732.mp4",
          file_type: "mp4"
        }
      };
      this.postMessageFunction(data);
    },
    clickScan() {
      let data = {
        method: "scanQrCode"
      };
      this.postMessageFunction(data);
    },
    clickCopy() {
      let data = {
        method: "setPasteboard",
        param: {
          value: "这是需要复制的内容"
        }
      };
      this.postMessageFunction(data);
    },
    clickGetCopy() {
      let data = {
        method: "getPasteboard"
      };
      this.postMessageFunction(data);
    },
    clickCall() {
      let data = {
        method: "makePhoneCall",
        param: {
          phone: "10086"
        }
      };
      this.postMessageFunction(data);
    },
    clcikGetAppInfo() {
      let data = {
        method: "getAppDetailInfo"
      };
      this.postMessageFunction(data);
    },
    appBlockData(data) {
      alert(data);
    },
    postMessageFunction(data) {
      window.webkit.messageHandlers.callAppMethod.postMessage(
        JSON.stringify(data)
      );
    }
  },
  mounted() {
    window.appBlockData = this.appBlockData;
  }
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
