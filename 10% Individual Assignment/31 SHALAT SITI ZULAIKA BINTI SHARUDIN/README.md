> SHALAT SITI ZULAIKA BINTI SHARUDIN | 2022675452 | CDCS2554A | ITT400 | PREPARED FOR SIR SHAHADAN 

# Run Lab 1 on Docker Container



## What is Docker Container ? 

  - A standard software unit that encapsulates code together with all of its dependencies to enable rapid and dependable application execution 
  across various computer environments. Code, runtime, system tools, system libraries, and settings are all included in a small, independent, 
  executable software package known as a Docker container image.

  - Images become containers during Docker Engine operation. Container images become containers during runtime. Containerised software is 
  available for both Windows and Linux-based apps, and it will always function the same way regardless of the infrastructure.Containers allow software to be isolated
  from its surroundings and guarantee consistent operation even in case of variations, such as between development and staging environments.


### Docker Containers that runs on Docker engine

  1. Standard : Industry standard that are portable
  2. Lightweight : Containers that share the machine's OS system kernel and they eliminate the need for an OS for each application, increasing server efficiency and lowering server and licencing expenses.
  3. Secure : Applications are safer in containers and Docker provides the strongest default isolation capabilities in the industry.


## Comparison between Docker Containers and Virtual Machines

   | Docker Containers | Virtual Machines |
   | --- | --- |
   | No space is need to virtualize, hence less memory | Requires entire OS to be loaded before starting the surface | 
   | Prone to advesities as no provisions for isolation systems | Interference possibility is minimum because of the efficient isolation mechanism |
   | Has complex usage mechanism consisting of both third party and docker managed tools | Tools are easy to use and simpler to work with |


## Advantages and Disadvantages of Docker Containers

  | Advantages | Disadvantages |
  | --- | --- |
  | highly scalable and can be expanded easily | need to pay for the security |
  | allowed to use any programming language | no support for GUI |
  | faster deployment speed | hard learning curve |


## Lab 1 (Fork) on Docker Containers
  
  1. Install Docker
          Windows/Mac:  Download and install Docker Desktop from the official   Docker website. Follow the installation instructions and ensure Docker is running.
          Linux: Follow the official installation guide for your distribution from the Docker documentation.
  2. Set Up Your Environment
        Create a directory for your project. Inside this directory, you will have your source code and Dockerfile.
        !(10% Individual Assignment/31 SHALAT SITI ZULAIKA BINTI SHARUDIN/1st.png)

  3.  Write the C Program
Create a file named fork_example.c with the following content:
      !(10% Individual Assignment/31 SHALAT SITI ZULAIKA BINTI SHARUDIN/2ns.png)

 4. Create a Dockerfile
      !(10% Individual Assignment/31 SHALAT SITI ZULAIKA BINTI SHARUDIN/dockr.png)
 5. Build the Docker Image. Open a terminal, navigate to your project directory, and build the Docker image:
      !(10% Individual Assignment/31 SHALAT SITI ZULAIKA BINTI SHARUDIN/build docker.png)
 6. Run the Docker Container. The output will be shown.
     !(10% Individual Assignment/31 SHALAT SITI ZULAIKA BINTI SHARUDIN/output.png)

   
