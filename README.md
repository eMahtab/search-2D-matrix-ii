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
# Implementation : Naive
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0)
            return false;
        int rows = matrix.length;
        for(int i = 0; i < rows; i++) {
            if(binarySearch(matrix[i], target))
                return true;
        }
        return false;
    }
    
    private boolean binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;
        while(left <= right) {
            int mid = (left + right) / 2;
            if(target < arr[mid])
                right = mid - 1;
            else if(target > arr[mid])
                left = mid + 1;
            else
                return true;
        }
        return false;
    }
}
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

We keep comparing the target number with `matrix[row][column]` in the while loop as long as `row < matrix.length` and `column >= 0`

After the end of while loop we return false, which will only be executed if we never found the number in the 2D grid.

## Implementation :

```java
public  boolean searchMatrix(int[][] matrix, int target) {
    if(matrix == null || matrix.length == 0)
        return false;

      int row = 0;
      int column = matrix[0].length - 1;

      while(row < matrix.length && column >= 0){
        if(matrix[row][column] > target)
          column--; 
        else if (matrix[row][column] < target)
          row++;
        else 
          return true;    
      }
      return false;
 }
```

## Time and Space Complexity

![3 by 10 Matrix](3-by-10-matrix.PNG?raw=true "3 by 10 Matrix")

**Lets search for number `1` in the above matrix which have 3 rows and 10 columns**

We will compare `1 with 100` `1 with 90` `1 with 80` `1 with 70` `1 with 60` `1 with 50` `1 with 40` `1 with 30` `1 with 20` `1 with 10`. Finally we will exit out of while loop and return false because we didn't find `1` in above matrix. In this case while loop executed `10` times, which is equal to number of columns.

**Now lets search for number `21` in the above matrix**

We will compare `21 with 100` `21 with 90` `21 with 80` `21 with 70` `21 with 60` `21 with 50` `21 with 40` `21 with 30` `21 with 20` `21 with 25` `21 with 15` `21 with 20`. Finally we will exit out of while loop and return false because we didn't find `21` in above matrix. In this case while loop executed `12` times, which is equal to (number of rows + number of columns - 1)

So the time complexity of above implementation will be O(m + n) because while loop will never execute more than (m + n) times (regardless of whether target number exists in the matrix or not) and space complexity will be O(1), where m is the number of rows in the input matrix and n is the number of columns in the input matrix.

```
Runtime Complexity = O(m + n)
Space Complexity   = O(1)
```

## References :
https://www.youtube.com/watch?v=Ohke9-qwAKU

