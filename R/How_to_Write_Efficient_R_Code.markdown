# How to Write Efficient R Code

Author: Shirley Li, xue.li37@tufts.edu

## Introduction

Writing efficient R code is essential when working with large datasets or computationally intensive tasks. This tutorial covers best practices to optimize speed while maintaining readability and reproducibility.

## 1. Use Vectorized Operations Instead of Loops

R is optimized for vectorized operations, which are significantly faster than explicit loops. When using loops, R processes each iteration separately, introducing interpretation overhead. Each iteration requires multiple function calls and memory accesses, which slow down execution. Vectorized operations execute calculations at the C or Fortran level, reducing overhead and leveraging optimized memory access.

**Example:** Instead of looping through elements, use vectorized addition.

```r
# Inefficient (loop)
a <- 1:1000000
b <- 1:1000000
c <- numeric(length(a))
for (i in 1:length(a)) {
  c[i] <- a[i] + b[i]
}

# Efficient (vectorized)
c <- a + b
```

By using vectorized operations, the entire computation is handled internally in a single optimized step instead of requiring R to interpret each iteration individually.

------

## 2. Avoid Growing Objects in Loops

Appending elements inside a loop creates new copies in memory, leading to inefficient memory allocation. Every time an element is added, R creates a new vector with increased size, copies all existing elements to the new vector, and then appends the new element. This repeated reallocation is time-consuming and inefficient, especially for large objects. To improve performance, pre-allocate memory before populating an object.

**Example:**

```r
# Inefficient
x <- c()
for (i in 1:10000) {
  x <- c(x, i) 
}

# Efficient (pre-allocate memory)
x <- numeric(10000)
for (i in 1:10000) {
  x[i] <- i
}
```

The efficient approach reserves the necessary memory in advance, avoiding costly repeated memory allocations and improving execution speed.

------

## 3. Use `apply()` Functions Instead of Loops

The `apply()` family (`apply`, `lapply`, `sapply`) executes operations more efficiently than explicit loops by using pre-compiled C functions. Instead of processing elements one by one in R, these functions pass the entire structure to optimized internal routines, which perform computations much faster.

**Example:**

```r
# Inefficient (loop)
m <- matrix(rnorm(1000000), ncol = 1000)
means <- numeric(ncol(m))
for (i in 1:ncol(m)) {
  means[i] <- mean(m[, i])
}

# Efficient (apply)
means <- apply(m, 2, mean)
```

By using `apply()`, we eliminate the explicit loop, allowing R to process the matrix columns more efficiently in a single function call.

------

## 4. Use Data Table for Large Data Frames

`data.table` is optimized for fast data manipulation, reference-based modifications, and efficient grouping, making it much faster than `data.frame` for large datasets. Instead of copying data during modifications, `data.table` modifies objects in place, reducing memory usage and execution time.

**Example:**

```r
library(data.table)
DT <- data.table(x = rnorm(1e7), y = rnorm(1e7))
DT[, .(mean_x = mean(x), mean_y = mean(y)), by = y > 0]
```

In this example, `data.table` efficiently groups and processes data without creating unnecessary copies, making it ideal for big data applications.

### `data.table` vs. `tidyverse`

- When to use `data.table`?
  - For extremely large datasets where performance is critical.
  - When frequent updates or in-place modifications are required.
  - When you need efficient grouping, filtering, and aggregation.
- When to use `tidyverse` (`dplyr`)?
  - When you prioritize code readability and a consistent, user-friendly syntax.
  - When working with small-to-medium-sized datasets where speed is less critical.
  - When your workflow integrates heavily with other `tidyverse` packages such as `ggplot2` and `tidyr`.

**Comparison Example:**

```r
library(dplyr)

# Using tidyverse (dplyr)
df <- data.frame(x = rnorm(1e7), y = rnorm(1e7))
df %>% group_by(y > 0) %>% summarise(mean_x = mean(x), mean_y = mean(y))

# Using data.table
DT <- data.table(x = rnorm(1e7), y = rnorm(1e7))
DT[, .(mean_x = mean(x), mean_y = mean(y)), by = y > 0]
```

While `tidyverse` offers intuitive and readable syntax, `data.table` is optimized for speed, especially when handling large datasets. The choice depends on the dataset size, readability preference, and computational efficiency needs.

------

## 5. Use `matrix` Instead of `data.frame` When Possible

Matrices store homogeneous data more efficiently than data frames, reducing memory overhead and improving performance. A data frame is essentially a list of vectors, each of which can have different types, requiring additional memory management. In contrast, matrices store data in a contiguous block of memory, allowing for faster computations.

**Example:**

```r
# Less efficient (data frame)
df <- data.frame(a = runif(1000000), b = runif(1000000))

# More efficient (matrix)
m <- matrix(runif(2000000), ncol = 2)
```

By using a matrix instead of a data frame, operations become more memory-efficient, making calculations significantly faster.

------

## 6. Use `match()` Instead of Loops for Lookups

The `match()` function is optimized for fast vectorized lookups and is significantly faster than looping through elements manually. Instead of performing comparisons in a loop, `match()` efficiently finds indices using a search algorithm, reducing computational overhead.

**Example:**

```r
# Inefficient (loop lookup)
lookup_values <- c("A", "B", "C")
data_vector <- sample(LETTERS, 1e6, replace = TRUE)
found <- numeric(length(data_vector))
for (i in 1:length(data_vector)) {
  found[i] <- which(lookup_values == data_vector[i])
}

# Efficient (using match)
found <- match(data_vector, lookup_values)
```

Using `match()`, the entire lookup operation is optimized at a lower level, reducing the need for repetitive comparisons and significantly improving performance.

------

## Conclusion

By leveraging vectorized operations, pre-allocating memory, and using optimized functions like `apply()`, `data.table`, and `match()`, you can significantly improve the efficiency of your R code. Choosing between `data.table` and `tidyverse` depends on your dataset size and performance needs. These best practices help reduce execution time while maintaining clarity and reproducibility. Happy coding!