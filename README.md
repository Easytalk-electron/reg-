# electron EasyTalk

## 技术栈

vue +  vue-router + mockjs + webpack + ES6/7 + scss + electron + electron-build + axios

### 项目说明

基于 electron-vue + element ui 仿微信客户端(美工可能会再改)参考了几个网页版im的格式
暂时使用mock.js实现本地数据
待完善前端功能：
* 登录
* 拉群
* 视频
* 音频
待完善后端功能：
* 用户数据库
* 替换前后端接口



### 项目目录

```
src
├── index.ejs
├── main
│   ├── module(待测试)
│   │   ├── login.js
│   │   ├── mainWindow.js
│   │   ├── webView.js
│   ├── index.dev.js
│   └── index.js
└── rendererd
│   ├── App.vue
│   ├── assets
│   │   └── logo.png
│   ├── components
│   │   ├── chatInput
│   │   ├── chatList
│   │   ├── message
│   │   ├── search
│   │   ├── sidebar
│   ├── config
│   │   └── http.js
│   ├── main.js
│   ├── router
│   │   └── index.js
│   ├── service
│   │   ├── api.js
│   │   └── http.js
│   │   └── index.js
│   └── store
│        ├── emoji.js
│        ├── index.js
static
├── emogi
├── images
```

### 构建应用

``` bash
# 安装依赖（建议优先用yarn）
yarn / npm install

# 补充依赖环境(能够解决一些报错问题)
yarn add --global windows-build-tools /npm install --global windows-build-tools
# 热加载服务运行在 localhost: 9080
yarn run dev / npm run dev

# 打包项目
yarn run build/ npm run build
```

