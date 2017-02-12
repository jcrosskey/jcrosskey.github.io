---
layout: post
title:  "Get object from path in string format in Python"
date:   2017-02-11 21:15:30 -0500
categories: Python tricks
---
Sometimes we want to pass a string as a parameter's value in Python, instead of using a function as the parameter value. For example, if I use a configuration file for a program, it is hard to specify a function in the configuration file. It is also much easier to serialize a string than a function or class object. Python's `functools.reduce` combined with `getattr()` provides a perfect solution to this problem. Now I can just get the object from its names, which could have many levels. One example is `tensorflow.nn.train.AdamOptimizer`, an operation that uses Adam optimizer for learning. 

A good solution is suggested on [stackflow][stackflow_answer], here I made some small changes so that it is compatible with Python 3.5.

{% highlight python %}
class NoDefaultProvided(object):
    pass

def getattrd(obj, name, default=NoDefaultProvided):
    """
    Same as getattr(), but allows dot notation lookup
    Discussed in:
    http://stackoverflow.com/questions/11975781
    """

    try:
        return reduce(getattr, name.split("."), obj)
    except AttributeError as e:
        if default != NoDefaultProvided:
            return default
        raise
{% endhighlight %}

[stackflow_answer]: http://stackoverflow.com/questions/11975781/why-does-getattr-not-support-consecutive-attribute-retrievals
