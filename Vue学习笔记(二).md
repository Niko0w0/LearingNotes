## 一、组件化开发


### 组件化开发高级

#### 1. slot - 插槽的基本使用

组件的思想是可以复用的

 1. 插槽的基本使用 `<slot></slot>`

 2. 插槽的默认值  `<slot><button></button></slot>`

 3. 如果有多个值，同时收入到组件进行替换时，一起作为替换元素

    ```html
    <div id="app">
      <cpn></cpn>
      <cpn></cpn>
      <cpn></cpn>
      <cpn></cpn>
      <cpn>
        <span>哈哈哈哈</span>
        <div>嘟嘟嘟</div>
      </cpn>
      <cpn></cpn>
      <cpn><div>啦啦啦</div></cpn>
    </div>
    <template id="cpn">
      <div>
        <h2>我是组件</h2>
        <p>我是组件，哈哈哈</p>
          <!-- 插槽默认值 -->
        <slot><button>按钮</button></slot>
      </div>
    </template>
    <script src="../js/vue.js"></script>
    <script>
      const app = new Vue({
        el:"#app",
        data:{},
        components:{
          cpn:{
            template : "#cpn"
          }
        }
      })
    </script>
    ```



#### slot - 具名插槽的使用

具名插槽可以让插槽按指定的顺序填充，没有具名的插槽是按照填充的顺序排列的，而具名插槽可以自定义排列。

```html
  <div id="app">
    <cpn></cpn>
    <cpn><span>标题</span></cpn>
    <cpn><span slot="center">标题</span></cpn>
    
    <!--参考他人github代码-->
    <cpn>
      <span>具名插槽</span>
      <span slot="left">这是左边具名插槽</span>
      <!-- 新语法 -->
      <template v-slot:center>这是中间具名插槽</template>
      <!-- 新语法缩写 -->
      <template #right>这是右边具名插槽</template>
    </cpn>
  </div>
  
  <template id="cpn">
    <div>
      <!--
		如果有多个按顺序排列。具名插槽按照自定义的顺序排列。
		定义具名插槽，使用name属性，给插槽定义一个名字。
		使用具名插槽，在自定义组件标签内使用slot="left"，插入指定插槽
	  -->
      <slot name="left"><span>左边</span></slot>
      <slot name="center"><span>中间</span></slot>
      <slot name="right"><span>右边</span></slot>

      <slot><span>哈哈哈哈</span></slot>
    </div>
  </template>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el:"#app",
      data:{},
      components:{
        cpn:{
          template : "#cpn"
        }
      }
    })
  </script>
```



#### 3. 编译的作用域



```html
  <!-- 父组件 -->
  <div id="app">
    <!-- 使用的vue实例作用域的isShow -->
    <cpn v-show="isShow"></cpn>
  </div>
  <!-- 子组件 -->
  <template id="cpn">
    <div>
      <h2>我是子组件</h2>
      <p>哈哈哈</p>
      <!-- 组件作用域，使用的子组件的作用域 -->
      <button v-show="isShow"></button>
    </div>
  </template>

  <script src="../js/vue.js"></script>

  <script>
    const cpn = {
      template: "#cpn",
      data() {
        return {
          isShwo:false
        }
      },
    }
    const app = new Vue({
      el: "#app",
      data() {
        return {
          message: "我是父组件消息",
          isShow:true
        }
      },
      components: {
        cpn
      },
    })
  </script>
```

子组件使用的是子组件的isShow，子组件为false，所以button没显示，被隐藏。

#### 4. 作用域插槽案例

父组件替换插槽的标签，但是内容是由子组件来提供。

当组件需要在多个父组件多个界面展示的时候，将内容放在子组件插槽中，父组件只需要告诉子组件使用什么方式展示界面。

==组件中使用`slot-scope="slot"`**（2.6.0已经废弃）**给插槽属性命名，在通过`slot`调用绑定在插槽上的属性。也可以使用`v-slot="slot"`。==

```html
  <div id="app">
    <cpn></cpn>
    <cpn>
      <!-- 
        //！ 这样是不可以的 
        <span v-for="item in pLanguages">{{item}}</span> 
      -->
      <!-- 目的是获取子组件中的pLanguages -->
      <template slot-scope="slot">
        <span v-for="item in slot.data">{{item}} - </span>
      </template>
    </cpn>

    <cpn>
      <template slot-scope="slot">
        <span>{{slot.data.join(' * ')}}</span>
      </template>
    </cpn>
  </div>
  
  <template id="cpn">
    <div>
      <slot :data="pLanguages">
        <ul>
          <li v-for="item in pLanguages">{{item}}</li>
        </ul>
      </slot>
    </div>
  </template>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el:"#app",
      data:{
        message:'你好啊'
      },
      components:{
        cpn:{
          template : "#cpn",
          data(){
            return {
              pLanguages:['JavaScript','C++','C#','Python','Go','Swift']
            }
          }
        }
      }
    })
  </script>
```



### Vue示例的生命周期

![img](Vue学习笔记(二).assets/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f6b7269736c696e7a68616f2f494d47636c6f75642f696d672f32303230303531363038353234322e706e67)

建议看这个

[Vue示例的生命周期]([https://github.com/krislinzhao/StudyNotes/blob/master/Vue/13-Vue%E5%AE%9E%E4%BE%8B%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.md](https://github.com/krislinzhao/StudyNotes/blob/master/Vue/13-Vue实例的生命周期.md))




## 二、前端模块化

### 1. 为什么要模块化

aaa.js

```javascript
var name = "小明"
var age=22

function sum(num1,num2){
  return num1 + num2
}
  
var flag = true

if(flag){
  console.log(sum(10,20));
}
```



bbb.js

```javascript
var name="小红"
var flag=false
```

mmm.js

```javascript
if(flag){
  console.log("flag是true")
}
```

在index.html中导入这些js文件

```html
  <script src="aaa.js" ></script>
  <script src="bbb.js" ></script>
  <script src="ccc.js" ></script>
```

此时在aaa.js中定义的`flag`是`true`，但是bbb.js中也定义了`flag`为`false`，所以mmm.js文件并没有打印出“flag是true”。

这是全局变量同名所引发的问题

### 2. 模块化的实现 - 解决全局变量同名问题

aaa.js

```javascript
var name = 'xiaoming'
var age = 18
var flag = true

function sum(num1, num2) {
  return num1 + num2;
}

if (flag) {
  console.log(sum(20, 30));
}

// 导出方式1
export {
  flag,
  sum
}

// 导出方式2
export var num1 = 1000;
export var height = 188;

//导出函数类
export function mul(n1,n2){
  return n1+n2;
}

export class Person{
  run(){
    console.log('run');
  }
}

// export default
// 某些情况下，一个模块中包含某个功能，我们并不希望给这个功能命令，而且让导入者可以自己来命名
// 这个时候就可以使用export default
// 一个js文件中只能有一个default
// const address = '烟台市'
// export default address;
export default function(argument){
  console.log(argument);
}
```

bbb.js

```javascript
var name = 'xiaohong'
var flag = false
```

mmm.js

```javascript
// 导入{}中定义的变量
import {flag,sum} from './aaa.js';
if(flag){
  console.log("小明是天才");
  console.log(sum(10,20))
}

// 直接导入export定义的变量
import {num1,height} from './aaa.js';
console.log(num1,height);

// 导入export的function
import {mul} from './aaa.js';
console.log(mul(20,40));

import {Person} from './aaa.js';
const p = new Person();
p.run();

// 导入default中的内容
import addr from './aaa.js';
console.log(addr);

// 统一导入
// 相当于将文件中的全部导出变量存在一个对象中，从对象中取出变量
import * as aaa from './aaa.js';

```

然后在index.html中导入三个js文件，这样直接使用aaa.js导出的变量能够获得小明自己定义的flag



## 三、webpack

### 1.1 什么是webpack

`webpack`是一个JavaScript应用的静态模块打包工具

从这句话中有两个要点，**模块**和**打包**需要关注。**grunt/gulp**都可以打包，那有什么区别。

`webpack`可以支持前端模块化的一些方案，例如`AMD、CMD、CommonJS、ES6`。可以处理模块之间的依赖关系。不仅仅是js文件可以模块化，`图片、css、json`文件等等都可以模块化。

`webpack`可以将模块资源打包成一个或者多个包，并且在打包过程中可以处理资源，例如压缩图片，将`scss`转成`css`，ES6语法转成ES5语法，将TypeScript转成JavaScript等等操作。**grunt/gulp**也可以打包。

**和grunt/glup的对比**

- grunt/glup的核心是Task
  - 我们可以配置一系列的task，并且定义task要处理的事务（例如ES6/TS转化，图片压缩，scss转css）
  - 之后可以让grunt/glup来依次执行这些任务，让整个流程自动化
  - 所以grunt/glup也被称为前端自动化任务管理工具
- 看一个gulp例子
  - task将src下的js文件转化为ES5语法
  - 并输入到dist文件夹中

```
const gulp = require('gulp')
    const babel = require('gulp-babel')
    gulp.task('js'()=>
      gulp.src('src/*.js')
        .pipe(babel({
          presets:['es2015']
        }))
        .pipe(gulp.dest('dist'))
    );
```

- 什么时候使用grunt/gulp呢？
  - 如果工程依赖简单，甚至没有模块化
  - 只需要进行简单的合并/压缩
  - 如果模块复杂，相互依赖性强，我们需要使用webpack
- grunt/glup和webpack区别
  - grunt/glup更加强调的是前端自动化流程，模块化不是其核心
  - webpack加强模块化开发管理，而文件压缩/合并/预处理等功能，是附带功能

webpack的安装请参考百度

```json
//package.json文件中的内容
{
  "name": "meetwebpack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {//开发时依赖F
    "webpack": "^3.6.0"
  },
  "dependencies": {}//运行时依赖
}

```



### webpack的loader

loader是webpack中一个非常核心的概念。

webpack可以将js、图片、css处理打包，但是对于webpack本身是不能处理css、图片、ES6转ES5等。

此时就需要webpack的扩展，使用对应的loader就可以。

**loader使用**

 步骤一：通过npm安装需要使用的loader

 步骤二：通过webpack.config.js中的modules关键字下进行配置

大部分loader可以在webpack的官网找到对应的配置。





老师使用的`webpack`配置的相关版本

```xml
老师的webpack配置相关版本：
webpack
npm install webpack@3.6.0

css-loader
npm install css-loader@2.0.2 --save-dev

style-loader
npm install style-loader@0.23.1 --save-dev

less-loader
npm install --save-dev less-loader@4.1.0 less@3.9.0

url-loader
npm install --save-dev url-loader@1.1.2

file-loader
npm install file-loader@3.0.1 --save-dev
// file-loader不需要配置，只需要安装

es6转换成es5
npm install --save-dev babel-loader@7.1.5 babel-core@6.26.3 babel-preset-es2015@6.24.1

Vue
npm install vue@2.5.21 --save
npm install --save-dev vue-loader@13.0.0 vue-template-compiler@2.5.21

html-plugin
npm install html-webpack-plugin@3.2.0 --save-dev

//在开发时不建议使用丑化，在调试时就会很不方便
uglifyjs-webpack-plugin
npm install uglifyjs-webpack-plugin@1.1.1 --save-dev

//安装本地服务器
webpack-dev-server
npm install webpack-dev-server@2.9.3 --save-dev

webpack-merge
npm install webpack-merge@4.1.5 --save-dev

npm install -g @vue/cli@3.2.1
npm install @vue/cli-init@3.2.0 -g

vue-router
npm install vue-router --save

npm install vuex@3.0.1 --save

npm install axios@0.18.0 --save
```



![image-20200830194404905](Vue学习笔记(二).assets/image-20200830194404905.png)

![image-20200901100437371](Vue学习笔记(二).assets/image-20200901100437371.png)

![image-20200901100800295](Vue学习笔记(二).assets/image-20200901100800295.png)



## 四、Vue CLI

### 什么是vue-cli

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，提供：

- 通过 `@vue/cli` 搭建交互式的项目脚手架。
- 通过 `@vue/cli` + `@vue/cli-service-global` 快速开始零配置原型开发。
- 一个运行时依赖 (`@vue/cli-service`)，该依赖：
  - 可升级；
  - 基于 webpack 构建，并带有合理的默认配置；
  - 可以通过项目内的配置文件进行配置；
  - 可以通过插件进行扩展。
- 一个丰富的官方插件集合，集成了前端生态中最好的工具。
- 一套完全图形化的创建和管理 Vue.js 项目的用户界面。

Vue CLI 致力于将 Vue 生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置即可平稳衔接，这样你可以专注在撰写应用上，而不必花好几天去纠结配置的问题。与此同时，它也为每个工具提供了调整配置的灵活性，无需 eject。



### CLI什么意思

- CLI是Command-Line Interface，即命令行界面，也叫脚手架。
- vue cli 是vue.js官方发布的一个vue.js项目的脚手架
- 使用vue-cli可以快速搭建vue开发环境和对应的webpack配置

### 1.3 vue cli使用

**vue cli使用前提node**

vue cli依赖nodejs环境，vue cli就是使用了webpack的模板。

安装vue脚手架，现在脚手架版本是vue cli4

```
npm install -g @vue/cli
```

**拉取2.x模板（旧版本）**

Vue CLI >= 3 和旧版使用了相同的 `vue` 命令，所以 Vue CLI 2 (`vue-cli`) 被覆盖了。如果你仍然需要使用旧版本的 `vue init` 功能，你可以全局安装一个桥接工具：

```
npm install -g @vue/cli-init
# `vue init` 的运行效果将会跟 `vue-cli@2.x` 相同
vue init webpack my-project
```

**1.在根目录新建一个文件夹`16-vue-cli`，cd到此目录，新建一个vue-cli2的工程。**

```
cd 16-vue-cli
//全局安装桥接工具
npm install -g @vue/cli-init
//新建一个vue-cli2项目
vue init webpack 01-vuecli2test
```

注意：如果是创建vue-cli3的项目使用：

```
vue create 02-vuecli3test
```





vuecli2搭建项目

![image-20200901150831846](Vue学习笔记(二).assets/image-20200901150831846.png)

2.创建工程选项含义

![image-20200901150442905](Vue学习笔记(二).assets/image-20200901150442905.png)

- project name：项目名字（默认）
- project description：项目描述
- author：作者（会默认拉去git的配置）
- vue build：vue构建时候使用的模式
  - runtime+compiler：大多数人使用的，可以编译template模板
  - runtime-only：比compiler模式要少6kb，并且效率更高，直接使用render函数
- install vue-router：是否安装vue路由
- user eslint to lint your code：是否使用ES规范
- set up unit tests：是否使用unit测试
- setup e2e tests with nightwatch：是否使用end 2 end，点到点自动化测试
- Should we run `npm install` for you after the project has been created? (recommended)：使用npm还是yarn管理工具



全部选择完后的文件目录

![image-20200901155115064](Vue学习笔记(二).assets/image-20200901155115064.png)

build中将webpack的配置文件做了分离：

- `webpack.base.conf.js`（公共配置）
- `webpack.dev.conf.js`（开发环境）
- `webpack.prod.conf.js`（生产环境）

我们使用的脚本命令配置在`package.json`中。



1. runtime-only->代码中，不可以有任何的template
2. runtime-compiler->代码中可以有template，因为compiler可以用于编译template

```xml
// 将vue从runtime-only转换为runtime-compiler
  resolve:{
    // alias:别名
    // git config alias ''
    alias:{
      'vue$' : 'vue/dist/vue.esm.js'
    }
  }
```





## 使用路由

### 什么是路由？

- 路由就是通过互联的网络把信息从源地址传送到目的地的活动
- 路由提供了两种机制：路由和传送
  - 路由是决定数据包从来源到目的地的路径
  - 转送就是将数据转移
- 路由表
  - 路由表本质就是一个映射表，决定了数据包的指向

### 前端/后端路由

1. 后端渲染（服务端渲染） jsp技术 后端路由，后端处理URL和页面映射关系，例如springmvc中的@requestMapping注解配置的URL地址，映射前端页面
2. 前后端分离（ajax请求数据） 后端只负责提供数据 静态资源服务器（html+css+js） ajax发送网络请求后端服务器，服务器回传数据 js代码渲染dom
3. 单页面富应用（SPA页面） 前后端分离加上前端路由，前端路由的url映射表不会向服务器请求，是单独url的的页面自己的ajax请求后端，后端只提供api负责响应数据请求。改变url，页面不进行整体的刷新。 整个网站只有一个html页面。



### 3.`url`的`hash`方法和`html`的`history`方法

修改`url`但是不刷新页面的方法，`pushState`是栈结构

![image-20200907182324549](Vue学习笔记(二).assets/image-20200907182324549.png)

`history.back()`等价于`history.go(-1)`

`history.forward()`等价于`history.go(1)`

这三个结构等同于浏览器页面的前进后退





`<router-link>`是全局组件，最终被渲染成a标签，但是`<router-link>`只是标记路由指向类似一个a标签或者按钮一样，但是我们点击a标签要跳转页面或者要显示页面，所以就要用上`<router-view>`。

`<router-view>` 是用来占位的，就是路由对应的组件展示的地方，该标签会根据当前的路径，动态渲染出不同的组件。

路由切换的时候切换的是`<router-view>`挂载的组件，其他不会发生改变。

`<router-view>`默认使用hash模式，可以在index.js中配置修改为history模式。



![image-20200909102856621](Vue学习笔记(二).assets/image-20200909102856621.png)

URL：`scheme://localhost:port/path?query` 默认端口是80

`协议://本地主机:端口/路径?查询`

`meta`：元数据(描述数据的数据)

![image-20200909201958352](Vue学习笔记(二).assets/image-20200909201958352.png)



#### $route和$router是有区别的

- `$router`为`VueRoute`实例，想要导航到不同URL，则使用`$router.push`方法
- `$route`为当前`router`跳转对象里面可以获取`name`、`path`、`query`、`params`等



#### 文件路径的引用问题

```js
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      '@': resolve('src'),
      'assets': resolve('@/assets'),
      'components': resolve('@/components'),
      'views': resolve('@/views'),
    }
  }
```











