# ThemisPool
> 这是一个简易的使用 `Python` 语言连接 `Mysql` 数据库的 `连接池`。

> This is a simple `connection pool` that uses `Python` language to connect to `Mysql` database.
<br>

## 取名&emsp;(Named)

- Themis(忒弥斯) 取名来自于古希腊神话中秩序女神的名字, 就如同连接池的作用一样, 管理所有用户的连接, 减少不必要的损耗。

- Themis is named after the name of the goddess of order in ancient Greek mythology, just like the role of the connection pool, it manages the connections of all users and reduces unnecessary losses.

<br>

## 需要的配置文件&emsp;(Required configuration file)
```
your python project
    |
    |
    |-- util
         |
         |-- db.cnf
         |
         |-- ThemisPool.py
```
- 我们需要在与 `ThemisPool.py` 同级文件夹下有用一个后缀名为 `.cnf` 的配置文件。
- We need to have a configuration file with the suffix `.cnf` in the same folder as `ThemisPool.py`.

<br>

```cnf
# db.cnf file

[mysql]
host = localhost
user = root
password = 12345678
database = practice
initsize = 3
maxsize = 6
```
- 在db.cnf中我们需要对将要连接的 `mysql数据库` 和 `ThemisPool连接池` 做一些基本配置。
- In db.cnf we need to do some basic configuration of the `mysql database` and `ThemisPool connection pool` to be connected.

<br>

### 所有可配置属性如下&emsp;(All configurable properties are as follows)
|参数<br>(Attribute)|说明<br>(Description)|类型<br>(Type)|默认值<br>(Default)|
|:-:|---|:-:|---|
|host|连接数据库的地址<br>The address to connect to the database|String|localhost|
|user|连接数据库的用户名<br>User name to connect to the database|String|root|
|password|连接数据库的密码<br>Password to connect to the database|String|-|
|database|本次需要连接的数据库<br>The database that needs to be connected this time|String|-|
|initsize|连接池初始化连接数<br>Number of initial connections in connection pool|int|-|
|maxsize|连接池可以同时存在的最大连接数<br>The maximum number of connections that the connection pool can exist at the same time|int|-|


<br>

## 开始使用&emsp;(Start Using)
```python

from util.ThemisPool import ThemisPool

# 初始化ThemisPool连接池 (Initialize the ThemisPool connection pool)
db = ThemisPool()

# 查询拉取数据,函数会直接返回数据 (Query pull data.It returns data directly)
selectSql = "select * from user;"
data = db.fetchone(selectSql)

# 增、删、改语句, 如果有使用mysql自增长插入的值函数会返回自增长的数据 (insert,upate delete and alter. If there is a value function inserted using mysql self-growth, it will return self-growth data)
insertSql = "insert into user values(null,'user001','123456')"
id = db.update(selectSql)


```

<br>

## 自定义配置文件名或者配置区块名?&emsp;(Custom configuration file name or sections name?)
- `ThemisPool` 支持开发者自定义配置文件和配置文件中的区块名!
- `ThemisPool` supports developers to customize configuration files and sections in configuration files!

<br>

### 这里举个例子&emsp;Here is an example

- 我们的配置文件取名为: `myDB.cnf`
- Our configuration file is named: `myDB.cnf`

```cnf
# myDB.cnf file

# 配置文件内的区块名为: "volcano"
# The sections in the configuration file is: 'volcano'

[volcano]
host = localhost
user = root
password = 12345678
database = practice
initsize = 3
maxsize = 6

```
- 那么我们可以在初始化时进行声明
- Then we can declare at initialization
```python
from util.ThemisPool import ThemisPool

# 声明配置文件名和配置块名 
# Declare the configuration file name and sections
db = ThemisPool(fileName='myDB.cnf', configName='volcano')

```

<br>

### 以上就是本次的全部内容, 下版本将会解决 python 不能对 `datetime` 类型的数据进行 `json格式化 `的问题, 并将它集成进来 !
### The above is all the content of this time. The next version will solve the problem that Python cannot format the data of type `datetime` with `json format`, and integrate it!

<br>
<br>
<br>

<p align="center">感谢您的浏览</p>
<p align="center">Thank You For Browsing!</p>
