TASK2 R语言创意绘图


------

2018秋统计软件应用课程作业
作者：沈先亭 16307110443
2019-01-04

> 录频文件：链接：https://pan.baidu.com/s/1xlCUQPE7VqsHbnuF4Wq83g 提取码：ulmv 


### 1. 成果图展示

### 2. 函数代码

```{r}
##dream
theta = 1:60
x = sin(theta)
y = cos(theta)
op = par(bg = 'black') #把背景换成黑色
plot.new() #到新的图形框架绘图
plot.window(xlim = c(-1, 1), ylim = c(-1, 1), asp = 1) #为图形窗口设置坐标
lines(x, y, col = hsv(0.65, 1, 1))  #hsv:色调、饱和度、明度
lines(0.8 * x, 0.8 * y, col = hsv(0.8, 1, 1))
lines(0.6 * x, 0.6 * y, col = hsv(0.9, 1, 1))
lines(0.4 * x, 0.4 * y, col = hsv(0.1, 1, 1))

##cosmos
op = par(bg = "black", mar = rep(0.5, 4),asp = 1) 
x<-rnorm(10000)
y<-rnorm(10000)
plot(x,y,col=hsv(runif(1, 0.85, 0.95), 1, 1, runif(1, 0.2, 0.5)),cex=0.01)

##fireworks
theta = seq(0, 2*pi, length = 200)
x = cos(theta)
y = sin(theta)
plot(x, y, type = 'n')
segments(rep(0, 199), rep(0, 199), x[1:199] * runif(199, 0.7),
         y[1:199] * runif(199, 0.7),
         col = hsv(runif(199, 0.1, 0.2), 1, 1, runif(199, 0.5)),
         lwd = 3*runif(199)) #在点之间画线段

##love
theta = seq(-2*pi, 2 * pi, length = 200)
x = cos(theta)
y = x + sin(theta) 
op = par(bg = "black")
plot(x, y, type = "n", xlim = c(-8, 8), ylim = c(-1.5, 1.5))
for (i in seq(-2*pi, 2*pi, length = 100))
{  
lines(i*x, y, col = hsv(runif(1, 0.85, 0.95), 1, 1, runif(1, 0.2, 0.5)), lwd = 0.8)
}
```


