# re 模块函数

1. 查找一个匹配项：match、search、fullmatch  
2. 查找多个匹配项：findall、finditer  
3. 分割：split  
4. 替换：sub、subn  
5. 编译正则对象：compile、template  
6. 其它：escape、purge  

## 1. match

- 描述  
`re.match` 尝试从字符串的起始位置匹配一个模式

- 语法  
`re.match(pattern, string, flags=0)`

|参数|说明|
|---|---|
|pattern|匹配的正则表达式语法|
|string|要匹配的字符串|
|flags|标志位，用于控制正则表达式的匹配方式 e.g. re.I|

返回值：匹配成功返回匹配的对象；否则返回 None

- 实例  
```py
```

## 2. search
- 描述  
`re.search` 扫描整个字符串并返回第一个成功的匹配

- 语法  
`re.search(pattern, string, flags=0)`

|参数|说明|
|---|---|
|pattern|匹配的正则表达式语法|
|string|要匹配的字符串|
|flags|标志位，用于控制正则表达式的匹配方式 e.g. re.I|

返回值：匹配成功返回匹配的对象；否则返回 None

- 实例  
```py
```