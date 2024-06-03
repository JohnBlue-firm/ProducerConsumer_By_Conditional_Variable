
Object
- It's an example of producer and consumer using (pthread) conditional variable.

Here, we create a Buffer struct for synchronization of data
- The initBuffer function initializes the buffer and its lock (synchronization variables).
- The clearBuffer function clears its locks.
- The addItem function adds an item to the buffer, waiting if the buffer is full.
- The removeItem function removes an item from the buffer, waiting if the buffer is empty.

We also create functions to represents the producer and consumer
- The producer and consumer functions represent the producer and consumer, respectively.
- In the main function, the producer and consumer threads are created to perform their work independently.

Some notes about conditional variable
- Is it a lock ? \
  No, a conditional variable in pthreads is not a lock itself. Instead, it is a synchronization primitive used in conjunction with locks to enable threads to wait for a particular condition to become true before proceeding.
- How it work ? \
A conditional variable lets threads to suspend until another thread "signals" or "broadcasts" to inform that a condition has changed. \
When a thread waits on a conditional variable, it goes to sleep, relinquishing the CPU until the condition is signaled. This avoids busy waiting and reduces CPU usage compared to spinning on a semaphore. \
```
    while (condtion not match) { // prepare from waking up and condition not match 
        pthread_cond_wait(<cond_var>, <mutex>);
    }
```
- The Linux kernel does not implement conditional variables ! \
  In C, it is only exists in pthread (or user space).
