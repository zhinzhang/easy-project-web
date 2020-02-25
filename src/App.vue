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
    returnAppStorage(key, value) {
      console.log(value);

      let student = JSON.parse(value);
      alert(student.name);
      this.name = student.name;
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
    postMessageFunction(data) {
      window.webkit.messageHandlers.callAppMethod.postMessage(
        JSON.stringify(data)
      );
    },
    alertType(params) {
      console.log(params);
    }
  },
  mounted() {
    window.alertType = this.alertType;
    window.returnAppStorage = this.returnAppStorage;
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
