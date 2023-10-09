# ZMind
</div>  
<p align="center">
</p>
<p align="center">
  <a href="./LICENSE">
      <img src="https://img.shields.io/github/license/zyascend/ZMindMap" alt="MIT License" />
  </a>
  <a href="https://v3.cn.vuejs.org/">
      <img src="https://img.shields.io/badge/vue.js-3.2-green" alt="Vue3.2">
  </a>
  
</p>

## 简介
**仿[幕布](https://mubu.com)思维导图网站。支持导图编辑、大纲编辑、图片导出**  



Node端地址：[zmind-backend](https://github.com/zanderzhao/zmind-backend) 

## 下载&安装

docker-compose 版本

```yml

version: '3'

services:
  zmind-frontend:
    container_name: zmind-frontend
    image: zanderzhao/zmind-frontend
    # image: zmind-frontend
    restart: always
    ports:
      - 3004:8080
    # network_mode: host
    # volumes:
    #   - ${PWD}/data:/app
    links:
      - zmind-backend
    environment:
      - NODE_ENV=production
      - WATER_PRINT_COPYRIGHT=ZMIND
      - ZMIND_FRONTEND_URL=http://127.0.0.1:3004
      - ZMIND_BACKEND_URL=http://127.0.0.1:3003
      - BAIDU_HM=https://hm.baidu.com/hm.js?zzz

  zmind-backend:
    container_name: zmind-backend
    image: zanderzhao/zmind-backend
    # image: zmind-backend
    ports:
      - 3003:3003  # 如果你的App需要公开端口，可以映射到宿主机
    links:
      - zmind-backend-redis
      - zmind-backend-mongodb
    environment:
      - NODE_ENV=production

  zmind-backend-redis:
    container_name: zmind-backend-redis
    image: redis:latest
    # 6379

  zmind-backend-mongodb:
    container_name: zmind-backend-mongodb
    image: mongo:latest
    # 27017

```


## 效果图

| <img src="https://github.com/zyascend/ZMindMap/blob/main/assets/export07.png?raw=true" style="zoom:20%;" /> | <img src="https://github.com/zyascend/ZMindMap/blob/main/assets/export02.png?raw=true" style="zoom:20%;" /> |
| :------------------------------------------------------------------------------: | -------------------------------------------------------------------------------- |
| <img src="https://github.com/zyascend/ZMindMap/blob/main/assets/export03.png?raw=true" style="zoom:20%;" /> | <img src="https://github.com/zyascend/ZMindMap/blob/main/assets/export04.png?raw=true" style="zoom:20%;" /> |
| <img src="https://github.com/zyascend/ZMindMap/blob/main/assets/export05.png?raw=true" style="zoom:20%;" /> | <img src="https://github.com/zyascend/ZMindMap/blob/main/assets/export06.png?raw=true" style="zoom:20%;" /> |

视频版：[点击播放](https://cdn.kimjisoo.cn/videos%2Fpresentation_v1.0.mp4)

## Features
- Vue3 CompositionApi
- Pinia状态管理
- VueRouter路由控制
- SVG画图
  - 类幕布思维导图的文档构建方式实现
    - 数据驱动UI的思路
  - svg导出为png图片 
- Element-plus
  - splitChunks单独打包
- 基于七牛云的CDN加速
- JWT & 二维码扫码登录
- 夜间模式
- 前端监控
  - 使用Sentry收集错误信息
  - 百度统计

## TODOs
- [x] 基于vue响应式，通过数据驱动svg子元素更新
- [x] 对于大纲编辑，如何不通过递归查找的方式在源数据中定位到待更新的节点
  - [x] key-value形式构建map
- [x] Vuex切换为pinia
  - [x] store分模块维护
- [x] 支持撤回操作
  - [x] bug fix
- [x] 导图风格切换
- [x] 支持导出
  - [x] 导出为图片
    - [x] 图片不显示 bug fix
  - [ ] 导出为其他格式
- [x] 二维码扫码登录
  - [x] 轮询接口查状态 => websocket
- [x] 大纲编辑页相关优化
  - [x] 防止XSS攻击
- [x] 支持添加图片
- [x] 重写节点宽高计算逻辑
- [x] 全面重写MindMap组件
  - [x] 代码臃肿：分离UI渲染部分和数据部分
  - [x] 可拓展性：提取各种样式导图的公共dom结构 方便切换导图风格
  - [x] 公共逻辑抽取 方便随时切换颜色样式
  - [x] 导图计算：抽取公共逻辑  + 继承封装
  - [x] map store 逻辑优化
- [ ] 页面的loading 和 错误处理
- [ ] 监听全局异常 error boundary
- [ ] 使用自定义的loader处理svg图标
  - [ ] 将svg icon处理为SFC
  - [ ] 封装SFC为Icon组件：绑定属性 灵活使用
- [x] 所有配置项由`window.CFG`注入



## 说明


+ 这是前端

+ 基于[zyascend/ZMindMap](https://github.com/zyascend/ZMindMap)参考[seasnakes/ZhiGeng](https://github.com/seasnakes/ZhiGeng)

+ 截止202310，好像还不支持主题拖动排序

+ 还有一些url作者写死的改成localhost了，本地可以跑通，云端可能要改点东西



