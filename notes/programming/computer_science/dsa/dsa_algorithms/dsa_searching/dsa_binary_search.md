# Binary search

Binary search is a [search algorithm](dsa_search_algorithms.md) used to search for data in a [sorted](../dsa_sorting/dsa_sorting_algorithms.md) [array](../../dsa_data_structures/dsa_array.md). It compares the middle element of the array with the target value. If they are not equal, the half of the array in which the target can't lie will be excluded completely and the search continues in the remaining half. This procedure is repeated until either the target value is found or the remaining half being empty. In this case, the target element is not in the array.

An implementation of binary search in pseudocode can look like this:

```
function binarySearch(array, value):
	start = 0
	end = array length - 1

	while(start <= end):
		mid = (start + end) / 2

		if array[mid] is value:
			return true  // value is in array
		else if array[mid] > value:
			// value is in the first half of the array
			end = mid - 1
		else:
			// value is in the second half of the array
			start = mid + 1

	// value is not in array
	return false
```

Binary search works by splitting up the searched [array](../../dsa_data_structures/dsa_array.md) into sub-arrays of half the size. Because of this, it performs in $O(logN)$ [complexity](../dsa_time_complexity.md). Doubling the size of the dataset would, in the worst case, only require one additional search iteration.