Title : CALCULATE CUBIC NUMBER USING PARALLEL PROGRAMMING

Name : MUHAMMAD ADLI BIN AHMAD NASSRUDIN

Student ID : 2022484504

Group : M3CS2554A

Lecturer's name : SIR SHAHADAN BIN SAAD

# PYTHON PARALLEL PROGRAMMING

### Introduction to Python Parallel Programming
Parallel programming is a computing paradigm where multiple tasks or processes are executed simultaneously, either concurrently or in parallel, to improve performance and efficiency. In traditional sequential programming, tasks are executed one after the other, which can lead to underutilization of available computing resources, especially in modern multi-core processors and distributed systems. Parallel programming divides the task into smaller subtask using multiple cores in a processor.
 
*The difference between serial and parallel programming:*

![parallelProgramming](https://github.com/addff/2403-ITT440/assets/166043265/c28aa50b-505e-47f2-bcd4-b0745a67cede)


## Modules
 * The `thread` module allows concurrent execution for multiple threads of the same process. Meaning that it creates new threads of the same process to be executed at the same time. However, due to the Global Interpreter Lock (GIL), threading is more suitable for I/O-bound tasks rather than CPU-bound tasks.
   
 * Python’s `multiprocessing` module overcomes the GIL limitation by creating multiple processes each with its own Python interpreter and memory space. Thus, it's best suited for CPU-bound tasks as it takes full advantage of multi-core processors.
   
## The advantages of parallel programming
1. Computers can run the code more efficiently by executing multiple processes simultaneously, which can save time by sorting through “big data” faster than ever.
2. Parallel programming can also solve more complex problems like CPU-intensive task. It utilizes the multiple cores of the CPU, bringing more resources to the table.
   
## Getting Started
**Multiprocessing coding:**
```python
import multiprocessing
import time

# cubic function 
def cubic(x):
    return x * x * x

if __name__ == '__main__':
    start_time = time.time()

    # represents a pool of worker processes that can be used to parallelize tasks.
    pool = multiprocessing.Pool()

    # creates a list of asynchronous result objects by applying the cubic function
    result_async = [pool.apply_async(cubic, args = (i, )) for i in range(10)]

    # retrieves the results of the asynchronous computations by calling the get method on each AsyncResult object
    results = [r.get() for r in result_async]

    end_time = time.time()
    execution_time = end_time - start_time

    # prints the output
    print("Output: {}".format(results) ) 
    print("Execution Time: {:.6f} seconds".format(execution_time))
```
**Output:**
![image](https://github.com/addff/2403-ITT440/assets/166043265/cfe4f0ec-3666-4d9c-8f42-2fb2638d9835)

## Video
The demonstration of the coding is as follows:

[Coding demonstration](https://drive.google.com/file/d/1fiKjPP-cF9pJYIfE62FgW0mtfnuoDwap/view?usp=sharing)

## References
Here are some of the references uses in this project:
* [A Guide to Python Multiprocessing and Parallel Programming](https://www.sitepoint.com/python-multiprocessing-parallel-programming/)
* [Parallel Processing in Python](https://www.geeksforgeeks.org/parallel-processing-in-python/)
  


