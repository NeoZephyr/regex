```
\\d
```
```
a*bd_+-\da\a
```

```py
import re

re.findall('\\\\', 'a*b+c?\\d123d\\')
```
四个反斜杠，经过第一步字符串转义，它代表的含义是两个反斜杠；这两个反斜杠再经过第二步正则转义，它就可以代表单个反斜杠了

```py
import re
re.findall(r'\\', 'a*b+c?\\d123d\\')
```

消除元字符特殊含义
```py
import re

re.escape('\d')
re.findall(re.escape('\d'), '\d')

re.escape('[+]')
re.findall(re.escape('[+]'), '[+]')
```

java 中可以使用 `Pattern.quote(text)`


字符组中的转义
```py
import re

# 转义前代表 非
re.findall(r'[^ab]', '^ab')

# 转义后代表普通字符
re.findall(r'[\^ab]', '^ab')
```

```py
import re

# 中划线在中间，代表 范围
re.findall(r'[a-c]', 'abc-')

# 中划线在中间，转义后的
re.findall(r'[a\-c]', 'abc-')

# 在开头，不需要转义
re.findall(r'[-ac]', 'abc-')

# 在结尾，不需要转义
re.findall(r'[ac-]', 'abc-')
```

```py
import re

# 右括号不转义，在首位
re.findall(r'[]ab]', ']ab')

# 右括号不转义，不在首位
re.findall(r'[a]b]', ']ab')

# 转义后代表普通字符
re.findall(r'[a\]b]', ']ab')
```

一般来说如果我们要想将元字符（.+?()）表示成字面上的意思，需要对其进行转义，如果出现在字符组中括号里，可以不转义。但如果在中括号中出现 \d 或 \w 等符号时，他们还是元字符本身的含义

```py
import re

# 单个长度的元字符
re.findall(r'[.*+?()]', '[.*+?()]')

# \w，\d等在中括号中还是元字符的功能
re.findall(r'[\d]', 'd12\\')
```
