---
layout: post
title: TensorFlow for Beginners
date: '2017-06-15 19:40:22'
tags:
- python
- tensorflow
---

I have spent couple of hours on weekend to understand the concepts of tensorflow and would like to contribute in simplest form as most of the articles I read were too complicated and took me a while to understand.

A **tensor** consists of a set of primitive values shaped into an array of any number of dimensions. To make it more simple, consider it as an array of data.
```
ex:
[1]
[1,2]
[[1,2],[3,4]]
.....
```
**Tensorflow** is the flow of data(_tensor_) between different nodes(operation) of graph.

####Installation :
pre-requisite : Python 3.5
```
pip install tensorflow
```

####Building Blocks
**Constant** : You can store your data and cannot be altered(as the word says)
```
constant1 = tf.constant([2])
constant2 = tf.constant([2,4])
```
**[Variable](https://www.tensorflow.org/programmers_guide/variables)** : data can be altered
```
var_data = tf.Variable(5)  // var_data = 5
new_value = tf.add(var_data,var_data) // new_value = 10
update = tf.assign(var_data,new_value) // var_data =10
```
You need to initialize all variables using below function before running it using session(will discuss later).
```
tf.initialize_all_variables()
```
**Placeholder** : Same as variable but data would be assigned later in session. Consider scenario, you have a formulae by no data yet.
```
x = tf.placeholder(tf.float32)
y = x*x

with tf.Session() as session:
    result = session.run(y,{x:10})
    print(result) // 100
```

