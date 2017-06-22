# @classmethod 与 @staticmethod
一开始看到python中的`@classmethod`和`@staticmethod`分不清楚这两个方法有什么区别，后来通过网上查资料，看到别人的解释后才对此有了一定的理解。  
比如下面是一个表示日期的类，通过年月日几个数字可以对其进行初始化。
``` python
class Date(object):
    def __init__(self, day=0, month=0, year=0):
        self.day = day
        self.month = month
        self.year = year

if __name__ == '__main__':
    # 表示2017年1月20日
    date = Date(20, 1, 2017)
```
## Class Method
但是如果有的人不希望通过这种方式进行初始化，比如输入一个字符串，那么怎么创建该类呢？这时你有两种选择：  
* 先将字符串转换为数字，再进行创建

``` python
class Date(object):
    def __init__(self, day=0, month=0, year=0):
        self.day = day
        self.month = month
        self.year = year

if __name__ == '__main__':
    # 通过数字进行创建
    date = Date(20, 1, 2017)

    # 先将字符串转换为数字，再进行创建
    string_date = '20-1-2017'
    day, month, year = map(int, string_date.split('-'))
    date1 = Date(day, month, year)
```
* 通过`@classmethod`进行创建

``` python
class Date(object):
    def __init__(self, day=0, month=0, year=0):
        self.day = day
        self.month = month
        self.year = year

    @classmethod
    def from_string(cls, date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        date1 = cls(day, month, year)
        return date1

if __name__ == '__main__':
    # 通过数字进行创建
    date = Date(20, 1, 2017)

    # 通过classmethod创建
    date2 = Date.from_string('20-1-2017')
```
这里我们可以与C++进行类比，发现它的作用与C++中的构造函数的功能非常类似。

## Staic Method
如果我们希望检查一个字符串是否是有效的日期，那么我们也有若干的方法：
``` python
def is_date_valid_1(date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        return day <= 31 and month <= 12 and year <= 3999


class Date(object):
    def __init__(self, day=0, month=0, year=0):
        self.day = day
        self.month = month
        self.year = year

    def is_date_valid_2(date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        return day <= 31 and month <= 12 and year <= 3999

    @staticmethod
    def is_date_valid_3(date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        return day <= 31 and month <= 12 and year <= 3999


if __name__ == '__main__':
    string_date = '20-1-2017'

    # 第一种方法：
    is_date_valid_1(string_date)

    # 第二种方法
    data = Date()
    data.is_date_valid_2(string_date)

    # 第三种方法
    Date.is_date_valid_3(string_date)
```
从以上的示例种可以知道，他们都能够完成检查日期是否有效的功能。那么我们来做一个简单的比较：  
* 第一种方式  
在类之外定义一个普通的函数，但该函数与这个类已经完全脱离，并没有起到一个很好的聚合作用。
* 第二种方式  
在类中定义一个成员函数，在使用时必须创建出一个类的实例出来，这样做有点画蛇添足的意思。
* 第三种方式  
定义一个静态函数，该功能能够随着类一起供他人使用，同时也无需额外创建实例对象。他与C++中的静态函数的作用一样一样的。

---
**参考资料：**
[Meaning of @classmethod and @staticmethod for beginner?](https://stackoverflow.com/questions/12179271/meaning-of-classmethod-and-staticmethod-for-beginner/12179752#12179752)
