ThreadPool
==========

A simple C++11 Thread Pool implementation.

Basic usage:
```c++
// create thread pool with 4 worker threads
ThreadPool pool(4);

// enqueue and store future
auto result = pool.enqueue([](int answer) { return answer; }, 42);

// get result from future
std::cout << result.get() << std::endl;

```

```
#include <iostream>
#include "ThreadPool.h"
 
void func()
{
    std::this_thread::sleep_for(std::chrono::milliseconds(100));
    std::cout<<"worker thread ID:"<<std::this_thread::get_id()<<std::endl;
}
 
int main()
{
    ThreadPool pool(4);
    while(1)
    {
       pool.enqueue(fun);
    }
}
```
可以看出，四个线程都在运行。但是如果把func()中的延时放在main()的while循环中，就只有一个线程在运行了。

线程池，最简单的就是生产者消费者模型了。池里的每条线程，都是消费者，他们消费并处理一个个的任务，而任务队列就相当于生产者了。

线程池最简单的形式是含有一个固定数量的工作线程来处理任务，典型的数量是std::thread::hardware_concurrency()
