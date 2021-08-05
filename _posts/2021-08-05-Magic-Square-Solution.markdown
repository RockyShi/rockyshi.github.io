---
layout: post
title: "Magic Square Solution"
subtitle: "The extension of Combinatorics Chanpter 2 Excercise 9"
date: 2021-08-05
author: Rocky Shi
category: notes
tags: notes combinatorics algorithm
finished: false
---

## 概念
   幻方的概念很简单，中国古代的河图洛书就是三阶幻方的最早例子。
   一个n阶的幻方，就是把1到n*n的整数，填入n*n的方阵中，使得每行每列以及两条对角线上的数字之和均相等。
## 搜索的实现
   我一开始用了一个DFS试验了一下，用数字和的约束条件剪枝，5阶大概10来秒能搜出来，再往上就遥遥无期了。
   所以最终还是要靠数学的办法，蛮干是行不通的。
## 奇数阶幻方的实现
   这个成熟的方法有三种：罗伯法，杨辉法和巴舍法。后两种都需要将数字斜排，唯有第一种步骤简单明了，简直就是用计算机算法描述的。
   所以用罗伯法写一个实现。后面发现其他阶幻方也会有用到这个，又改了改以适应更通用的情况。
## 4K阶幻方的实现
   TBC
## 单偶阶幻方的实现
   TBC
