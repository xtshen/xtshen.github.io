#TASK3 酒鬼漫步函数编制
------
2018秋统计软件应用课程作业
作者：沈先亭 16307110443
2019-01-01

> 录频文件：暂无

### 1. 问题背景
背景材料参考：[酒鬼漫步的数学—随机过程][1]

### 2. 函数编写思路
 - 目标：将酒鬼漫步的路径可视化，根据酒鬼步数确定停下的位置
 - 输入：起点；步数
 - 输出：终点；可视化行走路径

### 3. 所用包/函数

 - animation包 ：绘制动画
 - set.seed()：生成随机数种子
 - sample.int(): 得到长度为size的整数向量样本
 - ani.options()：设置动画参数
 - saveGIF()：保存gif
 - paste0(): 连接函数
 - text(): 给绘图添加文字
 

### 4. 函数代码

```{r}
library(animation)  
randomwalk <- function(x0=0,y0=0,N=100,random_seed=12){
  set.seed(random_seed) 
  rand <- sample.int(4, N, replace=TRUE)   
  x <- x_temp <- x0
  y <- y_temp <- y0
  for(i in 1:N){
    if(rand[i]==1)           
      x_temp <- x_temp+1
    else if(rand[i]==2)     
      x_temp <- x_temp-1
    else if(rand[i]==3)       
      y_temp <- y_temp+1
    else                      
      y_temp <- y_temp-1
    x <- c(x, x_temp)
    y <- c(y, y_temp)
  }
  result <- data.frame(step=0:N, x=x, y=y)  
  x <- result[1:N,]$x
  y <- result[1:N,]$y
  max_xy <- max(abs(range(c(x,y))))   
  ani.options(interval=0.3, ani.width=800, ani.height=800, autobrowse=FALSE) 
  saveGIF(
    for(i in 1:N){
      plot(x[1:i], y[1:i], type='o', asp=1, xaxs="i",yaxs="i",
           xlab='x',ylab='y',cex.lab=2.5, cex.axis=1.5,cex.main=3,
           xlim=c(-max_xy, max_xy), ylim=c(-max_xy, max_xy), 
           col='blue', pch=1, cex=2, lwd=2.5, 
           main=paste0('N = ', i-1))
      points(x0, y0, pch=19, cex=2)    
      points(x[i], y[i], pch=19, col='red', cex=2)   
      text(0, -max_xy, paste0('(', x[i], ', ', y[i], ')'), pos=3, col='red', cex=2.5) 
      abline(h=seq(-max_xy, max_xy), col="gray", lty=3)   
      abline(v=seq(-max_xy, max_xy), col="gray", lty=3)   
    }, movie.name='2d_random_walk_1.gif')
  return(c(x[N],y[N]))   
}
```
  [1]: http://blog.sciencenet.cn/blog-677221-1071588.html
  
