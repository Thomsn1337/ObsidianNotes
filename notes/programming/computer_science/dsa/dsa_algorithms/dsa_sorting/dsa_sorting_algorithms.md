# Sorting algorithms

Sorting algorithms are a type of [algorithm](../dsa_algorithms.md) which commonly take in some sort of [array](../../dsa_data_structures/dsa_array.md) or list as input and arrange the list items in a particular order. Typically, data is sorted in numerical order, either ascending or descending.

Sorting algorithms are often times essential for performance optimization of other algorithms. They allow to manage data in an organized manner, which allows for easier search, analysis and processing of data.

## Classification of sorting algorithms

Sorting algorithms can be classified in several different ways based on specific criteria:

- Comparison-Based and Non-Comparison-Based
- Internal and External
- Stable and Unstable

### Comparison-Based and Non-Comparison-Based

Comparison-Based algorithms determine the sorting order of elements based on comparisons. They commonly compare pairs of elements and decide their relative order. Comparison-Based sorting algorithms can't perform better than $O(N \cdot logN)$ on average.

Non-Comparison-Based algorithms don't rely on comparing elements to determine the sorting order. They use other methods such as counting or bucketing. Because of this, these algorithms are not always limited to $O(N \cdot logN)$, and they can often reach performance of $O(N)$.

### Internal and External

Sorting algorithms can be classified as internal, when the sorting operations can be performed entirely in the main memory (RAM) of the computer. This can commonly be done when the entire dataset can fit into memory. Internal sorting is generally faster than external sorting, since main memory can be accessed faster by the CPU than external storage, but they are limited by the amount of available RAM.

External sorting algorithms are used on datasets that are too large to fit into memory. Because of this, the data must reside on external storage. They involve data transfer between storage and memory. Because of this, they are generally slower than internal sorting algorithms, but are in turn not limited that much by the size of the dataset.

### Stable and Unstable

Stable sorting algorithms maintain the relative order of elements with equal keys. If two elements have the same key and one appears before the other in the original dataset, they will be in the same order after sorting.

Unstable sorting algorithms do not guarantee to preserve the initial relative order of equal keys. The original order of elements might be changed after sorting.