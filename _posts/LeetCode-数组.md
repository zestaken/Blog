---
title: LeetCode-数组
date: 2020-09-20 10:01:51
tags:
---

# 一维数组的动态和 1480

* 题目：
---
给你一个数组 nums 。数组「动态和」的计算公式为：runningSum[i] = sum(nums[0]…nums[i]) 。

请返回 nums 的动态和。

示例 1：

输入：nums = [1,2,3,4]
输出：[1,3,6,10]
解释：动态和计算过程为 [1, 1+2, 1+2+3, 1+2+3+4] 。

## Java解法

* 法一：
  * 设置一个新数组，每一项为前面所有项之和；
  * 通过双重循环实现。
```java
public class Sums {

    public static int[] runningSums(int nums[]) {
        int[] sums = new int[nums.length];
        for(int i = 0 ; i < nums.length; i++) {
            for(int j = 0; j <= i; j++) {
                sums[i] += nums[j];
            }
        }
        return sums;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4,5};

        int[] sums = Sums.runningSums(nums);

       for(int i : sums) {
           System.out.println(i);
       }
    }
}
```
* 法二：
  * 动态求和过程中，每一项都是前一项与自身之和。
  * 第一个元素没有前一个元素，对它没有操作，所以直接从第二个元素开始遍历求和。
```java
public class Sums {

    public static int[] runningSums (int[] nums) {

        for(int i = 1; i < nums.length; i++) {
//            if(i == 0) {
//                continue;
//            }因为0是无需操作的，所以直接从1开始就好了
            nums[i] += nums[i-1] ;
        }
        return nums;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3,4};

        int[] sums = Sums.runningSums(nums);
        for (int i : sums) {
            System.out.println(i);
        }
    }
}
```

# 拥有糖果最多的孩子 1431

* 题目：
---
给你一个数组 candies 和一个整数 extraCandies ，其中 candies[i] 代表第 i 个孩子拥有的糖果数目。

对每一个孩子，检查是否存在一种方案，将额外的 extraCandies 个糖果分配给孩子们之后，此孩子有 最多 的糖果。注意，允许有多个孩子同时拥有 最多 的糖果数目。

 

示例 1：

输入：candies = [2,3,5,1,3], extraCandies = 3
输出：[true,true,true,false,true] 
解释：
孩子 1 有 2 个糖果，如果他得到所有额外的糖果（3个），那么他总共有 5 个糖果，他将成为拥有最多糖果的孩子。
孩子 2 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。
孩子 3 有 5 个糖果，他已经是拥有最多糖果的孩子。
孩子 4 有 1 个糖果，即使他得到所有额外的糖果，他也只有 4 个糖果，无法成为拥有糖果最多的孩子。
孩子 5 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。

* java解法
---
* 先找到拥有糖果数量最多的孩子，将加上补充的糖果数后的与这个最大比较
```java
public class Candy {
    public static boolean[] isMax(int kids[], int extraCandies) {
        //找出原有最多的数
        int max = 0;
        for(int i = 0; i < kids.length; i++) {
            if(max < kids[i]) {
                max = kids[i];
            }
        }
        //设置判别数组
        boolean[] isMax = new boolean[kids.length];
        for(int i = 0; i < kids.length; i++) {
            if(kids[i] + extraCandies >= max) {
                isMax[i] = true;
            } else{
                isMax[i] = false;
            }
        }
        return isMax;
    }

    public static void main(String[] args) {
        int[] kids = {2, 3, 5, 1, 3};
        int extraCandies = 3;
        boolean[] isMax = Candy.isMax(kids, extraCandies);
        for(boolean i : isMax) {
            System.out.println(i);
        }
    }
}
```

# 重新排列数组 1470

* 题目：
---
1470. 重新排列数组
给你一个数组 nums ，数组中有 2n 个元素，按 [x1,x2,...,xn,y1,y2,...,yn] 的格式排列。

请你将数组按 [x1,y1,x2,y2,...,xn,yn] 格式重新排列，返回重排后的数组。

 

示例 1：

输入：nums = [2,5,1,3,4,7], n = 3
输出：[2,3,5,4,1,7] 
解释：由于 x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 ，所以答案为 [2,3,5,4,1,7]

* Java解法：
---
* 法一：设置一个额外的数组，用来将重排后的数据记录；
```java
public class Resort1470 {
    public static int[] resort(int[] nums1){
        int n = nums1.length / 2;
        int[] nums2 = new int[nums1.length];

        for(int i = 0 ,j = 0; j < n;  i++, j++) {
            nums2[i] = nums1[j];
            nums2[++i] = nums1[n + j];
        }
    
        return nums2;
    }

    public static void main(String[] args) {
        int[] nums1 = {2,5,1,3,4,7};
        int[] nums2 = Resort1470.resort(nums1);
        for(int i : nums2) {
            System.out.println(i);
        }
    }
}
```

#  左旋转字符串 剑指offer 58-II

* 题目：
---
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

示例 1：

输入: s = "abcdefg", k = 2
输出: "cdefgab"

* Java解法：
---
* 将该字符串分为两个子串，然后再反向连接起来
```java
import java.util.Scanner;

public class ReverseLeftWords {

    public String reverseLeftWords(String s, int n) {
         String str1 = s.substring(0, n); //读入从0到n（但是不包括下标为n的）
         String str2 = s.substring(n); //从n开始到最后（包括下标为n的）
         String  s1 = str2 + str1;//反向连接，达到左旋转的效果

         return s1;
// return s.substring(n) + s.substring(o, n);

    }

    public static void main(String[] args) {
        String s = " ";
        int n;
        Scanner in = new Scanner(System.in);

        System.out.println("请输入字符：");
        s = in.nextLine();

        System.out.println("请输入从哪里开始转：");
        n = in.nextInt();

        var reverse = new ReverseLeftWords();
        s = reverse.reverseLeftWords(s, n);

        for(int i = 0; i < s.length(); i++) {
            System.out.print(s.charAt(i) + " ");
        }

    }
}
```
* 数组形式解法：
```java
public class ReverseLeftWords {
    public static char[] reverseLeftWords(char[] nums, int n) {
        char[] nums1 = new char[n];
        char[] nums2 = new char[nums.length];

        for(int i = 0; i < nums.length; i++) {
            if(i < n) {
                nums1[i] = nums[i];
            }else {
                nums2[i - n] = nums[i];
            }
        }
        for(int i = 0; i < n; i++) {
            nums2[nums.length - n + i] = nums1[i];
        }

        return nums2;
    }

    public static void main(String[] args) {
       char[] nums = {'a','b','c','d','e'};

       char[] nums2 = ReverseLeftWords.reverseLeftWords(nums, 2);

       for(char i : nums2) {
           System.out.println(i);
       }
    }
}
```

# 好数对的数目 1512

* 题目
---
给你一个整数数组 nums 。

如果一组数字 (i,j) 满足 nums[i] == nums[j] 且 i < j ，就可以认为这是一组 好数对 。

返回好数对的数目。

 

示例 1：

输入：nums = [1,2,3,1,1,3]
输出：4
解释：有 4 组好数对，分别是 (0,3), (0,4), (3,4), (2,5) ，下标从 0 开始.

* java解法
---
* 法一：双重循环遍历数组，外层为数组这个计数循环，内层取寻找与当前元素相同的元素（但是只找当前位置之后的，避免重复计算）
```java
import java.util.Scanner;

public class NumPairs1512 {

    public static int numIdenticalPairs(int[] nums) {
        int ans = 0;

        for(int i = 0; i < nums.length; i++) {
            for(int j = 1; j < nums.length; j++) { //每次统计相同的元素都是从当前位置向后遍历，这样就不会有重复的情况
                if(nums[i] == nums[i+j]) {
                    ans++;
                }
            }
        }
        return ans;
    }
    public static void main(String[] args) {
        int[] nums = {1,2,3,1,1,3};
        System.out.println(Solution.numIdenticalPairs(nums));
    }
}
```


