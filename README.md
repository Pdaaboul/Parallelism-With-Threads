# Parallelism-With-Threads

# Parallel Occurrences Counter

This repository contains a C program that demonstrates the use of multi-threading for parallel computation. The program counts the occurrences of the number 3 in a large array of integers, leveraging different mechanisms for thread coordination and data sharing.

## Description

The program explores parallelism with a selected number of threads, specifying thread data working-sets statically, and exploring different ways to coordinate thread results. It aims to evaluate the effect of the number of threads on performance and explores the problem of false sharing.

The array size is defined by the variable `N`, and the number of threads is denoted by `NT`. The main goal is to investigate the performance of different approaches for coordinating counting in a parallel environment.

## Implementation Cases

The program includes four distinct cases for counting occurrences:

1. **Case 1:** A sequential version of the occurrences counting.
2. **Case 2:** A parallel version using a globally shared counter (protected by a mutex).
3. **Case 3:** A parallel version where each thread counts occurrences in a portion of the array using a local counter and then combines the results.
4. **Case 4:** A parallel version using a global array of counters, with one element per thread (each element accessed privately by each thread), and then combining the results.

## Compilation

The code utilizes the POSIX threads library (pthreads), so make sure to link the pthread library when compiling the program. For example, you can use the following command if you're using gcc:

```bash
gcc -o run Threads-Parallelism.c
```

## Execution

Run the compiled program directly from the terminal:

```bash
./run
```

## Performance Analysis

The performance of each case was measured in terms of the time taken to count the occurrences of the number 3 in the array. Here is a summary of the results:

- **Case 1 - Sequential:** Time taken: 219 milliseconds.
- **Case 2 - Parallel with Global Shared Counter:** Time taken: 768 milliseconds.
- **Case 3 - Parallel with Local Counters:** Time taken: 56 milliseconds.
- **Case 4 - Parallel with Private Counters:** Time taken: 111 milliseconds.

> **Caution/PS:** The results presented here are specific to the machine on which the tests were run, which in this case is a MacBook Air with M1 chip and 8GB RAM. Performance can vary significantly with different hardware configurations, operating systems, and the number of processor cores available. Always consider these factors when interpreting the performance metrics.

## Observations

- The sequential version (Case 1) provides a baseline for performance comparison.
- Case 2, which uses a globally shared counter with a mutex for protection, shows significant overhead due to contention and locking.
- Case 3, with local counters for each thread, drastically improves performance by reducing contention.
- Case 4, using private counters for each thread, also performs well but not as good as Case 3, possibly due to the overhead of combining results or cache effects.

## Conclusion

The program demonstrates the importance of choosing the right strategy for data sharing and synchronization in multi-threaded applications. Proper utilization of thread-local data and minimizing contention on shared resources can lead to significant performance improvements.

