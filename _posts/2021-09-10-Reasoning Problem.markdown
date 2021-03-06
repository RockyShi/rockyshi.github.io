---
layout: post
title: "Detective Reasoning Problem"
date: 2021-09-10
author: Rocky Shi
category: notes
tags: notes reasoning
finished: false
---

## 题目
![Problem Image](/img/10Questions.JPG)
很多人在网上都看到过这道题目。因为题目彼此之间相关，推理起来十分劳心劳力，所以最常见的办法反而是编程暴力破解。即便暴力破解，将每道题目正确的用程序表达出来也不是件容易的事情。  
既然题目上写着是推理题，身为推理爱好者，自然是要尝试一下从纯推理的角度如何解开这道题。身为程序员，自然也是要编程暴力破解然后验证推理的答案。

### 1 题目相关性分析
下面会分析每道题目和其他题目的相关性，以及题目本身蕴含的意义。  
为了方便说明以及和实际数字区分，题目用序号①②③④⑤⑥⑦⑧⑨⑩表示，用=A表示选择A，用≠A表示不能选择A，用←表示依赖，例如①←③=B，表示当③选择B的时候会影响到①，用→表示影响。   
- 题目①：  
        分析： 本身无意义  
        依赖： ④=A时=⑤,④=C时=⑨; ⑥=B时=⑥=⑧;  
        影响： ⑧; ⑨;
- 题目②：
        分析： 与⑤相关，乱序  
        依赖： ③=ABD时=③，③=C时≠C;  ④=B时=⑦; ⑥=A时=④=⑧; ←①，⑧=C时不相邻，否则相邻;  
        影响： ⑤;  
- 题目③：
        分析： 信息量最大的题之一，选择后，可以确定3道题的选项一致，另一道题不一致  
        依赖： ⑥=C时=⑩=⑧;  
        影响： ②; ④; ⑥; ⑩;  
- 题目④：  
        分析： 选择后可以确定一对题目选项一致，另外三对题选项不一致  
        依赖：③=ABC时=③，③=D时≠D;  ⑤=B时=B否则≠⑤; ⑥=A时=②=⑧;  
        影响：①; ②; ⑤; ⑥; ⑦; ⑨; ⑩;  
- 题目⑤：  
        分析： 选择后可以确定另一题与本题一致，其余3选项不一致  
        依赖：④=A时=①; ⑥=D时=⑨=⑧; ←①，⑧=B时不相邻，否则相邻;  
        影响： ④; ⑦; ⑧; ⑨;  
- 题目⑥：  
        分析：信息量最大的题之一，选择后可以确定3道题的选项一致，另外三组三道题不完全一致。  
        依赖：④=D时=⑩; ③=ACD时=③，③=B时≠B;  
        影响：①; ②; ③; ④; ⑤; ⑥; ⑨; ⑩;  
- 题目⑦：  
        分析： 本题只能选一个，说明字母分布只有一个最小值，因此满足条件的分布只有：0118，0127，0136，0145，0226，0235，0244，0334，1225，1234，1333  
        依赖：←①，⑧=A时不相邻，否则相邻; ④=B时=⑦; ⑤=D时=D否则≠⑤;  
        影响：无  
- 题目⑧：  
        分析：选择后一道题与①相邻，其余3道不相邻  
        依赖：⑤=A时=A否则≠⑤;  
        影响：②; ⑤; ⑦; ⑩;  
- 题目⑨：  
        分析：本题的条件十分复杂，依赖3道题目的结果，因此至少应该在知道2个结果之后再来讨论本题的结果。  
        依赖：⑤=C时=C否则≠⑤; ④=C时=①; ←①⑥⑤  
        影响：无  
- 题目⑩：  
        分析： 根据⑦的分析，将可能分布按照最大值和最小值的差值分类，得到： {0118,0127,0136,0145,0226,0235}>4,   
        依赖：←①，⑧=D时不相邻，否则相邻; ④=D时=⑥; 整体的答案分布;  
        影响：无

### 2 分析讨论

处理这种复杂相关的推理，唯一的办法是分步讨论，推导出矛盾则剪枝回溯。

2.1 根据⑦和⑩可知答案字母的分布只有6种，并且⑩≠D。 
    {0244,0334,1225}=4, {1234}=3, {1333}=2;

2.2 讨论③的结果：
    2.2.1 ③=B → ②③④=B,⑥≠B;  
          ②=B → ⑤=D → ⑦=D; 现在我们已经有3个B，2个D了，根据⑦=D,D必须是选的最少的选项，而在2.1的结果中无法找到2开头的分布。  
          矛盾，放弃。  
    2.2.2 ③=D → ②③⑥=D,④≠D;  
          ②=D → ⑤=B → ④=B → ⑦=②=D; 这次我们有4个D，也不可能，矛盾放弃。
    2.2.3 ③=C → ③④⑥=C,②≠C;
          ⑥=C → ③=⑩=⑧=C; ⑩=C → 分布有差为4的3种，而现在有5个C，所以只能是1225的分布。
          ④=C → ①=⑨; 接下来要讨论①和⑨的结果
    2.2.3.1 ①=⑨=A
            ①≠⑥ → ⑤=⑥=C → ⑨=C  矛盾，放弃。
    2.2.3.2 ①=⑨=D  
            ①≠⑥ → ⑤=⑥=D → ⑦=D, 现在有5个D，矛盾放弃。
    2.2.3.3 ①=⑨=C  
            则C的数量会变成7，与分布不符，放弃。
    2.2.3.4 ①=⑨=B
            ①≠⑥ → ⑤=⑩ ，则C的数量会增加，矛盾放弃。

    因为BCD都有矛盾，所以③=A → ②④⑥≠A; ②≠A → ⑤≠C; ④≠A → ①≠⑤; 

2.3 讨论⑥的结果：
    由2.2的结果⑥≠A
    2.3.1 ⑥=B → ①=⑧=B → ⑤和①不相邻 → ⑤=D → ⑦=D 矛盾放弃。
    2.3.3 ⑥=C → ③=⑩=⑧=A → 字母分布只能是1234，现在我们有3个A，1个C，接下来讨论④,由2.2知④≠A，则
    2.3.3.1 ④=B → ②=⑦ , 接下来讨论⑦
    2.3.3.1.1 ⑦=D 则D有2个，矛盾放弃。
    2.3.3.1.2 ⑦=C 但A已经有3个，矛盾放弃。
    2.3.3.1.3 ⑦=B 但算上②和④B已经有3个，矛盾放弃。
    2.3.3.1.4 ⑦=A 目前只有一个C，无矛盾。但算上②和⑦已经有了5个A，矛盾放弃。
    2.3.3.2 ④=C → ①=⑨, 讨论①和⑨，由2.2.3可知①=⑨≠A
    2.3.3.2.1 ①=⑨=B → ⑤=⑩=A → ②=C, 则A有4个③⑤⑧⑩，C有3个②④⑥，B有2个①⑨，⑦只能是D，且只有1个。目前无矛盾。
              
2.4 **验证2.3.3.2.1的结果的确为正确结果**
    ①=B,②=C,③=A,④=C,⑤=A,⑥=C,⑦=D,⑧=A,⑨=B,⑩=A

### 3 编程实现
- 为了代码的美观以及一贯以来的习惯，决定用递归而非循环来枚举每道题的答案。
- 利用第一节对每道题的分析进行节点生成和剪枝。
- 不按照题目的自然顺序而是信息量的大小来枚举以加快收敛速度。
- 每一节点生成尽可能多的答案。

  符合以上几条的程序花了我一个下午的时间，最终生成了1177个节点，其中114个节点被剪枝，766个叶节点被检查，耗时0.002秒。
  比较让人郁闷的是，随后我花了几分钟写了一个暴力计算的10层嵌套循环，复用了之前方案里的最终检查函数，结果是该函数被调用401989次，耗时0.037秒。
  也就是说，我花了一下午的时间，把这个程序优化到了暴力枚举法效率的18.5倍，然而程序复杂了太多，很难维护。
  其中带来最大麻烦的是最后一条，模仿人类思维的方式，选择了某个题目的答案之后，如果能够推理出其他题目的答案，也会将其设上。这一做法极大地减少了节点的数量，但因此带来的复杂度也是相当的麻烦。
  从竞赛的角度来说，这一优化无可厚非。但从工程角度来说，这就是个过度优化的极佳范本。

  程序太长，就不附上全部代码了。下面是检测某一道题是否符合要求的函数，两种实现都用到了，算是核心代码了:)
  ```
  bool check_answer(char* answers, *int id, char answer)
  {
    switch (id)
    {
    case 1:
        break;
    case 2:
        if (answers[5])
        {
            switch (answer)
            {
            case 'a':
                return answers[5] == 'c';
            case 'b':
                return answers[5] == 'd';
            case 'c':
                return answers[5] == 'a';
            case 'd':
                return answers[5] == 'b';
            default:
                assert(0 || "error answer");
                return false;
            }
        }
        break;
    case 3:
        if (answers[2] && answers[4] && answers[6])
        {
            switch (answer)
            {
            case 'a':
                return (answers[2] == answers[4] && answers[4] == answers[6]);
            case 'b':
                return (answers[2] == 'b' && answers[4] == 'b' && answers[6] != 'b');
            case 'c':
                return (answers[2] != 'c' && answers[4] == 'c' && answers[6] == 'c');
            case 'd':
                return (answers[2] == 'd' && answers[4] != 'd' && answers[6] == 'd');
            default:
                assert(0 || "error answer");
                return false;
            }
        }
        break;
    case 4:
        switch (answer)
        {
        case 'a':
            if (answers[1] && answers[5] && answers[1] != answers[5])
            {
                return false;
            }
            break;
        case 'b':
            if (answers[2] && answers[7] && answers[2] != answers[7])
            {
                return false;
            }
            break;
        case 'c':
            if (answers[1] && answers[9] && answers[1] != answers[9])
            {
                return false;
            }
            break;
        case 'd':
            if (answers[6] && answers[10] && answers[6] != answers[10])
            {
                return false;
            }
            break;
        default:
            assert(0 || "error answer");
            return false;
        }
        break;
    case 5:
        switch (answers[2])
        {
        case '\0':
            break;
        case 'a':
            if (answer != 'c')
                return false;
            break;
        case 'b':
            if (answer != 'd')
                return false;
            break;
        case 'c':
            if (answer != 'a')
                return false;
            break;
        case 'd':
            if (answer != 'b')
                return false;
            break;
        default:
            assert(0 || "error answer");
            return false;
        }
        switch (answer)
        {
        case 'a':
            return answers[8] == 'a';
        case 'b':
            return answers[4] == 'b';
        case 'c':
            return answers[9] == 'c';
        case 'd':
            return answers[7] == 'd';
        default:
            assert(0 || "error answer");
            return false;
        }
        break;
    case 6:
        {
            bool result;
            switch (answer)
            {
            case 'a':
                result = equal_answers({ 8,2,4 });
                break;
            case 'b':
                result = equal_answers({ 6,1,8 });
                break;
            case 'c':
                result = equal_answers({ 8,3,10 });
                break;
            case 'd':
                result = equal_answers({ 8,5,9 });
                break;
            default:
                assert(0 || "error answer");
                return false;
            }
            return result;
        }
        break;
    case 7:
        if(answers_count[0] + answers_count[1] +
            answers_count[2] + answers_count[3] == 10) 
        {   
            int min = 11, count = 0;
            char a7;
            for (int i=0;i<4;i++)
            {
                if (answers_count[i] < min)
                {
                    min = answers_count[i];
                    a7 = 'a' + i;
                    count = 1;
                }
                else if (answers_count[i] == min)
                {
                    count++;
                }
            }
            if (count > 1)
                return false;
            switch (a7)
            {
            case 'a':
                return answer == 'c';
            case 'b':
                return answer == 'b';
            case 'c':
                return answer == 'a';
            case 'd':
                return answer == 'd';
            default:
                assert(0 || "error answer");
                return false;
            }
        }
        break;
    case 8:
        if (answers[1])
        {
            switch (answer)
            {
            case 'a':
                return !check_neighbour(7) && check_neighbour(5) && check_neighbour(2) && check_neighbour(10);
            case 'b':
                return check_neighbour(7) && !check_neighbour(5) && check_neighbour(2) && check_neighbour(10);
            case 'c':
                return check_neighbour(7) && check_neighbour(5) && !check_neighbour(2) && check_neighbour(10);
            case 'd':
                return check_neighbour(7) && check_neighbour(5) && check_neighbour(2) && !check_neighbour(10);
            default:
                assert(0 || "error answer");
                return false;
            }
        }
        break;
    case 9:
        if (answers[1] && answers[9] && answers[5])
        {
            switch (answer)
            {
            case 'a':
                return answers[6] && check_pairs(6);
            case 'b':
                return answers[10] && check_pairs(10);
            case 'c':
                return answers[2] && check_pairs(2);
            case 'd':
                return answers[9] && check_pairs(9);
            default:
                assert(0 || "error answer");
                return false;
            }
        }
        break;
    case 10:
        if (answers_count[0] + answers_count[1] +
            answers_count[2] + answers_count[3] == 10)
        {
            int min = 11, max = 0;
            for (auto i = 0; i < 4; i++)
            {
                if (answers_count[i] < min)
                    min = answers_count[i];
                if (answers_count[i] > max)
                    max = answers_count[i];
            }
            switch (answer)
            {
            case 'a':
                return (max - min == 3);
            case 'b':
                return(max - min == 2);
            case 'c':
                return (max - min == 4);
            case 'd':
                return(max - min == 1);
            default:
                assert(0 || "error answer");
                return false;
            }
        }
        break;
    default:
        assert(0, "Error id");
        return false;
    }
    return true;
  }
  ```
## 更新日志
- 9/10 完成纸上推理，耗时72分钟。  
       实际做题时第一部分的分析也不会写这么详细，而是遇到相关题目再回头确认。  
       如果不是码字而是在草稿纸上画思维导图，应该能更快一些。
- 9/12 完成程序，耗时5个多小时，期间大大小小的bug修了十几个。还好有随时加assert的好习惯，不然好些bug会很难发现。  
       就算到现在，应该还有bug没修掉，我应该只是幸运的在触发bug之前找到了答案。 
