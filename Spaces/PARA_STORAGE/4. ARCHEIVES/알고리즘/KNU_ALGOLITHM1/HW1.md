---
aliases:
  - HW1 - peak finding algorithm
---


1. **Pseudocode**:

1D algorithm - Binary search based version:
```Pseudo
function find_peak(arr):
    leftIndex = 1
    rightIndex = length of arr
    while 'leftIndex' is smaller than 'rightIndex':
        midIndex = leftIndex + (rightIndex - leftIndex) / 2
        if (arr의 leftIndex의 요소 < arr의 midIndex의 요소)
	        그리고 
	        (arr의 rightIndex의 요소 < arr의 midIndex의 요소):
	        return arr의 midIndex 요소
	    else:
		    if arr의 leftIndex의 요소 > arr의 rightIndex의 요소:
			    rightIndex = midIndex
			else:
				leftIndex = midIndex

arr = [a,b,c,d,e,f,g,h,i]
peak = find_peak(arr)
print(peak)
```

2D algorithm - Greedy approach:
```
function find_peak_2d(matrix):
    rows = matrix.length
    cols = matrix[0].length
    for row from 0 to rows - 1:
        col = argmax(matrix[row])
        if row == 0 or matrix[row][col] %3E= matrix[row - 1][col] and
                        (row == rows - 1 or matrix[row][col] >= matrix[row + 1][col]):
            return (row, col)
    return None
```

2D algorithm - Improved version:
```
function find_peak_2d_improved(matrix):
    rows = matrix.length
    cols = matrix[0].length
    mid_col = cols / 2
    max_val = -INF
    max_row = -1
    for row from 0 to rows - 1:
        if matrix[row][mid_col] > max_val:
            max_val = matrix[row][mid_col]
            max_row = row
    if max_col == 0 or matrix[max_row][mid_col] >= matrix[max_row][mid_col - 1] and
                       (max_col == cols - 1 or matrix[max_row][mid_col] >= matrix[max_row][mid_col + 1]):
        return (max_row, mid_col)
    if matrix[max_row][mid_col - 1] > matrix[max_row][mid_col]:
        return find_peak_2d_improved(matrix.submatrix(:, 0 to mid_col - 1)))
    else:
        return find_peak_2d_improved(matrix.submatrix(:, mid_col + 1 to end)))
```

2. **Correctness**:

1D algorithm - Binary search based version: Correct. It finds a peak in a 1D array by iteratively narrowing down the search space using binary search until a peak is found.

2D algorithm - Greedy approach: Incorrect. It does not guarantee finding the global peak; it only ensures finding a local peak in each row. Consider a case where the peak is located in the valley formed by neighboring peaks.

2D algorithm - Improved version #2: Correct. It recursively divides the matrix into submatrices and searches for the peak in the middle column, then narrows down the search space based on adjacent elements until a peak is found. This approach guarantees finding a global peak.

3. **Time complexity**:

1D algorithm - Binary search based version:
- T(n) = O(log n)
- f(n) = n
- O(n log n)

2D algorithm - Greedy approach:
- T(n) = O(n*m)
- f(n) = m
- O(n*m)

2D algorithm - Improved version #2:
- T(n) = O(n*log(m))
- f(n) = m
- O(n*log(m))>)