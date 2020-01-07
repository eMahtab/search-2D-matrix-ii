# Search 2D Matrix II
## https://leetcode.com/problems/search-a-2d-matrix-ii

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.

```
Example:

Consider the following matrix:

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

Given target = 5, return true.
Given target = 20, return false.
```

## Approach :
We are given in the question that, the input matrix is sorted in ascending order both row wise and column wise.

![Search 2D Matrix sorted row and column wise](search-2D-grid.PNG?raw=true "Search 2D Matrix sorted row and column wise")

The idea is to start the search from top-right corner of the 2D matrix.
We start from first row and last column, and compare it with target number. 

So  initially `row = 0` and `column = matrix[0].length - 1` . Now there can be 3 possibilities :
1. target number is less than the matrix[row][column], it means target number will definitely not lie in that column (because we are given in the question that, `matrix[row + 1][column]` will be greater than `matrix[row][column]`, so no need to search in that entire column and we can skip that entire column. So we decrement the value of column `column--`) 

2. target number is greater than the matrix[row][column], it means target number will definitely not lie in that row (because we are given in the question that, `matrix[row][column + 1]` will be greater than `matrix[row][column]`, so no need to search in that entire row and we can skip that entire row. So we increment the value of row `row++`) 

3. It means target number is equal to `matrix[row][column]` so we return true


## Implementation :


## References :
https://www.youtube.com/watch?v=Ohke9-qwAKU

