# 如何以螺旋格式打印给定的矩阵

> 原文：<https://javascript.plainenglish.io/walk-the-matrix-ee58c1919cf5?source=collection_archive---------8----------------------->

## 给定一个 2D 数组，以螺旋形式打印出来。

![](img/83d142bdf9fc0c12b16bc2e133b4d1d8.png)

给定一个 2D 数组，以螺旋形式打印出来。请参见以下示例。

## **例子:**

```
**Input:**  1    2   3   4
        5    6   7   8
        9   10  11  12
        13  14  15  16
**Output:** 1 2 3 4 8 12 16 15 14 13 9 5 6 7 11 10 
**Explanation:** The output is matrix in spiral format. **Input:**  1   2   3   4  5   6
        7   8   9  10  11  12
        13  14  15 16  17  18
**Output:** 1 2 3 4 5 6 12 18 17 16 15 14 13 7 8 9 10 11
**Explanation :**The output is matrix in spiral format.
```

![](img/b193f7573f73a76a4ef9c21d88caa8b9.png)

## 步骤:

1.  声明矩阵和函数

```
const matrix = [ [0, 1, 2, 3], [11, 12, 13, 4], [10, 15, 14, 5], [9, 8, 7, 6],];const walkMatrix = matrix => { // your code here
}
```

2.声明结果数组

```
const result = [];
```

3.初始化上限和下限索引

```
const rowCount = matrix.length;const columnCount = matrix[0].length;let startRow = 0;let endRow = rowCount - 1;let startColumn = 0;let endColumn = columnCount - 1;
```

4.创建 while 循环

```
while (endRow >= startRow && endColumn >= startColumn) { // your code here
}
```

5.在 while 循环中，创建一个 for 循环，将第一行的值从左到右推入结果数组

```
for (let column = startColumn; column <= endColumn; column++) { result.push(matrix[startRow][column]);}
```

6.增加起始行索引

```
startRow++;
```

7.创建第二个循环，从上到下遍历最后一列

```
for (let row = startRow; row <= endRow; row++) { result.push(matrix[row][endColumn]);}
```

8.减少结束列索引

```
endColumn--;
```

9.第三个循环向后遍历最后一行，同时确保我们仍在界限内

```
if (endRow >= startRow) {//  Walk right-left on the bottom row for (let column = endColumn; column >= startColumn; column--) { result.push(matrix[endRow][column]); }}
```

10.减少结束行索引

```
endRow--;
```

11.最后一个循环从下到上遍历第一列，同时确保我们仍然在范围内

```
if (endColumn >= startColumn) {// walk bottom-top for the start column for (let row = endRow; row >= startRow; row--) { result.push(matrix[row][startColumn]); }}
```

12.增加起始列索引

```
startColumn++;
```

13.返回结果数组

```
return result;
```

您的输出应该如下所示:

```
[ 0,  1,  2,  3,  4,  5, 6,  7,  8,  9, 10, 11, 12, 13, 14, 15]
```

## 空间/时间复杂性

*   **时间复杂度:**遍历矩阵需要 O(endColumn * endRow)时间。
*   **空间复杂度:** O(1)。不需要额外的空间。

## 带注释的完整解决方案:

尽情享受吧！

[](https://polojko.medium.com/) [## 波洛日科培养基

### 最近我遇到了一个实际问题:我妻子有一个展览，需要移动 35+各种…

polojko.medium.com](https://polojko.medium.com/) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)