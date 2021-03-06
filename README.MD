# vue-tap

> a v-tap directive of vue.js

## How To use

> * ES6

``` bash
# install v-tap  
npm install v-tap --save; 

# 请注意！是**v-tap** 不是 **vue-tap**
```

```javascript
import vueTap from 'v-tap';
Vue.use(vueTap);
```

> * 直接引入
```html
<script src="./vue.js"></script>
<script src="./vue-tap.js"></script>
```


## Example

```html
// 具体请看demo  test-href.html
<!--如果想要快速跳转直接写v-tap即可不用写任何参数-->
<a href="www" v-tap>test a标签没有href则不会跳转</a>
<p v-tap.prevent="scroll">无法滑动页面</p>
<!-- 这样的a标签可以进行一些处理而不跳转 -->
<a v-tap.prevent="callback" href="这是无法跳转的">这是无法跳转的</a>
<!--这样一样会直接快速跳转不会执行cant 除非设置了prevent-->
<a href="aaa" v-tap="callback">can't</a>
```

```javascript
new Vue({
	el: "body",
	methods : {
		callback : function(e) {
			//不带参数指令,e为event对象
			e.preventDefault();
			console.log('---e---',e);
			console.log('---tapObj---', e.tapObj);
		}
	}
});
```

## With parmas

```html
<ul>
	<li v-for="el in list"
		v-tap="args($index,el,$event)"
			>
		{{el.name}}---{{el.age}}
	</li>
</ul>
```

```javascript
args : function(index,el,e) {
	// v-for循环带参数的回调
	console.log('---index---',index);
	console.log('---el---',el);
	console.log('---e---',e);
	console.log(e.tapObj);
	//e.tapObj 可获得 tap的一些参数
	//pageX,pageY,clientX,clientY,distanceX,distanceY
	//后面2个分别的手指可能移动的位置(以后可用于拓展手势)
}
```

### 2016.9.19(update)

> * 优化了a标签快速跳转逻辑,可以直接在 <a href="xxx" v-tap></a> 写v-tap指令,这样即可快速跳转

### 2016.8.26(update)

> * 发布npm, 各位可用`npm i v-tap --save;`下载使用
> * 重写了currentTarget对象,避免currentTarget为null的情况
> * fix : 判断el是否为a标签,避免获取href出错

### 2016.8.25(update)

> * 经测试没有点透问题

### 2016.8.24(update)

> * 统一为v-tap,兼容`PC`和`移动端`
> * 新增捕获a标签的href地址,点击a标签可实现快速跳转
> * 解决部分手机点击没有反应的问题
> * 准备加入npm大家庭


### 2016.1.20(merge)

> * 新增 dom带有disable属性时，tap失效

### 2015.12.22(update)

> * 新增vue-tap-click版本兼容PC和移动端,v-tap指令将自动判断使用click还是tap事件
> * vue-tap 是不带兼容版本, vue-tap-click兼容版本, 请客官自行选择进食.

