---
title: "python基础知识--python普通继承方式和super继承方式对比"
layout: page
date: 2018-01-09 00:00
---

# 写在前面
本节总结了python中类的继承。类的一般继承和super(), 两者的对比。

# 一般继承

```
class Base(object):
    def __init__(self):
        self._a = 0
        self._b = 0
        print 'enter base'
        print 'leave base'

    def a(self):
        return self._a

    def b(self):
        return self._b

    def aa(self):
        c = self.a() + self.b()
        return c


class childA(Base):
    def __init__(self):
        self._c = 1
        print 'enter childA'
        Base.__init__(self)
        print 'leave childA'

    def c(self):
        return self._c

    def aa(self):
        d = self.a() + self.b() + self.c() + b
        return d


class childB(Base):
    def __init__(self):
        print 'enter childB'
        Base.__init__(self)
        print 'leave childB'


class childC(Base):
    def __init__(self):
        print 'enter childC'
        Base.__init__(self)
        print 'leave childC'


class childD(childB, childC, childA):
    def __init__(self):
        print 'enter childD'
        childB.__init__(self)
        childC.__init__(self)
        childA.__init__(self)
        print 'leave childD'


childD()

```

输出：
```
enter childD
enter childB
enter base
leave base
leave childB
enter childC
enter base
leave base
leave childC
enter childA
enter base
leave base
leave childA
leave childD
```
# super()继承

```
class Base(object):
    def __init__(self):
        self._a = 0
        self._b = 0
        print 'enter base'
        print 'leave base'

    def a(self):
        return self._a

    def b(self):
        return self._b

    def aa(self):
        c = self.a() + self.b()
        return c


class childA(Base):
    def __init__(self):
        self._c = 1
        print 'enter childA'
        super(childA, self).__init__()
        print 'leave childA'

    def c(self):
        return self._c

    def aa(self):
        d = self.a() + self.b() + self.c() + b
        return d


class childB(Base):
    def __init__(self):
        print 'enter childB'
        super(childB, self).__init__()
        print 'leave childB'


class childC(Base):
    def __init__(self):
        print 'enter childC'
        super(childC, self).__init__()
        print 'leave childC'


class childD(childB, childC, childA):
    def __init__(self):
        print 'enter childD'
        super(childD, self).__init__()
        print 'leave childD'

childD()
```

输出：
```
enter childD
enter childB
enter childC
enter childA
enter base
leave base
leave childA
leave childC
leave childB
leave childD
```


首先对比两者的代码，当我需要修改基类的名字的时候，普通的继承方式中则需要修改很多地方，无疑增加了代码量。另外，python在使用多继承的时候要多次重复的写继承方式，显得很累赘。

因此，python提供了一种方法super(). 尤其在多继承情况下，对比上面两段代码的输出，发现基类Base()调用的次数不一样。具体机制见参考文献。


# 参考文献
[1](https://www.cnblogs.com/junneyang/p/5993034.html)