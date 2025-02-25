# bsf-sunmi-idcard

此项目是基于**商米K2**的身份证和非接卡服务SDK专为`uniapp`/`uniappx`的App项目定制的`UTS`插件。

## 平台

- Android

## 兼容性
- uniapp
- uniappx

## 使用说明

### 引入插件

```js
import * as IdcardManager from "@uni_modules/bsf-sunmi-idcard";

```

## API接口

### bindIDCardService (绑定身份证服务)
```js
IdcardManager.bindIDCardService({
    onConnected() {
        console.log("服务已连接");
    },
    onDisConnected() {
        console.log("服务已断开");
    }
});
```

### unbindIDCardService (卸载身份证服务)
```js
IdcardManager.unbindIDCardService();
```

### sendCommand (发送自定义指令)
```js
IdcardManager.sendCommand({
    command: "01020304", // 指令内容
    success: (res) => {
        console.log("执行成功", res);
    },
    fail: (res) => {
        console.log("执行失败", res);
    }
});
```

### closeCard (关闭卡片)
```js
IdcardManager.closeCard({
    success: (res) => {
        console.log("关闭成功");
    },
    fail: (res) => {
        console.log("关闭失败", res);
    }
});
```

### openMemoryCard (激活M1卡)
```js
IdcardManager.openMemoryCard({
    success: (res) => {
        console.log("激活成功", res);
    },
    fail: (res) => {
        console.log("激活失败", res);
    }
});
```

### openCpuCard (激活CPU卡)
```js
IdcardManager.openCpuCard({
    success: (res) => {
        console.log("激活成功", res);
    },
    fail: (res) => {
        console.log("激活失败", res);
    }
});
```

### memoryCardAuthEntication (M1卡认证)
```js
IdcardManager.memoryCardAuthEntication({
    mode: 0, // 0-KEYA模式;1-KEYB模式
    addr: 4, // 扇区地址
    key: "FFFFFFFFFFFF", // 密钥
    success: (res) => {
        console.log("验证成功", res);
    },
    fail: (res) => {
        console.log("验证失败", res);
    }
});
```

### memoryCardReadData (读取M1卡数据)
```js
IdcardManager.memoryCardReadData({
    addr: 0, // 读取地址
    success: (res) => {
        console.log("读取成功", res);
    },
    fail: (res) => {
        console.log("读取失败", res);
    }
});
```

### memoryCardReadDataVal (读取M1卡数值块)
```js
IdcardManager.memoryCardReadDataVal({
    addr: 0, // 读取地址
    success: (res) => {
        console.log("读取成功", res);
    },
    fail: (res) => {
        console.log("读取失败", res);
    }
});
```

### getJRICCardInfo (获取金融社保卡信息)
```js
IdcardManager.getJRICCardInfo({
    success: (cardno, name) => {
        console.log("卡号:", cardno, "姓名:", name);
    },
    fail: (res) => {
        console.log("获取失败", res);
    }
});
```

### getSiCardBaseInfo (获取社保卡基本信息)
```js
IdcardManager.getSiCardBaseInfo({
    success: (res) => {
        console.log("获取成功", res);
    },
    fail: (res) => {
        console.log("获取失败", res);
    }
});
```

### getEMID (获取EMID)
```js
IdcardManager.getEMID({
    success: (res) => {
        console.log("获取EMID成功", res);
    },
    fail: (res) => {
        console.log("获取EMID失败", res);
    }
});
```

### beep (蜂鸣器)
```js
IdcardManager.beep(5); // 参数为蜂鸣次数
```


