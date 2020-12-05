---
title: '【LeetCode】第200周赛参加记录'
date: 2020-08-02 12:03:30
tags: LeetCode
categories: 算法
---
# 5475. 统计好三元组
## 题目描述：
>给你一个整数数组 arr ，以及 a、b 、c 三个整数。请你统计其中好三元组的数量。
如果三元组 (arr[i], arr[j], arr[k]) 满足下列全部条件，则认为它是一个 好三元组 。
0 <= i < j < k < arr.length
|arr[i] - arr[j]| <= a
|arr[j] - arr[k]| <= b
|arr[i] - arr[k]| <= c
其中 |x| 表示 x 的绝对值。
返回 好三元组的数量 
<!-- more -->
>来源：力扣
链接：https://leetcode-cn.com/problems/count-good-triplets/
## 我的题解
```
class Solution {
    public int countGoodTriplets(int[] arr, int a, int b, int c) {
        int num = 0;
        int len = arr.length;
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j < len; j++) {
                for (int k = j + 1; k < len; k++) {
                    if(Math.abs(arr[i] - arr[j]) <= a && Math.abs(arr[j] - arr[k]) <= b && Math.abs(arr[i] - arr[k]) <= c) {
                        num++;
                    }
                }
            }
        }
        return num;
    }
}
```
# 1535. 找出数组游戏的赢家
## 题目描述：
>给你一个由 不同 整数组成的整数数组 arr 和一个整数 k 。
每回合游戏都在数组的前两个元素（即 arr[0] 和 arr[1] ）之间进行。比较 arr[0] 与 arr[1] 的大小，较大的整数将会取得这一回合的胜利并保留在位置 0 ，较小的整数移至数组的末尾。当一个整数赢得 k 个连续回合时，游戏结束，该整数就是比赛的 赢家 。
返回赢得比赛的整数。
题目数据 保证 游戏存在赢家。
>来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-the-winner-of-an-array-game
## 我的题解
```
class Solution {
    public int getWinner(int[] arr, int k) {
        int count = 0;
        int num = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if(num > arr[i]) {
                count++;
            } else {
                num = arr[i];
                count = 1;
            }
            if (count == k) {
                return num;
            }
        }
        return num;
    }
}
```
# 1536. 排布二进制网格的最少交换次数
## 题目描述：
>给你一个 n x n 的二进制网格 grid，每一次操作中，你可以选择网格的 相邻两行 进行交换。
一个符合要求的网格需要满足主对角线以上的格子全部都是 0 。
请你返回使网格满足要求的最少操作次数，如果无法使网格符合要求，请你返回 -1 。
主对角线指的是从 (1, 1) 到 (n, n) 的这些格子。
>来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/minimum-swaps-to-arrange-a-binary-grid
## 我的题解
```
class Solution {
    public int minSwaps(int[][] grid) {
        int n = grid.length;
		int count = 0;
        for (int i = 0; i < n; i++) {
        	for (int j = i + 1; j < n; j++) {
        		if(grid[i][j] != 0) {
        			int index = getSwaps(grid, i);
        			if (index == -1) {
        				return -1;
        			}
        			swap(grid, i, index);
        			count += index - i;
        			break;
        		}
        	}
        }
        return count;
    }
    public int getSwaps(int[][] grid, int i) {
		int n = grid.length;
		for (int k = i + 1; k < n; k++) {
			for(int j = i + 1; j < n; j++) {
				if(grid[k][j] != 0) {
					break;
				}
				if (j == n - 1){
					return k;
				}
			}
		}
		return -1;
	}
    public void swap(int[][] grid, int i, int index) {
		int[] temp = grid[index];
		for (int j = index; j > i; j--) {
			grid[j] = grid[j - 1];
		}
		grid[i] = temp;
	}
}
```
# 总结
在规定时间内做题可以看出自己对于特定知识点的熟练程度，因为知道肯定有更优解，但是碍于时间的关系只好用自己第一时间想到的解法，所以还是要勤加练习。