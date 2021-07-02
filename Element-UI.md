# Element UI

## 安装ElementUI

### 1. 通过vue脚手架创建项目

```bash
vue init webpack 项目名
```

### 2.  在vue脚手架中安装项目

```bash
# 下载elementui的依赖
npm i element-ui -S

# 指定当前项目中使用elementui 参考官网快速上手
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

# 在vue脚手架中使用elementUI
Vue。user(ElementUI);
```

## 组件

### 按钮 button

#### 按钮组件（实例）

```html
<!--
	默认样式按钮
-->
<el-row>
  <el-button>默认按钮</el-button>
  <el-button type="primary">主要按钮</el-button>
  <el-button type="success">成功按钮</el-button>
  <el-button type="info">信息按钮</el-button>
  <el-button type="warning">警告按钮</el-button>
  <el-button type="danger">危险按钮</el-button>
</el-row>

<!--
	简洁按钮 鼠标移动上去才会显示北京颜色
-->
<el-row>
  <el-button plain>朴素按钮</el-button>
  <el-button type="primary" plain>主要按钮</el-button>
  <el-button type="success" plain>成功按钮</el-button>
  <el-button type="info" plain>信息按钮</el-button>
  <el-button type="warning" plain>警告按钮</el-button>
  <el-button type="danger" plain>危险按钮</el-button>
</el-row>

<!--
	圆角按钮 round
-->
<el-row>
  <el-button round>圆角按钮</el-button>
  <el-button type="primary" round>主要按钮</el-button>
  <el-button type="success" round>成功按钮</el-button>
  <el-button type="info" round>信息按钮</el-button>
  <el-button type="warning" round>警告按钮</el-button>
  <el-button type="danger" round>危险按钮</el-button>
</el-row>

<!--
	图标按钮 icon
-->
<el-row>
  <el-button icon="el-icon-search" circle></el-button>
  <el-button type="primary" icon="el-icon-edit" circle></el-button>
  <el-button type="success" icon="el-icon-check" circle></el-button>
  <el-button type="info" icon="el-icon-message" circle></el-button>
  <el-button type="warning" icon="el-icon-star-off" circle></el-button>
  <el-button type="danger" icon="el-icon-delete" circle></el-button>
</el-row>
```

#### 按钮组件的详细使用

**总结：使用elementUI，ui的相关组件时需要注意的是，所有组件都是el-组件名开头**

#### 创建按钮

#### 按钮属性的使用

```html
<el-button type="primary" 属性名=属性值></el-button>

<el-button type="warning" size="mini" plain circle icon="el-icon-loading"></el-button>
```



**在elementui中所有组件的属性全部使用在组件标签上**

按钮组的使用

```html
<el-button-group>
  <el-button type="primary" icon="el-icon-arrow-left">上一页</el-button>
  <el-button type="primary">下一页<i class="el-icon-arrow-right el-icon--right"></i></el-button>
</el-button-group>
```

==注意==

- 在element ui中所有组件都是``el-组件名称``方式进行命名
- 在element ui中组件的属性使用`都是直接属性名=属性值方式写在对应的组件标签上`

### 文字链接组件 link

#### 文字链接组件的创建

```html
<el-link>默认链接</el-link>
```

#### 文字链接组件属性的使用

`primary 黄色 / success 绿色 / warning 黄色 / danger 红色 / info 灰色`

```html
<el-link type="primary" :underline="isunderline">默认链接</el-link>
<el-link type="success">默认链接</el-link>
<el-link type="warning" disabled>默认链接</el-link>
<el-link type="danger">默认链接</el-link>
<el-link type="info">默认链接</el-link>
```



### Layout（栅格） 布局组件的使用

`通过基础的 24 分栏，迅速渐变地创建布局`

`在element ui中布局组件将页面划分为多个行row，每行最多分为24栏(列)`

#### 使用Layout组件

```html
<el-row>
    <!--
		超出部分自动换行展示
	-->
    <el-col :span="2">占用两份</el-col>
</el-row>
```

`注意`

- 在一个布局组件中，是由行和列组合而成
- 在使用时，要区分`row属性`和`col属性`

#### 属性的使用

- 行属性的使用

  ```html
  <el-row :gutter="10" tag="span">
    <el-col :span="6"><div style="border: 1px pink solid">占用6份</div></el-col>
    <el-col :span="6"><div style="border: 1px pink solid">占用6份</div></el-col>
    <el-col :span="6"><div style="border: 1px pink solid">占用6份</div></el-col>
    <el-col :span="6"><div style="border: 1px pink solid">占用6份</div></el-col>
  </el-row>
  ```

- 列属性的使用

  ```html
  <h2>Layout属性中使用偏移offset</h2>
    <el-row>
      <el-col :span="12" :offset="3" :push="3" xs><div style="border: 1px pink solid">占用12份</div></el-col>
      <el-col :span="6"><div style="border: 1px pink solid">占用6份</div></el-col>
  </el-row>
  ```

  

### Container 布局容器组件

#### 创建布局容器

```html
<el-constainer>
</el-constainer>
```

#### 容器中包含的子元素

`<el-header>`：顶栏容器。

`<el-aside>`：侧边栏容器。

`<el-main>`：主要区域容器。

`<el-footer>`：底栏容器。

#### 容器的嵌套使用

```html
	<!-- 创建容器 -->
    <el-container>
      <!-- header -->
      <el-header>
        <div style="border: 1px solid gray"><h2>我是标题</h2></div>
      </el-header>
      <!-- asider -->
      <el-container>
        <el-aside>
          <div style="border: 1px solid pink"><h2>我是菜单</h2></div>
        </el-aside>
        <!-- main -->
        <el-main>
          <div style="border: 1px solid pink">
            <h2>我是中心内容</h2>
          </div>
        </el-main>
      </el-container>
      <el-footer>
        <div style="border: 1px solid pink">
          <h2>我是页脚</h2>
        </div>
      </el-footer>
    </el-container>
```

#### 水平容器

`注意：当子元素中没有 el-header 或 el-footer 时容器排列为水平`

```html
<el-container direction="horizontal">
      <!-- header -->
      <el-header>
        <div><h2>我是标题</h2></div>
      </el-header>
      <!-- asider -->
      <el-container>
        <el-aside>
          <div><h2>我是菜单</h2></div>
        </el-aside>
        <!-- main -->
        <el-main>
          <div>
            <h2>我是中心内容</h2>
          </div>
        </el-main>
      </el-container>
      <el-footer>
        <div>
          <h2>我是页脚</h2>
        </div>
      </el-footer>
    </el-container>
```

#### 垂直容器

```html
<el-container direction="vertical">
      <!-- header -->
      <el-header>
        <div><h2>我是标题</h2></div>
      </el-header>
      <!-- asider -->
      <el-container>
        <el-aside>
          <div><h2>我是菜单</h2></div>
        </el-aside>
        <!-- main -->
        <el-main>
          <div>
            <h2>我是中心内容</h2>
          </div>
        </el-main>
      </el-container>
      <el-footer>
        <div>
          <h2>我是页脚</h2>
        </div>
      </el-footer>
    </el-container>
```

### Form相关组件

#### Radio 单选框

1. 创建Radio按钮

   ```html
   <h2>Radio组件使用</h2>
   <!-- 组件创建 -->
   <el-radio v-model="label" label="男">男</el-radio>
   <el-radio v-model="label" label="女">女</el-radio>
   
   <script>
   export default {
     name: "Radio",
     data(){
       return{
         label: '男'
       }
     }
   }
   </script>
   ```

   `注意：在使用radio单选按钮时，至少加入v-model和label两个属性`

2. Radio使用属性

   ```html
   <el-radio v-model="label" name="gender" disabled label="男">男</el-radio>
   <el-radio v-model="label" name="gender" :border="true" label="女">女</el-radio>
   <el-radio v-model="label" border size="small" label="女">女</el-radio>
   <el-radio v-model="label" border size="mini" label="女">女</el-radio>
   <el-radio v-model="label" border size="medium" label="test"></el-radio>
   ```

   

3. Radio事件的使用

   ```html
   <el-radio v-model="label" @change="aa" name="gender" label="男">男</el-radio>
   <el-radio v-model="label" @change="aa" name="gender" label="女">女</el-radio>
   
   <!--js中的代码-->
   <script>
   export default {
     name: "Radio",
     data(){
       return{
         label: '男'
       }
     },
     methods:{
       aa(){	//定义的事件处理函数
         console.log(this.label);
       }
     }
   }
   </script>
   
   ```

   `总结`

   - 事件的使用也是和属性使用时一致的，都是写在对应的组件标签上
   - 事件在使用时，必须使用vue中绑定事件的方式进行使用，如@事件名=事件处理函数（绑定在vue组件中对应函数）

4. Radio按钮组

   ```html
   <h2>单选按钮组</h2>
       <!-- 创建单选按钮组 -->
   <el-radio-group v-model="radio">
     <el-radio :label="3">备选项3</el-radio>
     <el-radio :label="6">备选项6</el-radio>
     <el-radio :label="9">备选项9</el-radio>
   </el-radio-group>
   <!--vue中data中数据-->
   data() {
       return {
         radio: 3,
       };
     }
   
   <!--或者也可以写成这种形式-->
   <h2>单选按钮组</h2>
   <!-- 创建单选按钮组 -->
   <el-radio-group v-model="radio">
     <el-radio label="3">备选项3</el-radio>
     <el-radio label="6">备选项6</el-radio>
     <el-radio label="9">备选项9</el-radio>
   </el-radio-group>
   <!--vue中data中数据-->
   data() {
       return {
         radio: "3",
       };
     },
   ```

   

### checkbox组件的使用

1. 创建checkbox组件

2. 属性使用

   ```html
   <el-checkbox v-model="checked" true-label="烟台">烟台</el-checkbox>
   <el-checkbox v-model="checked" disabled true-label="青岛">青岛</el-checkbox>
   <el-checkbox v-model="checked" true-label="天津">天津</el-checkbox>
   ```

   

3. 事件使用

4. 复选框组

   ```html
   <el-checkbox-group v-model="checkList">
       <el-checkbox label="复选框 A"></el-checkbox>
       <el-checkbox label="复选框 B"></el-checkbox>
       <el-checkbox label="复选框 C"></el-checkbox>
       <el-checkbox label="禁用" disabled></el-checkbox>
       <el-checkbox label="选中且禁用" disabled></el-checkbox>
     </el-checkbox-group>
   <!--在data中写checkList:[]-->
   ```

   

### input组件的使用

1. 创建组件

   ```html
   <el-input v-model="name"></el-input>
   
   <script>
   export default {
     name: "Input",
     data(){
       return {
         name: 'niko'
       }
     }
   }
   </script>
   ```

   

2. 组件属性

   ```html
   <el-input v-model="name" disabled type="textarea"></el-input>
   <el-input v-model="price" :maxlength="10" show-word-limit></el-input>
   <el-input prefix-icon="el-icon-user-solid" placeholder="请输入用户名" v-model="username" clearable></el-input>
   <el-input suffix-icon="el-icon-star-off" placeholder="请输入密码" show-password type="password" v-model="password" clearable></el-input>
   <script>
   export default {
     name: "Input",
     data(){
       return {
         name: 'niko',
         price: 0.0,
         username:"",
         password: ""
       }
     }
   }
   </script>
   ```

   

3. 事件的使用

   ```html
   <el-input v-model="username" @blur="aaa" @focus="bbb"></el-input>
   methods:{
     aaa(){
       alert("失去焦点")
     },
     bbb(){
       alert("获取焦点")
     }
   }
   ```

   

4. 方法的使用

   ```html
   <h2>方法的使用</h2>
   <el-input v-model="username" ref="inputs"></el-input>
   <el-button @click="focusInputs">focus方法</el-button>
   <el-button @click="blurInputs">blur方法</el-button>
   
   methods:{
       focusInputs(){
         this.$refs.inputs.focus();
       },
       blurInputs(){
         this.$refs.inputs.blur();
       },
       blurInputs(){
         this.$refs.inputs.blur();
       },
     }
   ```

   `总结`

   - 在使用组件的方法时，需要在对应的组件中加入`ref = "组件别名"`
   - 在调用方法时直接使用`this.$refs.组件别名.方法名()`

`总结`

- 在使用组件的方法时需要在对应的组件中加入`ref="组件别名"`
- 在调用方法时直接使用`this.$refs.组件名.方法名`

​	`注意：在elementUI中所有组件都存在 属性 事件 方法`

​	`属性`：直接卸载对应组件标签上 使用方式：`属性名=属性值`方式

​	`事件`：直接使用vue绑定事件方式卸载对应的组件标签上 使用方式`@事件名=vue事件处理函数`

​	`方法`：1. 在对应组件标签上使用`ref=组件别名` 2.通过使用`this.$refs.组件别名.方法名`进行调用

### select组件的使用

1. 组件创建

   ```html
   <!--
   	数据写死在页面上
   	下拉列表中必须存在option的value属性值
   	要求select中必须绑定v-model
   -->
   <el-select v-model="cityname">
     <el-option value="北京">北京</el-option>
     <el-option value="天津">天津</el-option>
   </el-select>
   
   <!--动态获取数据-->
   <el-select>
     <el-option v-for="item in options" :v-key="item.id" :value="item.name" :label="item.value"></el-option>
   </el-select>
   
   <script>
   export default {
     name:"Select",
     data (){
       return {
         options: [
           {id: "1", name:"研发室"},
           {id: "2", name:"小卖部"},
           {id: "3", name:"小米部"},
         ]
       }
     }
   }
   </script>
   
   <!--获取下拉列表中选中数据-->
   <el-select v-model="cityid">
         <el-option 
           v-for="item in options" 
           :key="item.value"
           :label="item.value" 
           :value="item.name" ></el-option>
   </el-select>
   <script>
   export default {
     name:"Select",
     data (){
       return {
         options: [
           {id: "1", name:"研发室"},
           {id: "2", name:"小卖部"},
           {id: "3", name:"小米部"},
         ],
         cityid: ""
       }
     }
   }
   </script>
   ```

   

2. 属性使用

   ```html
   <el-select v-model="cityid" multiple clearable>
     ....
   </el-select>
   ```

   

3. 事件的使用

   ```html
   <el-select v-model="cityid" value-key="id" @change="aaa" multiple clearable>
         <el-option 
           v-for="item in options" 
           :key="item.id"
           :label="item.name" 
           :value="item.name" ></el-option>
       </el-select>
   <script>
   export default {
     name:"Select",
     data (){
       return {
         options: [
           {id: "1", name:"研发室"},
           {id: "2", name:"小卖部"},
           {id: "3", name:"小米部"},
         ],
         cityid: "",
         cityname: "",
         city:''
       }
     },
     methods:{
       aaa(value){
         console.log(value)
       }
     }
   }
   </script>
   ```

   

4. 方法的使用

   ```html
   <!--
   	给组件通过ref起别名并绑定到vue实例中
   	调用方法
   -->
   <el-select v-model="cityid" value-key="id" @change="aaa" multiple clearable ref="select">
         <el-option 
           v-for="item in options" 
           :key="item.id"
           :label="item.name" 
           :value="item.name" ></el-option>
   </el-select>
   <el-button @click="bbb">获取焦点</el-button>
   <script>
   export default {
     name:"Select",
     data (){
       return {
         options: [
           {id: "1", name:"研发室"},
           {id: "2", name:"小卖部"},
           {id: "3", name:"小米部"},
         ],
         cityid: "",
         cityname: "",
         city:''
       }
     },
     methods:{
       aaa(value){
         console.log(value)
       },
       bbb(){
         this.$refs.select.focus()
       }
     }
   }
   </script>
   ```

   

### switch组件的使用

```html
<el-switch v-model="value" active-text="打开" :active-value="true" inactive-text="关闭" active-color="#13ce66" inactive-color="#ff4949" :inactive-value="false" :width="100"></el-switch>
<script>
export default {
  name: "Switchs",
  data(){
    return {
      value: true
    }
  }
}
</script>
```

### DatePicker的使用

1. 组件创建

   ```html
   <el-date-picker v-model="createDate"></el-date-picker>
   ```

   

2. 属性

   ```html
   <el-date-picker
       v-model="createDate" :editable="false" :clearable="false"
       type="datetimerange"
       start-placeholde="开始时间"
       end-placeholde="结束时间">
   </el-date-picker>
   
   <script>
   export default {
     name:"DatePickers",
     data(){
       return {
         createDate:''
       }
     }
   }
   </script>
   ```

   

3. Picker Options & Shortcuts

- Shortcuts 用来增加日期组件的快捷面板
- Picker Option 用来对日期控件做自定义配置

###  Upload的使用

1. 创建组件

   ```html
   <el-upload action="https://jsonplaceholder.typicode.com/posts/" :file-list="fileList">
     <el-button size="small" type="primary">点击上传</el-button>
   </el-upload>
   <script>
   export default {
     name:"Upload",
     data(){
       return {
         fileList: [{name: 'food.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}, {name: 'food2.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}]
       }
     }
   }
   </script>
   ```

   `注意：在使用upload组件时必须设置action属性，action属性为必要参数不能省略`

2. 组件属性

   ```html
   <el-upload
         :data="info"
         name="pic"
         :show-file-list="true"
         :drag="true"
         accept=".txt,.png"
         :on-preview="show"
         :on-remove="remove"
         :limit="5"
         :on-exceed="exceed"
         :before-remove="beforeRemove"
         multiple
         action="https://jsonplaceholder.typicode.com/posts/"
         :file-list="fileList"
       >
         <i class="el-icon-upload"></i>
         <div class="el-upload__text">
           将文件拖到此处，或<em>点击上传</em>
         </div>
         <div class="el-upload__tip" slot="tip">
             只能上传jpg/png文件，且不超过500kb
           </div>
       </el-upload>
   <script>
   export default {
     name: "Upload",
     data() {
       return {
         fileList: [
           {
             name: "food.jpeg",
             url:
               "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100",
           },
           {
             name: "food2.jpeg",
             url:
               "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100",
           },
         ],
         info: { id: "21" },
       }
     },
     methods:{
       show(file){
         console.log(file)
       },
       remove(file,fileList){
         console.log(file,fileList)
       },
       beforeRemove(file,fileList){
         if(fileList.length<3){
           alert("文件的个数不能少于三个")
           return false;
         }
       },
       exceed(file,fileList){
         alert("文件超出个数限制")
       }
     }
   };
   </script>
   ```


   - 在使用upload组件时没有event事件，所有事件都是属性事件

3. 方法的使用

   ```html
   <el-upload ref="upload" ...>...</el-upload>
   <el-button @click="clearFiles">调用方法测试</el-button>
   clearFiles(){
     this.$refs.upload.clearFiles();
     //this.$refs.upload.abort();
     //this.$refs.upload.submit();
   }
   ```

   

### Form组件的使用

1. 组件的创建

   ```html
   <el-form ref="form" :model="form" label-width="80px">
         <el-form-item label="活动名称">
           <el-input v-model="form.name"></el-input>
         </el-form-item>
       ...
         <el-form-item>
           <el-button type="primary" @click="onSubmit">立即创建</el-button>
           <el-button>取消</el-button>
         </el-form-item>
       </el-form>
   
   <script>
   export default {
     name: "Form",
     data() {
       return {
         form: {
           name: "",
           ...
         },
       };
     },
     methods: {
       onSubmit() {
         console.log("submit!");
       },
     },
   };
   </script>
   ```

   

2. 内联表单(行内表单)

   ```html
   <el-form :inline="true"></el-form>
   ```

   `通过设置inline=true来设置内联表单`

3. 表单的验证

   `使用说明：`

   > Form 组件提供了表单验证的功能，只需要通过 `rules` 属性传入约定的验证规则，并将 Form-Item 的 `prop` 属性设置为需校验的字段名即可。校验规则参见 [async-validator](https://github.com/yiminghe/async-validator

### 消息提示

#### 警告提示

1. 组件创建

   ```html
   <el-alert title="成功消息提示" :closable="false" type="success">
         <div slot>辅助信息</div>
       </el-alert>
       <el-alert title="成功消息提示" type="info"></el-alert>
       <el-alert title="成功消息提示" type="warning"></el-alert>
       <el-alert title="成功消息提示" type="error"></el-alert>
   ```

   

2. 属性使用

   ```html
   <el-alert title="成功消息提示" effect="dark" :show-icon="true" center :closable="false" type="success">
     <div slot>辅助信息</div>
   </el-alert>
   ```

   

#### Message消息提示

1. 创建组件

   - `注意：这个组件的创建无法在页面中书写任何标签，他是一个js插件，在需要展示消息提示的位置直接调用提供的js插件方法即可`

   ```js
   // 创建最简单的消息
   this.$message('这是一个消息提示')
   // 自定义消息提示
   const h = this.$createElement;
   this.$message({
     message: h("p", null, [
       h("span", null, "订单创建成功，您的订单编号为:"),
       h("i", { style: "color: teal" }, "87"),
     ]),
   });
   // 不同主题的消息提示
   // 主题样式 success info warning error
   this.$message({
     message:'这是信息提示',
     type:'success'
   });
   // 属性使用
   showMsg() {
     this.$message({
       message: "这是信息提示",
       type: "success",
       showClose: true,
       center: true,
       iconClass: "el-icon-user-solid",
       duration: 0,
     });
   },
   // 方法的使用
   this.$message.closeAll()
   ```

   

### table组件的使用

1. 组件的创建

   ```html
   <el-table :data="tableData">
         <el-table-column label="编号" prop="id"></el-table-column>
         <el-table-column label="姓名" prop="name"></el-table-column>
         <el-table-column label="年龄" prop="age"></el-table-column>
         <el-table-column label="邮箱" prop="email"></el-table-column>
       </el-table>
   <script>
   export default {
     name:"Table",
     data(){
       return {
         tableData:[
           {id:21, name:'niko',age:23, email:'43@qq.com'},
           {id:22, name:'lalala',age:23, email:'11111@qq.com'},
         ]
       }
     }
   }
   </script>
   ```

   

2. 表格中的列属性

   - `el-table`

   ```html
   <el-table :data="tableData" border>
         <el-table-column
           label="编号"
           :resizable="false"
           prop="id"
           width="100px"
           fixed="right"
           header-align="left"
           align="center"
         ></el-table-column>
         <el-table-column label="姓名" prop="name"></el-table-column>
         <el-table-column
           label="年龄"
           :sort-method="sorts"
           sortable
           prop="age"
         ></el-table-column>
         <el-table-column label="邮箱" prop="email"></el-table-column>
         <el-table-column
           label="部门"
           prop="dept.name"
           :formatter="showDept"
         ></el-table-column>
       </el-table>
   
   <script>
   export default {
     name: "Table",
     data() {
       return {
         tableData: [
           {
             id: 21,
             name: "niko",
             age: 23,
             email: "43@qq.com",
             dept: { id: 1, name: "研发部" },
           },
           {
             id: 22,
             name: "lalala",
             age: 21,
             email: "11111@qq.com",
             dept: { id: 2, name: "小卖部" },
           },
           { id: 23, name: "嘟嘟嘟", age: 26, email: "222222@qq.com", dept: {} },
         ],
       };
     },
     methods: {
       sorts(a, b) {
         return a.age - b.age;
       },
       showDept(row, column, cellValue, index) {
         console.log("row", row);
         console.log("column", column);
         console.log("cellValue", cellValue);
         // console.log("index",index)
         if (cellValue) {
           return cellValue;
         }
         return "暂无部门";
       },
     },
   };
   </script>
   ```

   

3. 表格属性

   ```html
   <el-table :data="tableData" border highlight-current-row stripe></el-table>
   ```

   











