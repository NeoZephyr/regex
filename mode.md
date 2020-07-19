```py
import re
re.findall(r'a+', 'aaabb')

# ['aaa']
```

```py
import re
re.findall(r'a*', 'aaabb')

# ['aaa', '', '', '']
```

```py
import re
re.findall(r'a*?', 'aaabb')

# ['', 'a', '', 'a', '', 'a', '', '', '']
```

```py
import re
regex.findall(r'xy{1,2}+yz', 'xyyz')

# []
```

## 贪婪匹配
在正则中，表示次数的量词默认是贪婪的，在贪婪模式下，会尝试尽可能最大长度去匹配

字符串 aaabb 中使用正则 a* 的匹配过程
1. 从 0 到 3，发现 b 匹配不上，输出 aaa
2. 从 3 到 3，发现 b 匹配不上，输出空字符串
3. 从 4 到 4，发现 b 匹配不上，输出空字符串
4. 从 5 到 5，匹配剩下的空字符串，输出空字符串


## 非贪婪匹配
在量词后面加上英文的问号 ?


## 独占模式
贪婪模式与非贪婪模式，都需要发生回溯才能完成相应的功能。但是在一些场景下，我们不需要回溯，匹配不上直接返回失败，这就是独占模式。它类似贪婪匹配，但匹配过程不会发生回溯，因此在一些场合下性能会更好

在量词后面加上加号。独占模式和贪婪模式很像，独占模式会尽可能多地去匹配，如果匹配失败就结束，不会进行回溯


## 回溯
```
^([A-Za-z0-9._()&'\- ]|[aAàÀảẢãÃáÁạẠăĂằẰẳẲẵẬbBcCdD])+$
```

正则中有个加号，表示前面的内容出现一到多次，进行贪婪匹配，这样会导致大量回溯，占用大量 CPU 资源，引发线上问题。只需要将贪婪模式改成独占模式就可以解决这个问题

在这个例子中，匹配不上的就不合法，不需要进行回溯，因此可以使用独占模式


## 不区分大小写
```
(?i)cat
```
```
cat
CAT
Cat
```

```
(?i)(cat) \1
```
```
cat cat
CAT cat
Cat CAT
```

```
((?i)cat) \1
```
```
cat cat
CAT cat
Cat CAT
```

```
((?i)the) cat
```
```
the cat
The cat
the CAT
THE CAT
```


## 点号通配
```
(?s).+
```
```
the cat
The cat
the CAT
THE CAT
```

```
(?is)<head>(.+)<\/head>
```
```html
<!DOCTYPE html>
<html>
<head>
    <title>正则表达式</title>
</head>
<body>

</body>
</html>
```


## 多行匹配
```
^the|cat$
```
```
the little cat
the small cat
```

```
(?m)^the|cat$
```
```
the little cat
the small cat
```

正则中还有 \A 和 \Z，\A 仅匹配整个字符串的开始，\Z 仅匹配整个字符串的结束，在多行匹配模式下，它们的匹配行为不会改变，如果只想匹配整个字符串，而不是匹配每一行，用这个更严谨一些


## 注释模式
```
(\w+)(?#word) \1(?#word repeat again)
```
