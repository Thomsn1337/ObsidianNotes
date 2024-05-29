# Recursion

Recursion describes the idea of a function calling itself in its body. It is commonly used to break a big problem down into smaller pieces and then feed their results back into the original function to achieve some sort of solution. This principle is also referred to as **Divide and Conquer** [algorithm](dsa_algorithms/dsa_algorithms.md).

Such a Divide and Conquer algorithm solves a complex problem by recursively breaking it down into **two or more** sub-problems of the same of similar type. At some point these sub-problems will become simple enough to be solved directly and the solutions are combined into the solution of the original problem.

## Using recursion

This example defines a simple function `pow(x, n)`, that raises `x` by the power of `n` using iteration:

```js
function pow(x, n) {
	let result = 1;

	for (let i = 0; i < n; i++) {
		result *= x;
	}

	return result;
}
```

This example defines the same function, but uses recursion instead of iteration:

```js
function pow(x, n) {
	if (n === 1) {
		return x;
	} else {
		return x * pow(x, n - 1);
	}
}
```

The recursive variant splits the function into two paths:

- If `n === 1`, the function will return an obvious result, in this case `x`. This is commonly called the **base of the recursion**. If a recursive function has no base condition defined, it will cause an infinite loop.
- Otherwise, `pow(x, n)` can be represented as `x * pow(x, n - 1)`. Mathematically, this can be written as $x^n = x \cdot x^{n - 1}$. This is called the recursive step. It will transform the problem into a smaller sub-problem. The recursive step will be executed until the recursion base condition is met.

## When to use recursion

Any problem that can be solved recursively can also be solved iteratively using some type of loop. Recursion is commonly used for tasks that can naturally be split into several smaller tasks of the same kind, but simpler. In this use case, recursion can provide several advantages over iteration, but also some disadvantages.

### Advantages

- Recursion can often times allow for more readable and concise code, especially when dealing with nested data or repetitive structures like trees.
- A big problem will be broken down into several smaller, simpler problems.
- Recursive solutions tend to be more flexible over iterative ones, because the recursion depth will adjust dynamically based on the size of the input data.

### Disadvantages

- Each recursive call will consume additional memory on the [call stack](../../cs_call_stack.md). This can cause stack overflow errors, especially in languages with limited stack sizes.
- The additional overhead on the call stack caused by recursive calls can possibly impact performance.
- If not implemented properly, recursive functions can cause an infinite loop, most likely leading to program crashes.
- More complex recursions tend to become confusing, making it harder to follow the execution logic. This can make recursive functions harder to debug in some cases.