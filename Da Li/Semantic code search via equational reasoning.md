# Semantic code search via equational reasoning

这类论文起源于编译优化，从 program dependency graph -> ideal graph (?) -> program expression graph，慢慢衍生而来。

早在2009年，就有论文 Equality saturation: A new approach to optimization：本文应该是最早提出 PEG 的工作，看文章的 claim感觉很厉害。该数据结构用来刻画等价程序结构，具有两大优点：

1. 避免了优化排序：传统优化算法需要每次选择一种优化策略，并生成新的IR，等待进一步优化，损失了源代码信息，同时，当前优化应该选择哪一个具体策略不好决定。
2. 避免了局部贪心：传统优化如果想找全局最优解，最坏情况下需要遍历所有路径，但E-PEG可以在一个图里表示指数级别的程序，最后用全局的视角来计算最小代码，生成最优代码，可以克服上述问题。(但是否会空间爆炸？)

但PEG在具体实现时有像静态分析技术的类似考量：

1. 核心算法是针对 pure function 来设计的，如何考虑stateful的程序，如何考虑带side-effect的程序？
2. 如何处理分支和循环？
3. 如何考虑指针、别名等问题？

本质上，PEG是一种数据流分析，但我缺乏对数据流的一系列算法的基础认识，理解起来相对费劲。