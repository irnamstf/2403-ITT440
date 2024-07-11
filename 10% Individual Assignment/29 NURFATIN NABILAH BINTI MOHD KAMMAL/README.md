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

- Pool class can be used for parallel execution of a fuction for different input data.
- The muliprocessing.Poll() class spawns a set of processes called workers and can submit tasks using the methods apply/apply_async and map/map_async.
- For parallel mapping, you should first initialize a multiprocessing.Pool() object.
- The first argument is the number of workers; if not given, that number will be equal to the number of cores in the system.
```
    import multiprocessing
    import time

    def square(x):
        return x * x

    if __name__ == '__main__':
        pool = multiprocessing.Pool()
        pool = multiprocessing.Pool(processes=4)
        inputs = [0,1,2,3,4]
        outputs = pool.map(square, inputs)
        print("Input: {}".format(inputs))
        print("Output: {}".format(outputs))
```
-----------------------------------------------------------------------------------------------------------------------------
## CONCURRENT NETWORK SERVERS ##

- Server-type applications that communicate with many clients simultaneously demand both a high performance from the I/O subsystem.
- A good web server should be able to handle hundreds of thousands of concurrent connections and service tens of thousands requests per second.
- Ideally, we would like to write these kinds of applications using threads.
- Athread is the right abstraction.
- It allows the developer to focus an programming the interaction with a single client and then to lift this interaction to multiple client by simply forking many instances of the single-client interaction in separate threads.

<img src=https://intellipaat.com/blog/wp-content/uploads/2021/09/image-99.png>
-----------------------------------------------------------------------------------------------------------------------------

## CREATE PYTHON PARALLEL PROGRAMMING IN WINDOWS 11 ##


**STEP 1:** Open **command prompt**, create file with this command **"mkdir fatin"** and entered in the file with this command **"cd fatin"**. Next, type this command **"python"** to install python in **Microsoft Store**.

![image](https://github.com/addff/2403-ITT440/assets/167417605/e61c880d-fcef-4a91-b94a-a200bb84ad7f)



**STEP 2:** In **command prompt**, create file with this command **"echo showcpu.py"** and to enter the coding you must type this command for pop up notepad **"notepad showcpu.py"**. After that, type this command **"python showcpu.py"** for show the output in command prompt.

![image](https://github.com/addff/2403-ITT440/assets/167417605/cda61784-40c0-4594-bef5-dcb9c1dfa4a8)
![image](https://github.com/addff/2403-ITT440/assets/167417605/6f186dcc-5753-4e5d-8bfd-90e0f6fae764)



**STEP 3:** In **command prompt**, create file with this command **"echo showcid.py"** and to enter the coding you must type this command for pop up notepad **"notepad showid.py"**. After that, type this command **"python showid.py"** for show the output in command prompt.

![image](https://github.com/addff/2403-ITT440/assets/167417605/0f40b40f-b7ba-4f34-98b9-f6ebfb0b20c7)
![image](https://github.com/addff/2403-ITT440/assets/167417605/70f0c36a-863e-47a9-8268-15afc6b91585)



**STEP 4:** In **command prompt**, create file with this command **"echo process.py"** and to enter the coding you must type this command for pop up notepad **"notepad process.py"**. After that, type this command **"python process.py"** for show the output in command prompt.

![image](https://github.com/addff/2403-ITT440/assets/167417605/851979c4-aebc-4310-93d0-5e7490bf9331)
![image](https://github.com/addff/2403-ITT440/assets/167417605/e52fc8f1-6e5d-4f9e-bd50-8cbd1a6222dc)


Next, In **notepad** i try to change the command. After that, type this command **"python process.py"** for show the output in command prompt.

![image](https://github.com/addff/2403-ITT440/assets/167417605/c2d94de4-c620-4456-b917-c206bd602bb8)



**STEP 5:** In **command prompt**, create file with this command **"echo pool.py"** and to enter the coding you must type this command for pop up notepad **"notepad pool.py"**. After that, type this command **"python pool.py"** for show the output in command prompt.

![image](https://github.com/addff/2403-ITT440/assets/167417605/67b35d8f-1fd3-438a-994b-334a10d3c28a)
![image](https://github.com/addff/2403-ITT440/assets/167417605/3108b0c6-07e5-498e-a389-00d1e5543a1a)



**STEP 6:** The way to pop up input & output from python pool.py according to the current time.

![image](https://github.com/addff/2403-ITT440/assets/167417605/e9e7dfbe-68da-4dc4-ad2a-f2f643127f75)



