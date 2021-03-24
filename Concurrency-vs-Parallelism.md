[Concurrency vs. Parallelism / jenkov](http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html)   
[Concurrency vs. Parallelism / HowToDoInJava](https://howtodoinjava.com/java/multi-threading/concurrency-vs-parallelism/)

## Concurrency
특정 기간동안 동시에 여러 task가 실행됨. 각 task가 정확히 같은 시각에 실행되는 것이 아님. 각 task에 대한 처리를 위하여 switching이 발생

## Parallelism
특정 기간동안 여러 Task가 동시에 실행됨.


## Concurrent, not Parallel
2개 이상의 task가 동시에 실행됨. 각 task를 처리하기 위해 switch가 발생함.

## Paraller, Not Concurrent
하나의 task가 실행됨. 하나의 작업을 어러개의 sub-task로 분할하여 병렬로 실행.

## Neither Concurrent Nor Parallel
한번에 하나의 task만 실행되며, task는 sub-task로 분할되지 않음.

## Concurrent and Parallel
여러개의 task가 동시에 실행됨. 각 task는 sub-task로 분할하여 병렬로 실행.
