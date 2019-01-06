# TASK5 大数律和中心极限定理的R解说


------

2018秋统计软件应用课程作业
作者：沈先亭 16307110443
2019-01-04

> 录频文件：链接：https://pan.baidu.com/s/1NbaovlF06LoEpG1E_YrsJw 提取码：76iq 


### 1. 大数律
1.1 统计知识

**大数律（Law of Large Numbers）**：样本容量越大，样本越能准确地代表总体。回答了“为何能以某事件发生的频率作为该事件发生概率的估计”的问题。
简单地说，假设x1,x2,x3,……,xn是一组独立同分布的随机变量，x_m代表样本均值，μ为该分布下的总体均值，就有：当 n → ∞ , x_m → μ


1.2 代码

```{r}
#######用自由度为3的卡方分布验证大数律
a <- rchisq(10000,3)  
largenumber_experiment <- function(n,a){
  y <- rep(0,n)
  for (i in 1:n){
    y[i] <- mean(sample(a,i,replace=TRUE))
  }
  data <- data.frame(1:n,y)
}  
object <- largenumber_experiment(n=10000,a)#抽样
colnames(object) <- c("sample_size","average_value")
##画图
library(ggplot2)
ggplot(object,aes(x=sample_size,y=average_value,color="path")) + labs(title="样本均值变化趋势") + geom_line() + geom_abline(intercept=3,slope=0,color='grey')

######用t分布验证大数律
a <- rt(n = 10000,df = 2)  
largenumber_experiment_t <- function(n,a){
  y <- rep(0,n)
  for (i in 1:n){
    y[i] <- mean(sample(a,i,replace=TRUE))
  }
  data <- data.frame(1:n,y)
}  
object <- largenumber_experiment(n=10000,a)
colnames(object) <- c("sample_size","average_value")
library(ggplot2)
ggplot(object,aes(x=sample_size,y=average_value,color="path")) + labs(title="样本均值变化趋势") + geom_line() + geom_abline(intercept=0,slope=0,color='grey')
```

### 2. 中心极限定理

2.1 统计知识
**中心极限定理（Central Limit Theorems）**：对任何均值为μ，标准差为σ的总体，样本容量为n的样本均值的分布，随着n趋近于无穷大时，会趋近均值为μ，标准差为(σ/n^.5)的正态分布。因此当n≥30时，近似有X~N（μ，(σ/n^.5)）。


2.2 代码

```{r}
a <- runif(n = 100, min = -1,max = 1 )
# a <- exp(c(runif(10000, 0, 1)))
y <- rep(0,100)
z<- rep(0,100)
for(i in 1:100){
   y[i] <- mean(sample(a,5,replace=TRUE))
}
p<- rep(0,100)
for(i in 1:100){
  p[i] <- mean(sample(a,10,replace=TRUE))
}
q <- rep(0,100)
for(i in 1:100){
  q[i] <- mean(sample(a,50,replace=TRUE))
} 
##直方图比较
clt_data <- data.frame(c(z,p,q),as.factor(c(rep(5,100),rep(10,100),rep(50,100))))
colnames(clt_data) = c("value","sizelevel")
ggplot(data=clt_data,aes(x=value)) + labs(title="样本大小 vs ") + geom_histogram(aes(color=sizelevel,fill=sizelevel)) + facet_wrap(~sizelevel)
##密度图比较
clt_data <- data.frame(c(z,p,q),as.factor(c(rep(5,100),rep(10,100),rep(50,100))))
colnames(clt_data) = c("value","sizelevel")
qplot(value,data=clt_data,geom="density",color=sizelevel) +labs(title="各样本密度曲线") + xlab("value") 
#分开画图
qplot(value,data=clt_data,geom="density",color=sizelevel,facets=sizelevel~.) +labs(title="各样本密度曲线") + xlab("value") 
```




