css布局有文档流布局，浮动布局和定位布局，以及后面出现的flex布局和grid布局。
##### 使用flex实现水平居中、垂直居中
代码如下：

```
<div class="flex">
  <p>content content</p>
</div>

.flex{
  display:flex;
  justify-content:center;
  align-item:center;
}
```

#### flex的其他属性
* flex-wrap:wrap  换行

#### 具体需求的应用：
1. 基于flex布局的多行多个div水平垂直居中
代码如下：
```
<div class="content" >
   <div class="chart"></div>
   <div class="chart"></div>
   <div class="chart"></div>
   <div class="chart"></div>
   <div class="chart"></div>
   <div class="chart"></div>
</div>

.content{
 display:flex;
 flex-wrap:wrap;
 align-item:center;
 justify-content:center;
}
.chart{
text-algin:center;
}
```

2. 实现基于flex布局的左右布局，右侧内容居于最右边。内容垂直居中。
```
.tip{
    width:500px;height:40px;
    display: flex;
    align-items: center;
    .warn{
        margin-right: 8px;
    }
    .close{
        display: flex;
        justify-content: flex-end;//使之右对齐
        flex-grow: 1;//充满剩余空间
    }
}

```

##### 注意事项
* flex使得float属性无效

