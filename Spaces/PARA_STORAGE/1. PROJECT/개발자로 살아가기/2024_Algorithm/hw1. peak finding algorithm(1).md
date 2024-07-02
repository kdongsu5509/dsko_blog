---
aliases: []
---
#### 1.[30 points] Write the pseudocode of the 1D and 2D peaking finding algorithms discussed in the class
###### 1D algorithm – binary search based version
```Pseudocode
Function findPeak1D(arr):
    left = 1
    right = arr's length
    while left <= right:
        middle = (left + right) / 2
        if arr[mid] < arr[mid - 1]:
            right = mid - 1
        else if arr[mid] < arr[mid + 1]:
            left = mid + 1
        else:
            return arr[mid]
    return -1
```
###### 2D algorithm – the greedy approach
```
Function findPeak2D(matrix):
    rows = matrix.rows
    cols = matrix.cols
    for col in range(cols):
        max_row = 0
        max_val = matrix[0][col]
        for row in range(1, rows):
            if matrix[row][col] >
             max_val:
                max_row = row
                max_val = matrix[row][col]
        if is_peak(matrix, max_row, col):
            return matrix[max_row][col]
    return -1 // Peak not found
Function is_peak(matrix, row, col):
    if (row == 0 or matrix[row][col] <= matrix[row - 1][col]) and
       (row == matrix.rows - 1 or matrix[row][col] >= matrix[row + 1][col]):
        return True
    else:
        return False
```
###### 2D algorithm – improved version
```
Function findPeak2D(matrix):
    rows = matrix.rows
    cols = matrix.cols
    return findPeak2DHelper(matrix, 0, rows - 1, cols)
Function findPeak2DHelper(matrix, startRow, endRow, cols):
    midRow = (startRow + endRow) / 2
    maxCol = findMaxInColumn(matrix, midRow)
    if midRow == 0 or matrix[midRow][maxCol] >= matrix[midRow - 1][maxCol] and
                     (midRow == rows - 1 or matrix[midRow][maxCol] >= matrix[midRow + 1][maxCol]): return matrix[midRow][maxCol]
    else if matrix[midRow][maxCol] < matrix[midRow - 1][maxCol]:
        return findPeak2DHelper(matrix, startRow, midRow - 1, cols)
    else:
        return findPeak2DHelper(matrix, midRow + 1, endRow, cols)
Function findMaxInColumn(matrix, row): // n + c
    maxVal = matrix[row][0]
    maxCol = 0
    for col in range(1, cols):
        if matrix[row][col] > maxVal:
            maxVal = matrix[row][col]
            maxCol = col
    return maxCol
``` 
#### 2.[15 points] Show whether each algorithm is correct or incorrect
`1D peak fingidng algorithm` is correct. It efficiently searches for a peak element in a 1D array by using binary search, ensuring that the peak element satisfies the conditions mentioned in the slides.
`2D Peak-Finding Algorithm (Greedy Approach)` is correct for finding a peak in a 2D matrix. It iterates over each column and searches for a peak element in that column, ensuring that the peak satisfies the conditions mentioned in the slides.
`2D Peak-Finding Algorithm (Improved Version #2)` is not correct.
• Proof (by contradiction): Assume that no peak on the left then b must have a neighbor b1 with
higher value and b1 must have a neighbor b2 with higher value.
– We have to stay on the left side because we cannot enter the middle column
– But at some point, we would run out the elements of the left columns. Hence, we have to find a peak at some
#### 3.[30 points] Compute T(n), f(n) and O of each algorithm
###### 1D Peak-Finding Algorithm (Binary Search Based)
![[temp_1d_peak_finding.png|300]]
- **T(n) :** T(n/2^k) is time complexity of binary searching  algorithm. At this algorithm we use the concept of binary searching. So we have to add T(n/2^k). Also we compare three elements of array, at every case. that count's is fixed. So we also have to add specific constant. So the T(n) = T(n/2^k) + ck.
- **f(n) :** f(n) = O(g(n)) if and only if there exist positive constants c and n0 such that 0 <= f(n) <= c*g(n) for all n >= n0.* At this algorithm, T(n)=T(2kn​)+ck=T(2k2km​)+ck=T(2(m−1)k)+ck = T(2(m−2)k)+c(2(m−1)k)+ck=T(2(m−3)k)+c(2(m−2)k)+c(2(m−1)k)+ck=…=T(1)+c(2(m−1)k)+c(2(m−2)k)+⋯+c(20k)=T(1)+c(20k+21k+22k+⋯+2(m−1)k)=T(1)+ck(1−2k1−(2k)m​)=T(1)+ck(1−2k1−n​)​..-> So f(n) = n.
- **O (n) :** n.
###### 2D Peak-Finding Algorithm (Greedy Approach)
- **T(n):** \( O(m \times n) \) - At this Algorithm, the number of calcultion is depend on the number of columms and rows. Without considering `loop`, we have to show the number of calcultion to compare each elements. That is fixed number of each cases, and is independent from the number of rows and columms. So T(n) = (cols * rows) + 2c. 
- **f(n):** \( O(1) \) - let c and c2 is contant that can be negligible. Then T(n) = (cols * rows) + 2c <= c2 * n^2. So f(n) is n^2.
- **O(n):** normalerweise, the concept of O(n) is (O(f(n))). So O(n) is eqaul to O(n^2).
### 2D Peak-Finding Algorithm (Improved Version #2)
*let matrix is square arrangement.*
*I didn't distinguish between uppercase and lowercase letters to this explanation.* 
- **T(n):** At first, if we use this algorithm, a computer will choose a center column of the matrix. and then, it find a peak of that column so the number of the calculation is N. (the N is constanct, so we can see the time complexity of that is just Constant C.) After find some peak of that cols, then we find next step by recursion. So the T(n) is T(n/2) + O(1). the total T(n) is O(1), that is some constant's sum. So total T(n) = O(1) + ... O(1). the number of O(1) is log2N. So T(n) = log2N * O(1) * N.
- **f(n) :** T(n) is log2N * O(n) * N. that must be smaller than c * log2N * N.  (c is another constant.) 
- **O(n) :** O(n) == O(f(n)) . When apply O(n) notation to f(n), the constant is ignored. So O(n) = O(N*logN).