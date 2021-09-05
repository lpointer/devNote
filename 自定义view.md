## 自定义view
* 自定义绘制的方式是重写绘制方法，其中最常用的是 onDraw()
* 绘制的关键是 Canvas 的使用
* Canvas 的绘制类方法： drawXXX() （关键参数：Paint）
* Canvas 的辅助类方法：范围裁切和几何变换
* 可以使用不同的绘制方法来控制遮盖关系

### Canvas.drawXXX() 和 Paint 基础

> drawXXX() 系列方法和 Paint 的基础掌握了，就能够应付简单的绘制需求。它们主要包括：

* Canvas 类下的所有 draw- 打头的方法，例如 drawCircle() drawBitmap()。
* Paint 类的几个最常用的方法。具体是：
* Paint.setStyle(Style style) 设置绘制模式
* Paint.setColor(int color) 设置颜色
* Paint.setStrokeWidth(float width) 设置线条宽度
* Paint.setTextSize(float textSize) 设置文字大小
* Paint.setAntiAlias(boolean aa) 设置抗锯齿开关
