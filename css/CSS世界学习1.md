### 第3章 流、元素与基本尺寸
##### 块级元素：里元素默认的display值是list-item,<table>元素默认的display值是table，但是他们均是“块级元素“，因为他们都符合块级元素的基本特征，
也就是一个水平流上只能单独显示一个元素，多个元素则换行显示。
由于块级元素的换行特性，所以他们可以配合clear属性来清除浮动带来的影响。
```
.clear:after{
    content:"";
    display:table;//也可以是block，或者是list-item
    clear:both;
}
```
ie不支持伪元素的display值为list-item
##### 为什么list-item元素会出现项目符号？
######  list-item除了有一个“主块级盒子”，还有一个“附加盒子”（学名“标记盒子”），
专门用来放圆点、数字这些项目符号。IE浏览器下伪元素不支持list-item或许就是无法创建这个“标记盒子”导致的。
##### 由于display:inle-block;的出现，按照display的属性值不同，值为block的元素的盒子实际由外在的“块级盒子”和内在的“块级容器盒子”组成，
值为inline-block的元素则由外在的“内联盒子”和内在的“块级容器盒子”组成，值为inline的元素则内外均是“内联盒子”
#### 我们平时设置的width、height都是都是作用在内在的“容器盒子”上的。

#### width、height的具体细节：
##### width:auto 
1. 外部尺寸与流体特性
 *  正常流宽度
 *  格式化宽度：仅出现在“绝对定位模型”中，也就是出现在position属性值为absolute或fixed的元素中。
在默认情况下，绝对定位元素的宽度表现是“包裹性”，宽度由内部尺寸决定。
对于非替换元素，当left/right或top/bottom对立方位的属性值同时存在的时候，
元素的宽度表现为“格式化宽度”，其宽度大小相对于最近的具有定位特性（position属性值不是static）的祖先元素计算。
2. 内部尺寸与流体特性
* 包裹性
* 首选最小宽度
* 最大宽度：等同于“包裹性”元素设置white-space:norwrap声明后的宽度

#### width值作用的细节：
##### 盒尺寸：“内在盒子”又被分成4个盒子，分别是content box、padding box 、border box 、margin box
##### 宽度分离原则：就是css中的width属性不与影响宽度的padding/border（有时候包括margin）属性共存
##### 如何实现：width 独立占用一层标签，而padding、border、margin利用流动性在内部自适应呈现

#### box-sizing的作用：content-box/border-box
#### 替换元素：原生普通文本框<input>和文本域<textarea>，尺寸由内部元素决定，改变display无法使其100%自适应父元素尺寸。

### height:auto
对于width属性，就算父元素width为auto，其百分比也是支持的；但是，对于height元素，如果父元素height为auto，只要子元素在文档流中，其百分比值就完全被忽略了。（ 父级没有具体高度值的时候，height：100%会无效）
#### 如何让元素支持height:100%效果？
有两种办法：
* 设定显式的高度值：例如设置height：600px，或者可以生效的百分比值高度。比如：html,body{height:100%}
* 使用绝对定位。比如：div{height:100%;position:absolute;}此时的height:100%就会有计算值，即使祖先元素的height计算为auto也是如此。需要注意的是，绝对定位元素的百分比计算和非绝对定位的百分比计算是有区别的，区别在于绝对定位定位的宽高百分比计算是相对于padding box的，也就是说会把padding大小值计算在内，但是，非绝对定位元素则是相对于content box计算的。
1. max-width:权重很高，超越!important
2. 超越最大：指的是min-width覆盖max-width，此规则发生在min-width和max-width冲突的时候。

### 内联元素：
1. 特征，可以和文字一行显示，文字是内联元素，图片是内联元素，按钮是内联元素，输入框下拉框等原生表单控件也是内联元素
2. 内联盒模型：
* 内容区域
* 内联盒子：指元素的“外在盒子”，用来决定元素是内联还是块级。该盒子又可以细分为“内联盒子”和“匿名内联盒子”两类：
* 行框盒子
* 包含盒子
3. 幽灵空白节点：在html5文档声明中，内联元素的所有解析和渲染表现就如同每个行框盒子的前面有一个‘空白节点’一样。











