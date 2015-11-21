I used CMake to build the project. On a Linux distribution the build can be easily done by executing the following commands:

mkdir build
cd build
cmake /path/to/hpc-knapsack/
make

This will generate Unix Makefiles. Alternatively the cmake-gui can be used for easier handling of the available options.
Note that OpenMP has to be installed. CMake tries to find it. In case it is not installed cmake will not continue generating.


Input files table:

| Name                  | Capacity of knapsack | # Items (=exemplars*distinctItems) |
|-----------------------|----------------------|------------------------------------|
| firstFileExample.txt  | 15                   | 20                                 |
| secondFileExample.txt | 15                   | 6                                  |
| thirdFileExample.txt  | 645                  | 56                                 |
| fourthFileExample.txt | 4645                 | 56                                 |
| fifthFileExample.txt  | 45000                | 7500                               |
| sixthFileExample.txt  | 150000               | 25000                              |
| dpExample.txt         | 45000                | 10000                              |

**Measurement:**

The measurement for this algorithm has been performed on Laptop. At first it was used multiple times to solve the very simple problem firstFileExample.txt, which contains 20 items. Accordingly, the algorithm had to try 2^20 combinations to find the best solution.

~~~
Alogrithm;Brute Force (Sequential)
Number of Executions;5
Average Duration;0.2821
RMS Error;0.0083
1;0.2982
2;0.2812
3;0.2754
4;0.2782
5;0.2772
~~~

As one can see, the algorithm delivered the solution in suitable 0.2821 seconds. This is simply because there were only 2^20 combinations to try. A more complex problem, for example fourthFileExample.txt, would require 2^56 combinations to be tried, which corresponds to ~69 billion times 2^20 combinations. Accordingly it would take 69 billion times 0.2821 seconds or 614 years to solve the problem. This shows how unsuitable this algorithm becomes when solving complex problems. Even parallelization would not make it more suitable. Assuming we could fully parallelize the algorithm, so we would gain a factor of n where n is the number of available cores. In this case we would still need 614\*356\*24\*3600 cores to be able to solve the previous problem within one second. Because of this insight, we concentrated on implementing more promising algorithms rather than wasting time on parallelizing this one.