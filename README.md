# Number-of-Submatrices-That-Sum-to-Target
Given a matrix and a target, return the number of non-empty submatrices that sum to target.  A submatrix x1, y1, x2, y2 is the set of all cells matrix[x][y] with x1 &lt;= x &lt;= x2 and y1 &lt;= y &lt;= y2.  Two submatrices (x1, y1, x2, y2) and (x1', y1', x2', y2') are different if they have some coordinate that is different: for example, if x1 != x1'.

class Solution:
    def numSubmatrixSumTarget(self, matrix, target):
        m, n = len(matrix), len(matrix[0])

        for row in range(m):
            for col in range(1, n):
                matrix[row][col] += matrix[row][col - 1]

        count = 0

        for c1 in range(n):
            for c2 in range(c1, n):
                prefix_sum_count = {0: 1}
                sum_val = 0

                for row in range(m):
                    sum_val += matrix[row][c2] - (matrix[row][c1 - 1] if c1 > 0 else 0)
                    count += prefix_sum_count.get(sum_val - target, 0)
                    prefix_sum_count[sum_val] = prefix_sum_count.get(sum_val, 0) + 1

        return count

