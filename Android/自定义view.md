## 自定义view
* 自定义绘制的方式是重写绘制方法，其中最常用的是 onDraw()
* 绘制的关键是 Canvas 的使用
* Canvas 的绘制类方法： drawXXX() （关键参数：Paint）
* Canvas 的辅助类方法：范围裁切和几何变换
* 可以使用不同的绘制方法来控制遮盖关系

### x,y轴
> 在 Android 里，每个 View 都有一个自己的坐标系，彼此之间是不影响的。这个坐标系的原点是 View 左上角的那个点；水平方向是 x 轴，右正左负；竖直方向是 y 轴，下正上负（注意，是下正上负，不是上正下负，和上学时候学的坐标系方向不一样）

### Canvas.drawXXX() 和 Paint 基础

> drawXXX() 系列方法和 Paint 的基础掌握了，就能够应付简单的绘制需求。它们主要包括：

* Canvas 类下的所有 draw- 打头的方法，例如 drawCircle() drawBitmap()。
* Paint 类的几个最常用的方法。具体是：
* Paint.setStyle(Style style) 设置绘制模式
* Paint.setColor(int color) 设置颜色
* Paint.setStrokeWidth(float width) 设置线条宽度
* Paint.setTextSize(float textSize) 设置文字大小
* Paint.setAntiAlias(boolean aa) 设置抗锯齿开关

### drawXXX常用方法
* drawCircle(float centerX, float centerY, float radius, Paint paint) 画圆
* drawRect(float left, float top, float right, float bottom, Paint paint) 画矩形
* drawPoint(float x, float y, Paint paint) 画点
* drawPoints(float[] pts, int offset, int count, Paint paint) / drawPoints(float[] pts, Paint paint) 画点（批量）
* drawOval(float left, float top, float right, float bottom, Paint paint) 画椭圆
* drawLine(float startX, float startY, float stopX, float stopY, Paint paint) 画线
* drawLines(float[] pts, int offset, int count, Paint paint) / drawLines(float[] pts, Paint paint) 画线（批量）
* drawRoundRect(float left, float top, float right, float bottom, float rx, float ry, Paint paint) 画圆角矩形
* drawArc(float left, float top, float right, float bottom, float startAngle, float sweepAngle, boolean useCenter, Paint paint) 绘制弧形或扇形
* drawPath(Path path, Paint paint) 画自定义图形
