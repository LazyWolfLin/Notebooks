# Multicore Program

Resource:
Paul Butcher. Seven Concurrency Models in Seven Weeks

## Introduction

> Rob Pike: Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.

由于 CPU 多核化成为计算机性能提升的发展方向，为了更好地挖掘多核 CPU 性能，并行（Parallelism）和并发（Concurrency）就是解决之道。

并发是问题域中的概念，程序需要能够处理多个同时（或者几乎同时）发生的事情。并行是方法域中的概念，通过将问题中多个部分并行执行，来加速解决问题。

并发程序含有多个独立的逻辑执行块，它们既可独立地并行执行，也可用串行执行。并行程序可能含有多个独立的逻辑执行块，也可能仅有一个，但可以同时执行整个任务的多个部分。

### Concurrency

### Parallelism

计算机在不同层次上都使用了并行计算。
* Bit-Level Parallelism
* Instruction-Level Parallelism
* Data Parallelism
* Task-Level Parallelism

## Threads and Mutex

线程与锁模型是对底层硬件执行过程的形式化。

竞态条件：代码行为取决于运算的时序。

### Memory Model

https://en.cppreference.com/w/cpp/language/memory_model

### Mutual exclusion

#### Mutex
#### Condition variables
#### 信号量

### 并发问题

#### 死锁

哲学家问题

解决方法：按照一个全局固定的顺序获取多把锁。

### 非死锁

### Atomic value

### Thread pool

## Functional Programming

函数式编程没有可变状态，很容易做到线程安全，所以可以直接支持并行。 

## The Clojure Way—Separating Identity from State

## Actors

## Data Parallelism

## Lambda Architecture