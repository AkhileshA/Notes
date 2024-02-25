# Divide and Conquer

This is a method whose implementation is usually recursive. In this we divide a problem into smaller problems of the same type and solve the smallest unit of the problem. Later we can also combine all the instances of the problem to get the entire solution.

- **Divide** the problem into one or more subproblems that are smaller instances of the same problem.
- **Conquer** the subproblems by solving them recursively.
- **Combine** the subproblem solutions to form a solution to the original problem.

# Examples

## Merge Sort

Merge sort is a sorting algorithm which uses the Divide and Conquer algorithm to solve th sorting problem. It divides the array `A` into subarrays and each subarray `A[p:q]`. It starts with the entire array `A[1:n]` and recursing down it solves all the subarrays.

1. **Divide** the subarray `A[p:q]`to be sorted into two adjacent subarrays, each of half the size. To do so, compute the midpoint `r` of the array by averaging `p` and `q` ), and divide into subarrays `A[p:r]` and `A[r+1:q]`
3. Conquer by sorting each of the two subarrays using merge sort.
Combine by merging the two sorted subarrays , producing the sorted answer.


The base case of the algorithm is reached the the size of the array becomes one. 

The sorting happens in the combining step of this algorithm. When combining two subarrays in combime step, we combine by picking the smallest top element of the already sorted subarray