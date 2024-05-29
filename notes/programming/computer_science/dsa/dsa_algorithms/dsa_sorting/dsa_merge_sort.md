# Merge sort

Merge sort is an efficient comparison-based [sorting algorithm](dsa_sorting_algorithms.md). It sorts the dataset, generally stored in an [array](../../dsa_data_structures/dsa_array.md), by [recursively](../dsa_recursion.md) splitting it into smaller sub-arrays, sorting them and merging them back together.

The sub-arrays are split up further, until they are of either length 0 or 1, since empty arrays and single values are already considered sorted. The two sorted halves are then merged back together to produce a single sorted array.

The following [pseudocode](../../../../basics/pseudocode.md) can be used as an implementation of merge sort:

```
function mergeSort(array):
	if length of array <= 1:
		return array

	left = mergeSort(first half of array)
	right = mergeSort(second half of array)

	return merge(left, right)

function merge(left, right):
	result = []

	while left not empty && right not empty:
		if left[0] <= right[0]:
			append left[0] to result
			remove left[0] from left
		else:
			append right[0] to result
			remove right[0] from right

	if left is not empty:
		append all values from left to result

	if right is not empty:
		append all values from right to result

	return result
```

Merge sort applies the **Divide and Conquer** principle. It splits up the problem into smaller sub-problems and solves them recursively. It then combines the solutions back together. Because of this, merge sort generally performs in $O(N \cdot logN)$ [complexity](../dsa_time_complexity.md).