### UNIVERSITI TEKNOLOGI MARA (UiTM) CAWANGAN MELAKA KAMPUS JASIN

SEMESTER 4

MARCH 2023 – AUGUST 2023

ITT440

NETWORK PROGRAMMING 

ASSIGNMENT TITLE :

Calculate Cubic Number using Parallel Programming

NAME : MUHAMMAD ADLI BIN AHMAD NASSRUDIN (2022484504)

GROUP : M3CS2554A

PROGRAM : CDCS255

LECTURER’S NAME : SIR SHAHADAN BIN SAAD

### INTRODUCTION TO PYTHON PARALLEL PROGRAMMING
Parallel programming is a computing paradigm where multiple tasks or processes are executed simultaneously, either concurrently or in parallel, to improve performance and efficiency. In traditional sequential programming, tasks are executed one after the other, which can lead to underutilization of available computing resources, especially in modern multi-core processors and distributed systems. Parallel programming divides the task into smaller subtask using multiple cores in a processor.
 
## The difference between serial and parallel programming

The advantages of parallel programming are that computers can run the code more efficiently by executing multiple processes simultaneously, which can save time by sorting through “big data” faster than ever. Additionally, parallel programming can also solve more complex problems like CPU-intensive task. It utilizes the multiple cores of the CPU, bringing more resources to the table. 
One key point of parallel programming is multithreading. Python's threading module allows concurrent execution of multiple threads within the same process. Meaning it creates new threads to be executed at the same time. However, due to the Global Interpreter Lock (GIL), threading is more suitable for I/O-bound tasks rather than CPU-bound tasks.A
Next is the multiprocessing. Python’s multiprocessing module overcomes the GIL limitation by creating multiple processes each with its own Python interpreter and memory space. It's best suited for CPU-bound tasks as it takes full advantage of multi-core processors.





