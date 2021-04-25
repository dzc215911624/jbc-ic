README
===========================

## 说明

  大家好，欢迎使用jbc-ic，使用过程中如有任何问题都可以直接反馈到我的邮箱

  * 昵称：`laoding`
  * 邮箱：<215911624@qq.com>

## jbc-ic

> javascript instruction and component 指令和组件

## 安装

``` javascript
# install
npm install jbc-ic
或者
npm i jbc-ic
```

* 安装后在main.js中添加引用，jbc-ic库是基于[jbc(基础类库)](https://www.npmjs.com/package/jbc "欢迎使用jbc基础类库，这里有丰富的基础方法，简单快捷易上手，还等什么~")和Vue开发的
* 在Vue环境下提供了一些实用指令和常用组件
* jbc-ic增加了一些数据请求方法等挂载到了jbc下
* 所以安装jbc-ic后可直接使用jbc的方法，无需单独安装jbc,jbc调用方式又类似jquery，因为jbc在没有jquery的情况下会使用别名$
* 如果用户已使用jquery，jbc会把所有方法挂载到jquery上，综上：理论上安装jbc-ic完毕，就可以使用  $.变量或方法的方式来使用 例如：$.xxx 或$.xxx(),如不使用jbc方法请忽略
* jbc-ic的指令和组件调用跟Vue一致，例如：指令（v-clearSelect）

```javascript
import jbc from 'jbc-ic'
或
import 'jbc-ic'

Vue.use(jbc)
```

* 安装完毕，举个栗子获取uuid，测试jbc方法能否正常使用

```javascript
//获取具有唯一性的字符 三种形式均可
console.log(this.uuid());
console.log($.uuid());
console.log(jbc.uuid());
```

* 测试jbc-ic指令是否正常实用

```javascript
//禁止双击选中
v-clearSelect
```

---

## 新增或调整

* 新增 弹窗组件套装 cover coverbtn covercontent


## 方法

```javascript
//基础类1
toBin(data)     //十进制转成二进制
toDec(data)     //二进制转成十进制
toArgString(obj)  //返回请求参数xxx=111&xxx=222格式的字符串
fetch(arr)    //兼容到IE9数据请求，优先使用fetch，不支持的使用ajax + promise 内部会自动去使用下面的ajax方法请求
ajax(obj)   //XMLHttpRequest请求
//例子：
jbc.fetch(url, {
      type: "get",     //请求方式get（默认） post
      method: "fetch",   //调用类型 fetch（默认） ajax（自动使用上述方法的ajax请求，请求头为：application/x-www-form-urlencoded;charset=UTF-8）
      headers:{},    //请求头 默认application/x-www-form-urlencoded;charset=UTF-8
      cache: "force-cache",   //缓存 no-cache不缓存 force-cache强制缓存（默认）
      contentType: "json", //返回数据类型 text json（默认）
      data: {}  //参数
    })
    .then((e) => {
      console.log(e);
    })
    .catch((msg) => {
      console.log(msg);
    });
vlog(data) //格式化数据，用于Observer数据控制台显示预览


//节点类
hasClass(elem, class) //是否存在样式
addClass(elem, class) //添加样式
removeClass(elem, class) //删除样式
siblings(elem, class) //获取兄弟节点

//优化类
throttle(fn, delay = 200) //节流
debounce(fn, delay = 100, immediate = true) //防抖 函数，间隔时间，是否立即执行

//动画类
animate(obj, json, interval, sp, fn) //普通方向动画
//例子：
//jbc.animate(elem,  { left: 100 }, 16, 0.1, () => {});


animateplus(options) //动画增强功能
/*
 * elements  默认值为 null  四种类型，分别是：String、Element、NodeList、Array，  要确定动画的 DOM 元素。您可以传递一个 CSS 选择器或 DOM 元素
 * easing    默认值为 out-elastic，参数类型为字符串。它主要的作用是确定动画的加速曲线。
 * transform 动画形态 translate、rotate、skew、scale
 * opacity   Array 透明度 [1 , 0.8] 其他css属性同理
 * duration  默认值为 1000，参数类型为数字，或者函数。Number、Function。确定动画的持续时间（以毫秒为单位）。 回调函数将每个元素的索引作为参数，并返回一个数字。
 * delay     默认值为 0，参数类型为数字，或者函数。Number、Function。 确定动画的延迟（以毫秒为单位）    回调函数将每个元素的索引作为参数，并返回一个数字。
 * loop      默认值为 false，参数类型为 Boolean。主要作用是确定动画是否应该重复。
 * direction 默认值为 normal，参数类型为字符串 String。确定动画的方向。reverse 向后运行动画，alternate 如果动画循环，则在每次迭代之后切换方向。
 * speed     默认值为 1，参数类型为 Number。确定动画回放速率。在创作过程中有用，可以加快长序列的某些部分（值大于 1）或减慢特定的动画以观察（小于 1 的值）。
 * optimize  默认值为 false，参数类型为 Boolean。如果设置为“动画”，则强制进行硬件加速 true。除非遇到性能问题，否则建议不要使用硬件加速，否则可能会产生有害的副作用。
 * change    默认值为 null，参数类型为 Function。定义在动画的每个帧上调用的回调函数。回调以动画进程（0 到 1 之间）作为参数，可以独立使用而不受限制 elements。
*/

//例子：
/*
 * jbc.animateplus({
 *     elements: "ul li",
 *     easing: "out-elastic 1 0.4",
 *     duration: 2000,
 *     delay: (index) => index * 100,
 *     loop: false,
 *     opacity: [1, 0.6],
 *     //left:["0px","100px"],
 *     transform: ["scale(0)", 0.88],
 *     //transform: ["rotate(0deg)", "rotate(9deg)"],
 *     direction: "normal",
 *     speed: 1,
 *   })
 *   .then(function (options) {
 *     console.log(options);
 *     jbc.animateplus({
 *       ...options,
 *       easing: "out-elastic 1.4 0.2",
 *       transform: ["translateY(0px)", "translateY(100px)"],
 *     });
 *   });
 */

```

## 指令
```javascript
  // 溢出字符以省略号代替 
  // v-shenglue="8"       表达式传值超出值用省略号代替
  // v-shenglue.min="8"   min修饰符解决中英混排，计算长度时一个汉字为2个字符
* v-shenglue
  // <a v-shenglue="8">一二三四五六七八九</a>
  // <a v-shenglue.min="8">123abc文字</a>


  // 首字符为【或《的文本缩进0.5em  无修饰符功能 针对块状元素
  // v-textIndent
  // v-textIndent:%     arg值增加【或《之外的字符检查
  // v-textIndent="0.25"    表达式传值缩进0.25
  // v-textIndent:%,a,啊,b,c="0.25"   传值和表达式综合使用
* v-textIndent


  // 禁止双击选中文字
* v-clearSelect

  // 禁止右键菜单
* v-clearRight

  // 禁止图片拖拽
* v-clearImgDrag

  // 微信中禁止容器上下晃动
* v-wxRepairShake
  // <div v-wxRepairShake><div>

  // 滑动开始
* v-touchstart
                        
  // <div v-touchstart="touchstart"><div>

  // 滑动结束 
* v-touchend                     
  // <div v-touchend="touchend"><div>

  // 轻击   
* v-tap                  
  // <div v-tap="tap"><div> 
  // tap: function (e) { // e 事件对象
  //    console.log('轻击')
  // }

  // 长按 
* v-longtap                         
  // <div v-longtap="longtap"><div>

  // 左滑
* v-swipeleft                          
  // <div v-swipeleft="swipeleft"><div>

  // 右滑   
* v-swiperight                       
  // <div v-swiperight="swiperight"><div>

  // 上滑    
* v-swipeup              
  // <div v-swipeup="swipeup"><div>

  // 下滑
* v-swipedown                     
  // <div v-swipedown="swipedown"><div>

  // 拖拽 
* v-drag                     
  // <div v-drag="drag"><div>
  // drag: function (e) { // e 坐标+事件对象
  //    console.log(e.x, e.y)
  // }


  // 返回顶部
  // v-backTop 只有点击返回顶部功能 不监听滚动条状态
  // v-baclTop:Cur  有参数时会把它作为样式名 在滚动条离开顶部时增加当前样式
  // v-backTop.hide 有修饰符hide时 在滚动条返回顶部时会隐藏当前节点，离开顶部时会显示当前节点
* v-backTop
  // <div v-backTop:Cur.hide class="backTop">返回顶部</div>


  //打字机效果
  // v-print 默认打字速率60ms，无延时
  // v-print:80 打字速率为80ms，无延时
  // v-print:80="1000" 打字速率为80ms，延时1000ms执行
* v-print
  // <p v-print>
  //    疫情重压之下 菅义伟如何挺过年关？中国经营报
  //    发布时间：12-2811:24中国经营报官方帐号
  // </p>
  // <p v-print:80="4000">国家医保局：治疗新冠肺炎药品列入国家医保目录</p>
  // <p v-print:30="5000">本次调整高度重视新冠肺炎治疗相关药品的保障工作</p>
  // <p v-print:200="5800">编辑：高晨晨</p>


```

## 组件

* `placeholder` 文本框占位提示组件
  * 回调函数：
    * `v-on:input` 监听文本框数值
    * `v-on:blur`  文本框失去焦点回调
    * `v-on:focus` 文本框获取焦点回调

| 参数 | 类型 | 默认值 | 描述 |
| :------| :----- | :---------------- | :-------------|
| msg    | String | 请输入             | 提示信息|

#### 示例
```javascript
//placeholder功能，提供基础样式
//参数msg[string]   placeholder显示文字
//属性：自动继承
//方法：提供钩子 input、blur、focus
//无指令
<placeholder
  type="text"
  maxlength="20"
  class="myClass"
  msg="请输入"
  v-model="value"
  @input="aaa"
></placeholder>
```

<br>

* `lunbo` 轮播
  * 回调函数：
    * `v-on:begincallback` 运动开始出发回调 返回当前li节点
    * `v-on:overcallback`  运动结束后触发回调 返回当前li节点
    * `v-on:initcallback` 初始化回调 返回父级节点
    * `v-on:linkAClickcallback` a标签点击回调 返回a标签的所有属性
    * `v-on:liMouseOvercallback` li标签鼠标悬停回调 返回当前li
    * `v-on:liMouseOutcallback` li标签鼠标离开回调 返回当前li

  * 插槽：
    * `v-slot:loading` .parent > .loading 内的节点自定义  无返回值
    * `v-slot:ulliDom` ul > li 内的节点自定义  返回当前li的数据
    * `v-slot:olliDom` ol > li 内的节点自定义  返回当前li的数据
    
`<lunbo></lunbo>`

| 参数 | 类型 | 默认值 | 描述 |
| :------- | :-----  | :--------- | :-------------------   |
| dataJson | Object  | {}         | 轮播的图片和链接 { list: [{href:'link',src:'imgsrc',target: '_blank',olsrc: ''}],leftAndRight:['imgsrc','imgsrc'] } |
| loop     | Number  | 6000       | 轮播速率                |
| effect   | String  | 'left'     | 轮播方式:'left','up2down'，其他暂时没有开发      |
| autoplay | Boolean | true       | 是否启用自动轮播            |
| nogap    | Boolean | true       | 是否启用无缝滚动            |
| isHaveArrow  | Boolean | true   | 是否启用左右箭头            |
| isHavePoint  | Boolean | true   | 是否启用指示小标            |
| arrowClass   | String | 'Arrow' | 自定义左右箭头样式名         |
| activeClass  | String | 'Cur'   | 自定义当前活动li和游标li样式名 默认Cur  |
| loadingMsg   | String |'loading'| 加载提示文字                |

#### 示例
```javascript
//注意：lunbo不提供基础样式！！但是它可以千变万化，多研究，性能还不错
//注意：autoplay在nogap为true时生效
//提供钩子： initcallback、overcallback、begincallback、linkAClickcallback
//提供滑动手势：左右滑动
//组件自动响应异步数据
<lunbo
  class="lunbo"
  :dataJson="lunboConfig"
  :isHaveArrow="true"
  :isHavePoint="true"
  arrowClass="Guide"
  loadingMsg="加载中..."
  :autoplay="true"
  :loop="10000"
  effect="up2down"
  @initcallback="init"
  @overcallback="animateOver"
  @begincallback="animateBegin"
>
  <template #ulliDom="data">
    <a v-bind="data">
      <img :src="data.src" alt="" />
    </a>
  </template>
  <template #olliDom><div><h3>test<h3></div></template>
</lunbo>

//数据示例
let dataJson={
  list:[
    {},
    { href:"", target:"" , olsrc:"游标图片地址"，xxx:"xxx" },//所有属性会绑定到当前li的a标签上
    {}
  ],
  leftAndRight:["左侧箭头图片地址","右侧图片地址"]
}
```

<br>


* `copytext` 点击复制指定内容到剪贴板
  * 回调函数：
    * `v-on:success` 复制成功回调
    * `v-on:error`   复制失败回调

| 参数 | 类型 | 默认值 | 描述 |
| :------| :----- | :------- | :-------------|
| msg    | String | ""       | 需要复制到剪贴板的文本 |

#### 示例
```javascript
//自动生成的a标签继承组件所有属性,a标签无样式
//属性：自动继承
//方法：提供钩子 success、error
//无指令
<copytext
  msg="需要复制到剪贴板的文本"
  href=""
  target="_blank"
  @success="copySuccess"
  @error="copyFail"
></copytext>
```

<br>


* `yzmbtn` 验证码倒计时按钮
  * 回调函数：
    * `v-on:begintimer` 点击开始回调
    * `v-on:callback`   倒计时过程回调
    * `v-on:overtimer`  结束回调

| 参数 | 类型 | 默认值 | 描述 |
| :------| :----- | :------- | :-------------|
| num       | Number | 60         | 需要倒计时的时长，单位s，1s间隔，不支持负数 |
| startdesc | String | s后可重发   | 倒计时开始显示文案 |
| enddesc   | String | 获取验证码  | 倒计时结束显示文案 |

#### 示例
```javascript
//常用于发送手机验证码，点击后锁定按钮防止重复点击
//方法：提供钩子 begintimer、callback、overtimer
<yzmbtn
  :num="5.6"
  startdesc="s"
  enddesc="获取"
  @begintimer="consolefun"
  @callback="consolefun"
  @overtimer="consolefun"
></yzmbtn>
```

<br>



* `paging` 绑定数据分页
  * 回调函数：
    * `v-on:initcallback`     初始化回调
    * `v-on:selectcallback`   选择哪页回调

  * 插槽：
    * `v-slot:showData` div样式.showListPart内节点插槽  数据返回为当前选择的页码数据
    * `v-slot:prev` 上一页插槽
    * `v-slot:next` 下一页插槽
    * `v-slot:searchPrev` 搜索部分 前往插槽
    * `v-slot:searchNext` 搜索部分 页插槽

| 参数 | 类型 | 默认值 | 描述 |
| :------| :----- | :------- | :-------------|
| dataList  | Array   | []  | 数组源数据 |
| pageSize  | Number  | 6   | 每页尺寸，显示多少条数据 |
| pageNow   | Number  | 1   | 当前是哪一页 |
| maxCount  | Number  | 5   | 最多显示的页码数 |
| isSearch  | Boolean | false   | 是否显示搜索框 |
| isTotal   | Boolean | false   | 是否显示总计信息 |

#### 示例
```javascript
//用于数组数据快速分页
<paging
  :dataList="pagingArr"
  :pageSize="3"
  :pageNow="1"
  :maxCount="3"
  @selectcallback="consolefun"
>
    <template #showData="data">
      <div v-for="(item, key) in data" :key="key">{{ item }}</div>
    </template>
    <template #prev>&lt;</template>
    <template #next>&gt;</template>
    <template #searchPrev>前往</template>
    <template #searchNext>页</template>
</paging>
```

<br>


* `tab` 页签切换父组件
  * 回调函数：
    * `v-on:clickcallback` 点击切换页签回调 返回值为索引值

  * 插槽
    * `v-slot:tabList` 页签li节点内插槽，可自定义li内节点，返回当前对象{label:"xxx",name:"xxx"}

| 参数 | 类型 | 默认值 | 描述 |
| :------| :----- | :------- | :-------------|
| value     | Number、String | 0      | 默认显示第几个页签 |

#### 示例
```javascript
//快速实现常用菜单切换、选项卡切换等类似功能，子组件标签为<part></part>
//方法：提供钩子 clickcallback
//注意：参数value如果设置了值，父组件便会去查找name值与value值一致的子组件，
//如果未查找到，则不显示，如预先不知道子组件的name值可不设置，会默认显示第一个页签
<tab
  :value="a1"
  @clickcallback="click"
>
  <template #tabList="data">
    <a>{{ data.label }}</a>
  </template>
  <part label="首页" name="a1"></part>
  <part label="关于我们" name="a2"></part>
</tab>
```

<br>

* `part` 页签切换子组件
  * 回调函数：
    * `v-on:readycallback` 切换到当前页面触发的回调 返回值为当前对象

  * 插槽
    * `v-slot:default` 自定义子标签内所有节点

  * 所需配合父组件设置的属性：
    * label 显示在父组件的选项卡菜单列表处
    * name 用于父组件识别对应页签内容区域

#### tab选项卡组件综合示例
```javascript
//解决常用菜单切换、选项卡切换等类似问题，父组件标签为<tab></tab>
//方法：提供钩子 readycallback
<tab :value="0" @clickcallback="click">
  <part
    v-for="(item, key) in arrTab"
    :key="key"
    :label="item.label"
    @readycallback="ready"
  >
    <keep-alive>
      当前是： {{ item.label + item.name }}，页签内容
    </keep-alive>
  </part>
</tab>

```

<br>


* `cover` 弹窗组件（父组件）
  * 插槽
    * `v-slot:close` 关闭按钮内容插槽
    * 提供默认插槽

| 参数 | 类型 | 默认值 | 描述 |
| :------| :----- | :------- | :-------------|
| zIndex        | Number  | 99999   | 整个弹窗标签在body内所处的层级 |
| isCloseShow   | Boolean | true    | 控制关闭弹窗按钮是否显示 |

* `covercontent` 弹窗组件（内容子组件）
  * 回调函数：
    * `v-on:readycallback` 弹出所选弹窗触发的初始化回调 返回值为当前对象
  * 插槽
    * 提供默认插槽

| 参数 | 类型 | 默认值 | 描述 |
| :------| :----- | :------- | :-------------|
| width    | Number | 500  | 当前显示的内容弹窗的宽度 |
| height   | Number | 300  | 当前显示的内容弹窗的高度 |

* `coverbtn` 弹窗组件（按钮组件）
  * 回调函数：
    * 无
  * 插槽
    * 提供默认插槽
  * 参数
    * 无
  * 需设置name属性与covercontent组件的name属性一致即可触发

* cover组件开放两个js方法
  * open 打开某个弹窗 参数name值
  * close 关闭弹窗 无参数

#### cover弹窗组件综合示例
```javascript
//解决常用弹窗js逻辑，同样只有基础样式，父组件标签为<cover></cover>
//this.cover.open(name) 打开弹窗
//this.cover.close() 关闭弹窗
<div @click="openCoverA('aa')">js打开aa</div> //js控制可根据需要使用
<div @click="closeCover()" class="btnCover">js关闭弹窗</div>

<cover>
  <covercontent name="aa" :width="200" :height="200" >弹窗a</covercontent>
  <covercontent name="bb">弹窗b</covercontent>
</cover>

//弹窗按钮组件可放置在任意位置，与<cover>标签是兄弟标签
<coverbtn name="aa">打开aa</coverbtn>//name属性跟<covercontent>属性name一致即可关联
<coverbtn name="bb">打开bb</coverbtn>

//methods部分
openCoverA: function (name) {
  //打开某个弹窗
  this.cover.open(name);
},
closeCover: function () {
  //关闭整个弹窗
  this.cover.close();
}
```

<br>


----

[回到顶部](#readme)
