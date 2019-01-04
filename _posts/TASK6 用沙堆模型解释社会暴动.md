# TASK6 用沙堆模型解释社会暴动


------

2018秋统计软件应用课程作业
作者：沈先亭 16307110443
2019-01-04

> 录频文件：

### 1. 沙堆模型

 - 提出背景：
小地震经常发生，大地震也时有存在，那么地震规模和频率满足什么样的分布呢？
 - 特点：
自组织临界理论：沙堆达到“临界”状态后，所有沙都处于一个整体的状态，新下落的沙子会在周围产生扰动，这些扰动虽微细，却能够在整个沙堆中传递，使得沙堆的结构产生变化；
沙堆的结构将随每粒新沙落下而变得愈加脆弱，最终发生沙堆的崩塌。在到达临界态后，沙崩规模的大小与其出现的频率呈幂函数关系（幂律分布）

### 2. netlogo模型编写思路
二维的元胞自动机
冯-诺伊曼邻居
5状态
边缘崩塌
 
### 3. 函数代码

    patches-own[myvalue]
    
    to setup
      clear-all
      ask patches[
        set myvalue 0
        colorit
      ]
      reset-ticks
    end
    
    to go
      ask one-of patches
      [
        set myvalue myvalue + 1  #沙粒的输入
      ]
      ask patches[
        judge-cascading  #调用坍缩过程
      ]
      ask patches[
        colorit
      ]
    end
    
    to colorit
      if (myvalue = 0)[
        set pcolor black
      ]
      if (myvalue = 1)[
        set pcolor blue
      ]
      if (myvalue = 2)[
        set pcolor green
      ]
      if (myvalue = 3)[
        set pcolor red
      ]
      if (myvalue = 4)[
        set pcolor white
      ]
    end
    
    to judge-cascading
      if(myvalue > 4)
      [
        set myvalue myvalue - 4
        ask neighbors4[
          set myvalue myvalue + 1
        ]
      ]
    end
*(以上为新手友好代码，更复杂详细的代码参照netlogo模型库中的sandpile)*
### 4. 对社会暴动的解释
沙粒逐渐增加——负能量缓慢积累
沙堆瞬间崩塌——对社会的不满在一瞬间突然释放，发生社会暴动
指导意义：让社会群体有意识地释放能量，如举办竞争性赛事，让社会群体将能量释放出来


 










