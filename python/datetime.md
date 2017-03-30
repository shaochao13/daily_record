## **date 对象**

`date(year, month, day)` 产生一个 date 对象

```python
d1 = dt.date(2007, 9, 25)
d2 = dt.date(2008, 9, 25)
d1.strftime('%A, %m/%d/%y') #out: Tuesday, 09/25/07
d1.strftime('%a, %m-%d-%Y') #out: Tue, 09-25-2007

# 两个日期相差
d = d2 - d1 #返回的是一个 timedelta 对象

```

查看今天的日期

```python
dt.date.today()
```


## **time 对象**

使用 `time(hour, min, sec, us)` 产生一个 time 对象

因为没有具体的日期信息，所以 time 对象不支持减法操作

```python
t1 = dt.time(15, 38)
t2 = dt.time(18)
print t1
print t1.strftime('%I:%M, %p')
print t1.strftime('%H:%M:%S, %p')

#out:   15:38:00
#       03:38, PM
#       15:38:00, PM
```

## **datetime 对象**

使用 `datetime(year, month, day, hr, min, sec, us)` 来创建一个 datetime 对象

```python
d1 = dt.datetime.now()  #获得当前时间

#给当前的时间加上 30 天，timedelta 的参数是 timedelta(day, hr, min, sec, us)
d2 = d1 + dt.timedelta(30)


#可以通过一些指定格式的字符串来创建 datetime 对象
dt.datetime.strptime('2/10/01', '%m/%d/%y')
```

### datetime 格式字符表
字符|	含义
--|--
%a|	星期英文缩写
%A|	星期英文
%w|	一星期的第几天，[0(sun),6]
%b|	月份英文缩写
%B|	月份英文
%d|	日期，[01,31]
%H|	小时，[00,23]
%I|	小时，[01,12]
%j|	一年的第几天，[001,366]
%m|	月份，[01,12]
%M|	分钟，[00,59]
%p|	AM 和 PM
%S|	秒钟，[00,61] （大概是有闰秒的存在）
%U|	一年中的第几个星期，星期日为第一天，[00,53]
%W|	一年中的第几个星期，星期一为第一天，[00,53]
%y|	没有世纪的年份
%Y|	完整的年份