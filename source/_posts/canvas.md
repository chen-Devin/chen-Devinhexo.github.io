---
title: canvas
date: 2018-01-15 18:16:53
tags: canvas
---

### echarts：百度一款用于图表的库
+ 图表：折线图、饼图、柱状图

### 认识Canvas
+ canvas是H5中新增的一款HTML标签
    - 存在低版本浏览器兼容性问题(IE9以下不支持)
+ canvas标签元素的宽高
    - 默认宽高(300*150)：水平方向上300像素，垂直方向上150像素
    - 设置宽高
        - 通过样式来设置
        - 通过属性来设置
            - 更推荐用属性来设置

<!-- more -->

### 快速入门-绘制一条直线

```

        <html>
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <title>Title</title>
		</head>
		<body>
		<canvas id="canvas" width="800" height="600" style="border:1px solid red;"></canvas>
		</body>
		<script>
		    var canvas=document.getElementById("canvas");
		
		    var ctx=canvas.getContext("2d");
		
		    ctx.moveTo(50,50);
		    ctx.lineTo(300,300);
		
		    ctx.stroke();
		</script>
		</html>

```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<canvas id="canvas" width="800" height="600" style="border:1px solid red;"></canvas>
</body>
<script>
    var canvas=document.getElementById("canvas");

    var ctx=canvas.getContext("2d");

    ctx.moveTo(50,50);
    ctx.lineTo(300,300);

    ctx.stroke();
</script>
</html>
```

### Canvas坐标轴
+ canvas标签左上角顶点是坐标原点(0,0)
+ 从原点往右是x轴正方向，从原点往左是x轴负方向
+ 从原点往下是y轴正方向，从原点往上是y轴负方向

### 设置线条颜色
+ strokeStyle：接受一个字符串的值（比如："red" or "rgb(255,0,0)" "rgba(255,0,0,0.5)"）

### beginPath()：开辟新路径

### 路径
+ 每一次调用stroke/fill方法都会对当前路径进行重绘

+ 如果代码中没有beginPath过，那么当前代码都位于同一个路径下面

+ 可以通过ctx.beginPath()实现开辟新路径，这样就会忘记之前绘制的路径，从而可以绘制不同状态的图形（如果有需要绘制多种不同状态的图形，可以beginPath多次）


### closePath()：闭合路径

### 线宽:lineWidth

### 绘制虚线：
+ setLineDash()
+ getLineDash()
+ lineDashOffset

### clearRect：清除画布中指定的矩形区域
+ 参数(x,y,w,h)：分别表示矩形的左上角顶点坐标和矩形的宽度和高度

+ 清除画布：ctx.clearRect(0,0,canvas.width,canvas.height)

### 绘制矩形：
+ strokeRect(x,y,w,h):绘制一个描边的矩形
    - rect(x,y,w,h)+stroke()

### 折线图


### 折线图面向对象
+ 1、使用构造函数+原型的方式构建对象
+ 2、将使用到的数据以及一些全局变量(比如xLength/yLength)作为参数传入
+ 3、将canvas也作为参数传入，并在构造函数内部处理ctx的值，并处理方法中的ctx的值

### ctx.fill：绘制填充的图形
+ fill方法内部会自动的closePath

### 绘制文字
+ 绘制文字
    - ctx.strokeText("文本内容",文字的x轴坐标,文字的y轴坐标)
    - ctx.fillText("文本内容",文字的x轴坐标,文字的y轴坐标)
    - ctx.font="字体大小 字体类型";

+ 文字的水平对齐方式
    - 默认值是："start"-->"left"
    - "end"-->"right"
    - "center"：居中对齐

+ 文字的垂直对齐方式
    - "alphabetic"(默认值)-->就相当于英语四线格的第三条线，不适用于中文
    - "hanging"-->坐标位于四线格的顶部
    - "top"-->坐标跟四线格顶部上面有一段距离
    - "bottom"-->跟top对应，是底部对齐的意思
    - "middle"-->居中

### 绘制圆弧
+ arc()
    - 第一个参数、第二个参数：圆心的坐标
    - 第三个参数：圆的半径
    - 第四个参数、第五个参数：绘制圆弧的起始弧度和结束弧度
    - 第六个参数：是否以逆时针的方式绘制圆弧，默认值为false(顺时针)

