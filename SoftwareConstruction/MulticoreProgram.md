# Multicore Program

Resource:
Paul Butcher. Seven Concurrency Models in Seven Weeks

## Introduction

> Rob Pike: Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.

由于 CPU 多核化成为计算机性能提升的发展方向，为了更好地挖掘多核 CPU 性能，并行（Parallelism）和并发（Concurrency）就是解决之道。

并行是方法域中的概念，通过将问题中多个部分并行执行，来加速解决问题。并发是问题域中的概念，程序需要能够处理多个同时（或者几乎同时）发生的事情。

并行程序解决问题地速度往往比串行程序快得多，因为可以同时执行整个任务的多个部分。并行程序可能含有多个独立的逻辑执行块，也可能仅有一个。而并发程序则含有多个独立的逻辑执行块，它们既可独立地并行执行，也可用串行执行。

### Parallelism

计算机在不同层次上都使用了并行计算。
* Bit-Level Parallelism
* Instruction-Level Parallelism
* Data Parallelism
* Task-Level Parallelism

### Concurrency

## Threads and Mutex

## Functional Programming

## The Clojure Way—Separating Identity from State

## Actors

## Data Parallelism

## Lambda Architecture