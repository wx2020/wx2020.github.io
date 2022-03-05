---
title: 斐波那契数列的非递归实现
---
## 问题引入

有一对兔子，从出生后第3个月起每个月都生一对兔子，小兔子长到第三个月后每个月又生一对兔子，假如兔子都不死，问每个月的兔子对数为多少？

## 程序分析

兔子的规律为数列1，1，2，3，5，8，13，21 … ，属于斐波那契数列问题。该数列有一个规律: F(0) = 1 , F(1) = 1, F(n) = F(n-1) + F(n-2)(n>=2) …

由此可以用递归的方法实现，这样写出的代码比较简洁.

```
public class Prog1 {
    public static void main(String[] args) {
    int n = 50;
    for (int i = 1; i <= n; i++) {
        System.out.println("After " + i + " mouths, the number of rabbit is " + fun2(i));
        }
    }
    
    public static long fun2(int n) {
        if (n == 1 || n == 2)
            return 1;
        else {
            return fun(n-1) + fun(n-2);
        }
    }
}
```

这样的递归算法虽然只有简单的几行，但是效率却很低。为什么呢？我们可以分析其递归调用的时间复杂度：

**时间复杂度** —– O(2^N)

由于使用递归时，其执行步骤是：要得到后一个数之前必须先计算出之前的两个数，即在每个递归调用时都会触发另外两个递归调用，例如：要得到F(10)之前得先得到F(9)、F(8)，那么得到F(9)之前得先得到F(8)、F(7)……如此递归下去 。

这样的计算是以 2 的次方在增长的。

除此之外，我们也可以看到，F(8)和F(7)的值都被多次计算，如果递归的深度越深，那么F(8)和F(7)的值会被计算更多次，但是这样计算的结果都是一样的，除了其中之一外，其余的都是浪费，可想而知，这样的开销是非常恐怖的 。

所以，如果在时间复杂度和空间复杂度都有要求的话，我们可以用以下的非递归算法来实现。

## 非递归算法

**时间复杂度为\*O(N)\*，空间复杂度为\*O(1)\***

**思路**：借助两个变量 first 和 second ，每次将 first 和 second 相加后赋给 third ，再将 second 赋给 first ，third 赋给 second，如此循环。

```
public class Prog1 {
    public static void main(String[] args) {
        int n = 50;
        for (int i = 1; i <= n; i++) {
            System.out.println("After " + i + " mouths, the number of rabbit is " + fun2(i));
        }
    }
    
    public static long fun(int n) {
        long first = 0;
        long second = 1;
        long third = 1;
        for (int i = 2; i <= n; i++) {
            third = first + second;
            first = second;
            second = third;
        }
        return third;
    }
}
```

