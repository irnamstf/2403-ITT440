Universiti Teknologi MARA (UiTM) Cawangan Melaka Kampus Jasin
Semester 4 (March 2023 – August 2023)

ITT440 Network Programming
Assignment 1:/n
Topic: Calculate Cubic Number using Parallel Programming
Name: Muhammad Adli Bin Ahmad Nassrudin (2022484504)
Group: M3CS2554A
Program: CDCS255
Lecturer’s Name: Sir Shahadan Bin Saad

Introduction to Python Parallel Programming
Parallel programming is a computing paradigm where multiple tasks or processes are executed simultaneously, either concurrently or in parallel, to improve performance and efficiency. In traditional sequential programming, tasks are executed one after the other, which can lead to underutilization of available computing resources, especially in modern multi-core processors and distributed systems. Parallel programming divides tasks into smaller subtasks using multiple cores in a processor.

The Difference Between Serial and Parallel Programming
Serial Programming:

Tasks are executed one after another.
Can lead to underutilization of CPU resources.
Parallel Programming:

Tasks are executed simultaneously.
Utilizes multiple cores of the CPU, improving efficiency and performance.
Saves time by processing large datasets faster.
Solves more complex, CPU-intensive tasks.
Key Concepts in Python Parallel Programming
Multithreading
Python's threading module allows for concurrent execution of multiple threads within the same process. This means it creates new threads that can be executed at the same time. However, due to the Global Interpreter Lock (GIL), threading is more suitable for I/O-bound tasks rather than CPU-bound tasks.

Multiprocessing
Python’s multiprocessing module overcomes the GIL limitation by creating multiple processes, each with its own Python interpreter and memory space. It is best suited for CPU-bound tasks as it takes full advantage of multi-core processors.

