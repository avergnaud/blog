---
title: "ThreadLocal study"
date: 2019-01-01T11:01:22+02:00
draft: false
imagePreview: "images/threadlocal-study-preview.jpg"
tags: [
    "Java",
    "Spring"
]
---

I have read [this great article](https://dzone.com/articles/painless-introduction-javas-threadlocal-storage) about java ThreadLocal objects and wanted to test their behaviour.

<!--more-->

### java.lang.ThreadLocal

This blog post relates to those two Github repositories:
1. [Use of ThreadLocal with a ThreadPoolExecutor](https://github.com/avergnaud/threadlocal-executor)
2. [Use of ThreadLocal with Spring @RestController](https://github.com/avergnaud/threadlocal-restcontroller)

#### 1. ThreadLocal values for threads of a ThreadPoolExecutor:

See [this project](https://github.com/avergnaud/threadlocal-executor). 

**The first Unit Test** *GlobalCounterTest.java* executes 10 thousands commands:
```java
Runnable command = GlobalCounter::increment
```
It uses a ThreadPoolExecutor with 50 threads.

But the global counter never reaches 10 thousands.

The *GlobalCounter.java* is the cause of the race condition with the following instruction:
```java
public static void increment() {
    value = Integer.valueOf(value.intValue() + 1);
}
```
Please note that we did not use a ThreadLocal in this first example. The race condition can be fixed with the *SafeGlobalCounter.java*

**Another Unit Test** *LocalCounterTest.java* uses a thread local counter. It executes 10 thousands commands:
```java
Runnable command = LocalCounter::increment;
```
It uses a ThreadPoolExecutor with 10 threads. 

As "the value stored in a ThreadLocal instance is specific (local) to the current running thread", each thread increments its own counter value.

There is no race condition although we use the same faulty instruction to increment the counter:
```java
public static void increment() {
    counter.set(Integer.valueOf(getValue() + 1));
    //log.put(Thread.currentThread().getName(),counter.get();
}
```
The LocalCounter keeps a Map of each thread own counter value. Here is the console output of the *LocalCounterTest.java* Unit Test.

<pre>
pool-1-thread-1:2116
pool-1-thread-3:1274
pool-1-thread-2:908
pool-1-thread-5:3526
pool-1-thread-4:322
pool-1-thread-7:294
pool-1-thread-6:1001
pool-1-thread-9:15
pool-1-thread-10:118
pool-1-thread-8:426
10000
</pre>

#### 2. ThreadLocal values for threads of a Tomcat HTTP Connector pool:

See [this project](https://github.com/avergnaud/threadlocal-restcontroller).

*HelloControllerIT.java* is a SpringBoot Integration Test. We set up the embedded Tomcat thread pool size using the @TestPropertySource annotation. Then we call 1000 times a resource that increments a thread local counter. At the end of the test the total per thread is displayed:
<pre>
http-nio-auto-1-exec-5:195
http-nio-auto-1-exec-4:198
http-nio-auto-1-exec-1:220
http-nio-auto-1-exec-3:193
http-nio-auto-1-exec-2:194
1000
</pre>

*HelloControllerContextIT.java* is another test that requires the use of the ThreadLocal.remove method:
```java
public static void clean() {
    context.remove();
}
```
Indeed we need to clean the value of the ThreadLocal once the request has been processed, because the associated thread lives inside a pool and will be reused for the next request.