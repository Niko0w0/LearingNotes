### 一、Vue CLI

#### 1.1 runtime-compiler和runtime-only的区别

- ESLint到底是什么？
- template -> ast -> render -> vdom -> 真实DOM
- render:(h) => h -> createElement

#### 1.2 Vue-Router

- 如何通过CLI3创建项目
- CLI3的目录结构
- 配置文件：
  1. Vue UI
  2. 隐藏的配置文件
  3. 自定义vue.config.js



### 二、Vue-Router

#### 2.1.什么是前端路由

- 后端渲染\后端路由
- 前后端分离
- SPA\前端路由

#### 2.2 路由的基本设置

- 安装vue-router
- Vue.use ->创建VueRouter对象 ->挂载到Vue实例上
- 配置映射关系
  	1. 创建组件
   	2. 配置映射关系
   	3. 使用router-link/router-view

#### 2.3. 细节处理

- 默认路由：redirect
- mode:history
- router-link -> tag/replace/active-class

#### 2.4. 动态路由

- /user/:id
- this.$route.params.id

#### 2.5 参数的传递

- params
- query -> URL
- URL:
  - `协议://本地主机:端口/路径?查询`
  - `scheme://localhost:port/path?query` 默认端口是80

#### 2.6 路由嵌套

- children:[]

#### 2.7 导航守卫

- 全局导航守卫
- 路由独享守卫
- 组件类守卫



#### 2.8 Keep-alive



#### 2.9 TabBar的封装过程





### 三、Vuex



### 四、网络请求封装(axios)







