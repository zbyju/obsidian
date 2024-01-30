Consists of a number of $N$ threads running a number of $M$ jobs. The main motivation is to avoid costs of creating and destructing threads. In cases where $M$ is big and the running time of the job is relatively low, it might make sense to use a thread pool:
- Create threads once at the beginning
- Store them in a thread pool
- Thread pool manages their lifetime
- Number of threads can be adjusted dynamically during run-time
- Tasks are passed to the threads when they are ready to receive a new one

It is important to choose a good $N$:
- $N$ too big: wasting resources by having unused threads + overhead with destroying them later
- $N$ too low: poor client performance (high waiting times)


[[Non-GoF Patterns]]