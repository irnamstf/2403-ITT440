# TASK: PYTHON PARALLEL PROGRAMMING #

-----------------------------------------------------------------------------------------------------------------------
## THE MAXIMUM NUMBER OF PROCESSES CAN BE RUN ##

- The maximum number of processes you can run at a time is limited by the number of processors in your computer.
- If you don't know how many processors are present in the machine, the cpu_count() function in multiprocessing will show it.
  ```
    import multiprocessing as mp
    print("Number of processors: ", mp.cpu_count())
  ```
------------------------------------------------------------------------------------------------------------------------
## SYNCHRONOUS EXECUTION VS ASYNCHRONOUS EXECUTION ##
|        SYNCHRONOUS EXECUTION          |       ASYNCHRONOUS EXECUTION           |
| ------------------------------------- | -------------------------------------- |
| - A synchronus execution is one the processes are completed in the oder in which it was started. | - Asynchronous, on the other hand, same doesn't involve locking. | 
| - This is achieved by locking the main program until the respective processes are finished. | - As a results, the order of results can get mixed up but usually gets done quicker. |
 
------------------------------------------------------------------------------------------------------------------------
## CREATE A PROCESS WHICH PRINTS THE ASSIGNED ID ##

- By subclassing multiprocessing.process, you can create a process that runs independently.
- By the extending the __init__ method you can initialize resource and by implementing Process.run() method you can write the code for the subprocess.
```
    import multiprocessing
    import time

    class Process(multiprocessing.Process):
        def ___init___(self, id):
            super(Process, self). ___init___()
            self.id = id
        def ___init___(self):
            time.sleep(1)
            print("I'm the process witch id: {}".format(self.id))
```
- To spawn the process, we need to initialize our Process object and invoke Process.start() method. Here Process.start() will create a new process and will invike the Process.run() method.
- The code after p.start() will be executed immediately before the task completion of process p.
- To wait for the task completion, you can use Process.join().
```
    import multiprocessing
    import time

    class Process(multiprocessing.Process):
        def ___init___(self, id):
            super(Process, self). ___init___()
            self.id = id
        def ___init___(self):
            time.sleep(1)
            print("I'm the process witch id: {}".format(self.id))
    if ___name___ == '__main__':
        p = Process(0)
        p.start()
        p.join()
        p = Process(1)
        p.start()
        p.join()
```
-----------------------------------------------------------------------------------------------------------------------------
## POOL CLASS ##

- 


*******************************************************************************

