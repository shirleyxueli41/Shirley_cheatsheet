

# Accelerating R Code with Fast Loops and Parallel Processing

**Author:** 

Kyle Monahan 

Shirley Li, Bioinformatician, TTS Research Technology (xue.li37@tufts.edu)

### Overview

In R, processing large datasets can become time-consuming, especially when using `for` loops that execute sequentially. This tutorial explores techniques to speed up computations by leveraging parallel processing. We introduce the R libraries `parallel`, `doParallel`, `foreach`, and `parallelly`, each offering tools to efficiently distribute tasks across multiple cores.

We’ll cover:

- How to implement basic parallelization using `for` and `foreach` loops.
- Leveraging `foreach` and `doParallel` for more complex parallel workflows.
- Using `parLapply`  and `parallelly` for straightforward parallel operations.

Through examples and comparisons, this tutorial provides a practical guide to optimizing R code for faster execution, with insights on when to choose `for`, `foreach`, `parLapply`, and `parallelly` for different scenarios. 

------

### Libraries Required

In this tutorial, we’ll use the following R libraries for parallel processing:

- **`parallel`**: The base library in R for general parallel processing tasks.
- **`doParallel`**: Supports `foreach` loops and more complex parallelized workflows.
- **`foreach`**: Provides a more flexible looping option that can run in parallel.
- **`parallelly`**: Contains helper functions that simplify cluster management.

```

# Load necessary libraries
library(parallel)    # Base parallel library for R
library(doParallel)  # Enables parallelized foreach loops
library(foreach)     # Defines foreach loops for parallel processing
library(parallelly)  # Helper functions for cluster management
```

------

### Introduction to `for` Loops in R

`for` loops are commonly used in R for iterating over data but can be slow with large datasets because they run sequentially. Here’s an example:

```
# Basic for loop example
result <- 0
for (i in 1:100000) {
  result <- result + i
}
print(result)
```

This loop iterates from 1 to 100,000, summing the values sequentially. Parallel processing can improve the runtime by distributing tasks across multiple cores.

------

### Implementing `foreach` and `doParallel` for Parallel Loops

Using `foreach` with `doParallel` provides flexibility and allows customization of result combination and parallelization.

#### Example: Parallel Summation with Two Cores

In this example, we split the summation of numbers from 1 to 100,000 between two cores. Each core calculates the sum of an assigned range, and then the results are combined.

```
# Load necessary libraries
library(doParallel)
library(foreach)

# Set up parallel backend with 2 cores
registerDoParallel(cores = 2)

# Define the two ranges for summation
ranges <- list(1:50000, 50001:100000)

# Use foreach to process each range in parallel
partial_sums <- foreach(range = ranges, .combine = '+') %dopar% {
  sum(range)
}

# Print the final result after combining the two partial sums
print(partial_sums)

# Stop the parallel backend
stopImplicitCluster()
```

**Tip**: **With more cores, divide the range accordingly to increase efficiency.**

------

### Another `for` loop example

```
# Initialize a vector to store the results
results <- numeric(100000)

# Run tasks sequentially using a for loop
for (i in 1:100000) {
  results[i] <- i * 2
}

# Print or further process the results
print(results)
```

In this example, each loop is indenpendent from each other, and the results is a list of vectors instead of single value. In this case, we can use `parLapply` in `parellelly` package. 



------

### Using `parallelly` for Enhanced Cluster Management

```
library(parallelly)

# Set up a PSOCK cluster with available cores
cluster <- makeClusterPSOCK(detectCores() - 1)

# Run tasks in parallel using parLapply
results <- parLapply(cluster, 1:100000, function(x) x * 2)

# Stop the cluster to free up resources
stopCluster(cluster)
```

The `makeClusterPSOCK` function provides more control over cluster configuration, making it useful for customized parallel environments.

In this example, `parLapply` applies a function to each element of the list (1 to 100,000) in parallel.

### Running process:

If you have 10 cores available and set up a PSOCK cluster with `detectCores() - 1`, the code will create a cluster using 9 cores. Here’s how the job distribution will work:

1. **Task Distribution Across Cores**:
   - The `parLapply` function will split the task (multiplying each number in `1:100000` by 2) across the 9 cores.
   - R will automatically divide the `1:100000` range into chunks, and each core will be assigned a subset of these numbers to process.
2. **Chunking and Parallel Processing**:
   - The 100,000 tasks will be divided into 9 chunks, with each core processing approximately 11,111 numbers.
   - For example, Core 1 might handle numbers `1:11111`, Core 2 `11112:22222`, and so on.
   - The exact distribution of numbers may vary slightly depending on R's internal load-balancing, but each core will roughly process an equal amount of numbers.
3. **Results Collection**:
   - Each core computes the results for its assigned subset and returns a list of results.
   - Once all cores finish, `parLapply` will combine these lists into a single result vector (or list) containing all processed values.
4. **Core Utilization**:
   - The task distribution makes efficient use of the 9 cores, allowing each core to operate independently on its chunk, thereby reducing the overall runtime compared to sequential processing.

### 

------



### Comparison: `for` vs. `foreach` Loops in R

Choosing between `for` and `foreach` depends on the need for **parallel processing**, **speed**, and **task complexity**.

| Feature            | `for` Loop                     | `foreach` Loop                                      |
| ------------------ | ------------------------------ | --------------------------------------------------- |
| **Execution**      | Sequentially, single-core only | Parallel using `%dopar%`, multi-core capable        |
| **Performance**    | Slower for large tasks         | Faster for large, independent tasks                 |
| **Syntax**         | Straightforward                | Requires setup but allows flexible result combining |
| **Memory Usage**   | Lower memory usage             | Higher memory usage per core                        |
| **Ideal Use Case** | Small, sequential tasks        | Large, independent, repetitive tasks                |

**Conclusion**: Use a `for` loop for simple sequential tasks and `foreach` with `%dopar%` for large-scale parallel processing.

------

### `foreach` vs. `parLapply`

The choice between `foreach` and `parLapply` depends on the operation type, required flexibility, and desired output structure.

#### Key Differences

| Feature                | `parLapply`                                 | `foreach`                                       |
| ---------------------- | ------------------------------------------- | ----------------------------------------------- |
| **Package**            | `parallel`                                  | `foreach`, `doParallel`, etc.                   |
| **Setup**              | Cluster-based, explicit setup required      | Backend-based, no explicit cluster setup needed |
| **Result Combination** | Outputs list; post-processing may be needed | `.combine` option for direct result control     |
| **Flexibility**        | Best for simple, repetitive tasks           | Ideal for complex, customizable tasks           |
| **Error Handling**     | Limited                                     | More robust error-handling options              |

#### Examples

**Using `parLapply`**:

```
library(parallel)
cluster <- makeCluster(detectCores() - 1)
result <- parLapply(cluster, 1:100000, function(x) x * 2)
stopCluster(cluster)
```

**Using `foreach`**:

```
library(doParallel)
library(foreach)
registerDoParallel(cores = detectCores() - 1)
result <- foreach(i = 1:100000, .combine = c) %dopar% {
  i * 2
}
stopImplicitCluster()
```

**Conclusion**:

- Use `parLapply` for simple parallel tasks with independent iterations.
- Use `foreach` for tasks that require customized result aggregation, error handling, or flexible backend support.

------

### Final Thoughts

Parallel processing in R can significantly improve runtime for data-intensive tasks. Understanding when to use `for` loops, `foreach`, `parLapply`, or `parallelly` can help you optimize your code's performance. This tutorial provides a foundation for efficient parallelization in R.



## References

https://www.rdocumentation.org/packages/foreach/versions/1.5.2/topics/foreach

https://cran.r-project.org/web/packages/doParallel/index.html

https://gradientdescending.com/simple-parallel-processing-in-r/

https://davidzeleny.net/wiki/doku.php/recol:parallel

https://dept.stat.lsa.umich.edu/~jerrick/courses/stat701/notes/parallel.html