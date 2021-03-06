---
layout: post
title: "Combinatorics Chapter 2"
subtitle: "Reading notes and excercises of 'The combinatorics in programming'"
date: 2021-08-04
author: Rocky Shi
category: notes
tags: notes combinatorics
finished: false
---

## 笔记
无，这一章概念和例子比较多，并不难理解。
## 书面练习
1. 请构造一个7阶幻方
解： 用罗伯法，可得到以下结果
> 30      39      48      1       10      19      28  
> 38      47      7       9       18      27      29  
> 46      6       8       17      26      35      37  
> 5       14      16      25      34      36      45  
> 13      15      24      33      42      44      4   
> 21      23      32      41      43      3       12  
> 22      31      40      49      2       11      20  

2. 证明2阶幻方不存在：  
>  证：
>    1. 2阶幻方需满足1，2，3，4填入2 * 2 的方阵中，每行每列两条对角线加起来都等于（1+2+3+4）/2 = 5.
>    2. 4个数中满足加起来等于5的只有两对：1和4，2和3。所以无法满足每行每列两条对角线共6对加起来等于5的需求。
>    3. 证明完毕。  

3. 任取黑白混杂的棋子21个，排成3行7列，证明无论怎样排列，都可以找到一个小长方形子阵，使四个角上的棋子颜色相同。  
>  证：  
>  1. 首先将7个黑白棋子排成一行，根据抽屉原理，必有一种颜色的棋子数>=4，我们称该颜色棋子为这一行的优势棋子。
>  2. 同样根据抽屉原理，三行棋子中必有两行以上的优势棋子是同一种颜色。不妨设为第一、第二行，其颜色为黑。
>  3. 若两行均有黑色棋子>=4，由抽屉原理，至少有一列的第一第二行均为黑棋,不妨设为第一列。
>  4. 若其他列中有两个黑棋，则题目得证，若其他列中有两列均为白棋，则题目得证。故其他列均为一黑一白，顶多一列双白。
>  5. 一黑一白的列有5~6列，而一黑一白的情况只有两种：上黑下白和上白下黑。根据抽屉原理，至少有一种情况是>=3的，不妨设为上黑下白。
>  6. 考虑上黑下白列的第三行，由于列数>=3，而棋子只有两种颜色，所以由抽屉原理，必有一种颜色填了两次，若此颜色为黑，则与第一行的两黑形成相同颜色，否则与第二行的两白形成。
>  7. 证明完毕。  

4. 从2n个连续整数中任取n+1个，证明：这n+1个数中必有两个互质。
> 证：
> 1. 已知两个相邻的整数是互质的，因此若n+1个整数中如果有相邻的两个数，则它们互质。
> 2. 而从2n个连续整数中，最多可以选出n个不相邻的数，根据抽屉原理，选出n+1个数必定会导致选出两个相邻的整数。
> 3. 证明完毕。

5. 将1-67的正整数任意分成四部分，证明：其中必有一部分至少有一个元素是该部分中某两个数的差。
> （待完成）

6. 从1,2,...,200中任取100个数，其中之一小于16，证明：必存在2个数，使得其中一个数能被另一个数整除。
> 证：
> 1. 将200个数按以下规则分组：  
>    每个子集以奇数开头，后面的元素是前一个元素的两倍，如{1, 2, 4, 8, ..., 128}和{3, 6, 12, 24, ..., 192}等。
> 2. 如此则共有100个分组，100个分组落在100个抽屉里，若没有附加条件，则命题不成立，不能保证一个抽屉里有两个数来自同一分组。
> 3. 特别的，对于1~n个整数,其中任意取m个数(2<=m<=n),必存在2个数，一个数是另一个的倍数的条件是: m>(n>>1) + (n&1)。  
> 4. 考虑附加条件其中一个数小于16，待完成
> 
7. Ramsey理论的证明。在6个或者更多的人中，或者有3个人，他们中的每两个人都彼此不认识，或者有3个人，他们中的每两个人都互相认识。
>  证：
>  1. 用染色法证明，设每个人代表不同的点，若两个人互相认识，则将两点用蓝线连接，若互相不认识，则用红线连接。
>  2. 由此题目演变成：6个点彼此之间用红线或蓝线连接，其中必定能找到一个红色三角形或蓝色三角形。
>  3. 考虑其中一个点，设为点A，他与其余5个点BCDEF之间有5条线，可以染两种颜色，根据抽屉原理，必定有一种颜色>=3，不妨设为红线，不妨设红线连接的点是BCD。
>  4. 考虑BCD彼此之间的连线，如果有一条是红色，则该线的两端加上A点即可构成一个红色三角形。
>  5. 若BCD之间没有一条红线，则BCD构成一个蓝色三角形。
>  6. 证明完毕。

8. 一块多米诺骨牌恰好能覆盖国际象棋棋盘的两个相邻的格子。（1）证明32块骨牌能够覆盖完整的8*8棋盘。（2）割去棋盘两个对角上的各一个格子，证明用31块骨牌不能覆盖余下的棋盘。
>  证：
>  1. 用染色法证明。国际象棋棋盘原本就是黑白相间的格子，一块骨牌恰好可以覆盖1块黑格和1块白格。8*8的完整棋盘有32个黑格和32个白格，所以32块骨牌可以覆盖。
>  2. 对角上的格子是同色的格子，所以割去之后剩下32个黑格+30个白格或者30个黑格+32个白格，因此用31块骨牌是无法覆盖这些格子的。
>  3. 证明完毕。

    
## 编程练习
9. 输入一个奇数n(3<=n<=19),输出一个n阶的幻方。
>  [n阶幻方的程序实现](https://rockyshi.github.io/notes/Magic-Square-Solution.html)

10. 分数变小数问题。
    输入一个分子N和一个分母D，输出它的小数形式。如果存在循环节，用圆括号把循环节括起来。<br>
    例如： 1 / 3 = 0.(3)<br>
          22 / 5 = 4.4<br>
          45/56 = 0.803(571428)<br>
    程序如下：<br>

        string fraction(long N, long D)
        {
            unordered_map<long, long> flags;    
            std::string output;  
            output += std::to_string(N);  
            output += " / ";  
            output += std::to_string(D);  
            output += " = ";
            if((N < 0) ^ (D < 0)) { output += "-"; }  

            long numer = abs(N);
            long denom = abs(D);
            output += std::to_string(numer / denom);  

            int rest = (N % D) * 10;  
            if (rest == 0)  
            {  
                return output;    
            }
            output += ".";    
            while (rest != 0)  
            {  
                if (flags.find(rest) != flags.end())  
                {  
                    output.insert(flags[rest], 1, "(");  
                    output += ")";  
                    break;  
                }
                flags[rest] = output.size(); 
                output += std::to_string(rest / denom);  
                rest = (rest % denom) * 10;  
            }  
            return output;
        }

## 一些说明和感想
* 离开学校这么久，数学证明题果然还是有点难度，有些题目我完全是凭记忆答出来的。第7题第8题我记得很清楚，是年少时参加奥数培训，讲染色法的经典题目。<br>
* 第2题第3题比较简单，在草稿本上画了几下，用用抽屉原理就证出来了。<br>
* 第456题还要再想想，等我证出来，会再来更新。<br>
* 编程题两道都不算难。第10道是经常出现的面试题目，第9题用罗伯法也很容易实现。不过我在做第9题时自行增加了难度，想把偶数幻方也搞出来，为此花了一些时间。详细情况会记录在另一个帖子[n阶幻方的程序实现](https://rockyshi.github.io/notes/Magic-Square-Solution.html)里。<br>

## 更新日志
* 20210809 
  1. 更新第10题的程序，有些corner case之前没有考虑到。
  2. 更新第4题的证明。
  3. 更新第6题的一半证明。
           
