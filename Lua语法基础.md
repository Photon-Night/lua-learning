# Lua语法基础



## 注释

+ 单行注释

  ```lua
  --单行注释
  ```



+ 多行注释

  ```lua
  --[[
  多行
  注释
  ]]
  
  --[[
  第二种
  多行
  注释
  ]]--
  
  --[[
  第三种
  多行
  注释
  --]]
  ```
  
  

## 变量

### 四种简单类型变量

1.number

2.string

3.boolean

4.nil



### 四种复杂类型变量

1.function(函数)

2.table（表）

3.userdata（数据结构）

4.thread（协同程序）



```lua
 --[[lua的变量申明 都不需要申明变量类型 他会自动的判断类型

 lua中的一个变量 可以随便赋值 ——自动识别类型

 通过 type 函数 返回值时string 我们可以得到变量的类型

lua中可以直接使用没有初始化的变量，默认为nil
]]

type(xxx)
```



## 字符串操作

### 获取长度

```lua
--获取字符串的长度
print("**********字符串长度************")
s = "aBcdEfG字符串"
--一个汉字占3个长度
--英文字符 占1个长度
print(#s)
```



### 多行打印

```lua
--lua中也是支持转义字符的
print("123\n123")

s = [[我是
xxx
]]
print(s)
```



### 字符串拼接

```lua
--字符串拼接 通过..
print( "123" .. "456" )
s1 = 111
s2 = 111
print(s1 .. s2)

print(string.format("我是唐老狮，我今年%d岁了", 18))
--%d :与数字拼接
--%a：与任何字符拼接
--%s：与字符配对
```



### 其他类型转字符串

```lua
a = true
print(tostring(a))
```



### 字符串提供公共方法

```lua
str = "abCdefgCd"
--小写转大写的方法
print(string.upper(str))
--大写转小写
print(string.lower(str))
--翻转字符串
print(string.reverse(str))
--字符串索引查找
print(string.find(str, "Cde"))
--截取字符串
print(string.sub(str, 3, 4))
--字符串重复
print(string.rep(str, 2))
--字符串修改
print(string.gsub(str, "Cd", "**"))
--字符转 ASCII码
a = string.byte("Lua", 1)
print(a)
--ASCII码 转字符
print(string.char(a))

```



## 运算符



### 算数运算符 

```
 + - * / %(取余) ^(幂)
```

### 条件运算符

```
> < >= <= == ~=(不等于)
```

### 逻辑运算符

```lua
&&  ||  !   “短路”
and  or  not  lua中 也遵循逻辑运算的 “短路” 规则

and前为false则直接打印false而不去判断下一个变量是什么
or前为true则直接判断为true而不去判断下一个变量是什么

nil也被判断为false
```

+ lua不支持为运算符和三目运算符

  

## 条件分支

### if条件语句

```lua
a = 9
--if 条件 then.....end
--单分支
if a > 5 then
	print("123")
end

--双分支
-- if 条件 then.....else.....end
if a < 5 then
	print("123")
else
	print("321")
end

--多分支
-- if 条件 then.....elseif 条件 then....elseif 条件 then....else.....end
if a < 5 then
	print("123")
--lua中 elseif 一定是连这些 否则报错
elseif a == 6 then
	print("6")
elseif a == 7 then
	print("7")
elseif a == 8 then
	print("8")
elseif a == 9 then
	print("9")
else
	print("other")
end


if a >= 3 and a <= 9 then
	print("3到9之间")
end
```



+ 不支持switch
+ 不支持三目运算符



## 循环

### while

```lua
num = 0
--while 条件 do ..... end
while num < 5 do
	print(num)
	num = num + 1
end
```

### repeat until

```lua
num = 0
--repeat ..... until 条件 （注意：条件是结束条件）
repeat
	print(num)
	num = num + 1
until num > 5 --满足条件跳出 结束条件
```

### for

```lua
for i =2,5 do --默认递增 i会默认+1
	print(i)
end

for i =1,5,2 do --如果要自定义增量 直接逗号后面写
	print(i)
end

for i =5,1,-1 do --如果要自定义增量 直接逗号后面写
	print(i)
end
```



## 函数

### 函数声明

```lua
function F1()
	print("F1函数")
end
F1()
--有点类似 C#中的 委托和事件
F2 = function()
	print("F2函数")
end
F2()
```

### 函数传参和返回值

```lua
function F3(a)
	print(a)
end
F3(1)
F3("123")
F3(true)
--如果你传入的参数 和函数参数个数不匹配
--不会报错 只会补空nil 或者 丢弃
F3()
F3(1,2,3)

function F4(a)
	return a, "123", true
end
--多返回值时 在前面申明多个变量来接取即可
--如果变量不够 不影响 值接取对应位置的返回值
--如果变量多了 不应 直接赋nil
temp, temp2, temp3, temp4 = F4("1")
```

### 变长参数

```lua
function F7( ... )
	--变长参数使用 用一个表存起来 再用
	arg = {...}
	for i=1,#arg do
		print(arg[i])
	end
end
```



+ 函数类型为function

  

+ 不支持函数重载 ，默认调用最后一个声明的函数

  

  

### 函数嵌套

```lua
function F8()
	return function()
		print(123);
	end
end
f9 = F8()
f9()

--闭包
function F9(x)
	--改变传入参数的生命周期
	return function(y)
		return x + y
	end
end

f10 = F9(10)
f10(5)
```



## 表



+ 表是一切复杂数据的基础，数组，多维数组， 字典， 类等

  

+ 表的索引从1开始，nil变量在尾部将不被计算到长度中

  

+ 自定义索引值取长度时，在连续索引值且都不为nil结束后只取间隔为1且不为nil的索引值，超过或为nil都不计入长度，符合长度去最后一个合法索引值

  ```lua
  a = {[1] = 1,[2] = 2,[3] = 3,[4] = 4,[6] = "1231"}
  
  --如1至3中有nil变量则取长会在nil前截止
  --此表取长可取至6
  --如6为nil则只取到4
  ```

  

### 迭代器遍历

+ ipairs

  ```lua
  a = {[0] = 1, 2, [-1]=3, 4, 5, [5] = 6}
  --ipairs
  --ipairs遍历 还是 从1开始往后遍历的 小于等于0的值得不到
  --只能找到连续索引的 键 如果中间断序了 它也无法遍历出后面的内容
  for i,k in ipairs(a) do
  	print("ipairs遍历键值"..i.."_"..k)
  end
  ```

+ pairs

  ```lua
  --它能够把所有的键都找到 通过键可以得到值 建议使用其遍历不规则的表
  for i,v in pairs(a) do
  	print("pairs遍历键值"..i.."_"..v)
  end
  
  for i in pairs(a) do
  	print("pairs遍历键"..i)
  end
  ```



### 字典

+ 字典声明

  ```lua
  --字典是由键值对构成 
  a = {["name"] = "gcb", ["age"] = 14, ["1"] = 5}
  ```

  

+ 访问

  ```lua
  --访问当个变量 用中括号填键 来访问
  print(a["name"])
  print(a["age"])
  print(a["1"])
  --还可以类似.成员变量的形式得到值
  print(a.name)
  print(a.age)
  --虽然可以通过.成员变量的形式得到值 但是不能是数字，无法点访问数字
  print(a["1"])
  ```

  

+ 增删改

  ```lua
  --修改，直接访问赋值
  a["name"] = "TLS";
  print(a["name"])
  print(a.name)
  --新增，加key值赋值
  a["sex"] = false
  print(a["sex"])
  print(a.sex)
  --删除，置nil
  a["sex"] = nil
  print(a["sex"])
  print(a.sex)
  ```

  

+ 遍历

  ```lua
  --如果要模拟字典 遍历一定用pairs
  for k,v in pairs(a) do
  	--可以传多个参数 一样可以打印出来
  	print(k,v)
  end
  
  for k in pairs(a) do
  	print(k)
  	print(a[k])
  end
  
  for _,v in pairs(a) do
  	print(_, v)
  end
  ```

  

### 类

+ 成员申明

  ```lua
  --Lua中是默认没有面向对象的 需要我们自己来实现
  --成员变量 成员函数。。。。
  Student = { 
  	--年龄
  	age = 1, 
  	--性别
  	sex = true,
  	--成长函数
  	Up = function()
  		--这样写 这个age 和表中的age没有任何关系 它是一个全局变量
  		--print(age)
  
  		--想要在表内部函数中 调用表本身的属性或者方法
  		--一定要指定是谁的 所以要使用 表名.属性 或 表名.方法
  		print(Student.age)
  		print("我成长了")
  	end,
  	--学习函数
  	Learn = function(t)
  		--第二种 能够在函数内部调用自己属性或者方法的 方法
  		--把自己作为一个参数传进来 在内部 访问
  		print(t.sex)
  		print("好好学习，天天向上")
  	end
  }
  
  --Lua中 .和冒号的区别
  Student.Learn(Student)
  --冒号调用方法 会默认把调用者 作为第一个参数传入方法中
  Student:Learn()
  
  --申明表过后 在表外去申明表有的变量和方法
  Student.name = "gcb"
  --函数第二种声明
  Student.Speak = function()
  	print("说话")
  end
  --函数的第三种申明方式
  function Student:Speak2() --用冒号声明默认带有一个默认参数self
  	--lua中 有一个关键字 self 表示 默认传入的第一个参数
  	print(self.name .. "说话")
  end
  ```

  

### 公共操作



+ 插入

  ```lua
  t1 = { {age = 1, name = "123"}, {age = 2, name = "345"} }
  
  t2 = {name = "gcb", sex = true}
  print("**********插入************")
  --插入
  print(#t1)
  table.insert(t1, t2);
  ```



+ 移除

  ```lua
  --删除指定元素
  --remove方法 传表进去 会移除最后一个索引的内容
  
  table.remove(t1)
  
  --remove方法 传两个参数 第一个参数 是要移除内容的表
  --第二个参数 是要移除内容的索引
  
  table.remove(t1, 1)
  
  ```

  

+ 排序

  ```lua
  t2 = {5,2,7,9,5}
  --传入要排序的表 默认 降序排列
  table.sort(t2)
  for _,v in pairs(t2) do
  	print(v)
  end
  
  --传入两个参数 第一个是用于排序的表
  --第二个是 排序规则函数
  table.sort(t2, function(a,b)
  	if a > b then
  		return true
  	end
  end)
  for _,v in pairs(t2) do
  	print(v)
  end
  ```

  

+ 拼接

  ```lua
  tb = {"123", "456", "789", "10101"}
  --连接函数 用于拼接表中元素 返回值 是一个字符串
  str = table.concat(tb, ",")
  ```

  

## 多脚本执行



### 局部变量和全局变量

```lua
--本地（局部）变量的关键字 local
--全局变量不加local
```



### 多脚本执行

```lua
--关键字 require("脚本名") require('脚本名')
```



### 脚本卸载

```lua
--如果是require加载执行的脚本 加载一次过后不会再被执行
require("Test")
--package.loaded["脚本名"]
--返回值是boolean 意思是 该脚本是否被执行
print(package.loaded["Test"])
--置nil卸载已经执行过的脚本
package.loaded["Test"] = nil
print(package.loaded["Test"])

--require 执行一个脚本时  可以再脚本最后返回一个外部希望获取的内容
local testLA = require("Test")
print(testLA)
```



### _G表

```lua
--_G表是一个总表(table) 他将我们申明的所有全局的变量都存储在其中
for k,v in pairs(_G) do
	print(k,v)
end
--本地变量 加了local的变量时不会存到大_G表中
```



## 特殊用法

### 多变量赋值

```lua
local a,b,c = 1,2,"123"
--多变量赋值 如果后面的值不够 会自动补空
--多变量赋值 如果后面的值多了 会自动省略
```



### 多返回值

```lua
function Test()
	return 10,20,30,40
end
--多返回值时 你用几个变量接 就有几个值
--如果少了 就少接几个 如果多了 就自动补空
```



### and or

+ ```lua
  --逻辑与 逻辑或
  -- and or 他们不仅可以连接 boolean 任何东西都可以用来连接
  -- 在lua中 只有 nil 和 false 才认为是假
  -- "短路"——对于and来说  有假则假  对于or来说 有真则真
  -- 所以 他们只需要判断 第一个 是否满足 就会停止计算了
  
  --lua不支持三目运算符 但可以模拟
  x = 1
  y = 2
  -- ? :
  local res = (x>y) and x or y
  --(x>y) and x ——> x
  -- x or y —— > x
  
  --(x>y) and x ——> (x>y)
  -- (x>y) or y ——> y
  
  ```

  

## 协程



### 协程创建

```lua
--常用方式
--coroutine.create() 返回值为线程对象
fun = function()
	print(123)
end
co = coroutine.create(fun)
--协程的本质是一个线程对象
print(co)
print(type(co))

--coroutine.wrap() 返回值为函数对象
co2 = coroutine.wrap(fun)
```



### 协程启动

```
--第一种方式 对应的 是通过 create创建的协程
coroutine.resume(co)
--第二种方式
co2()
```



### 协程挂起

```lua
fun2 = function( )
	local i = 1
	while true do
		print(i)
		i = i + 1
		--协程的挂起函数
		coroutine.yield(i)
	end
end

co3 = coroutine.create(fun2)
--默认第一个返回值 是 协程是否启动成功
--yield里面的返回值
isOk, tempI = coroutine.resume(co3)
print(isOk,tempI)
isOk, tempI = coroutine.resume(co3)
print(isOk,tempI)
isOk, tempI = coroutine.resume(co3)
print(isOk,tempI)

co4 = coroutine.wrap(fun2)
--这种方式的协程调用 也可以有返回值 只是没有默认第一个返回值了

print("返回值"..co4())
print("返回值"..co4())
print("返回值"..co4())
```



### 线程状态

```lua
--coroutine.status(协程对象)
--dead 结束
--suspended 暂停
--running 进行中
print(coroutine.status(co3))
print(coroutine.status(co))

--这个函数可以得到当前正在 运行的协程的线程号
print(coroutine.running())
```



## 元表

### 元表概念

```lua
--任何表变量都可以作为另一个表变量的元表
--任何表变量都可以有自己的元表（父表）
--当我们子表中进行一些特定操作时
--会执行元表中的内容
```



### 元表设置和获取

```lua
meta = {}
myTable = {}
--设置元表函数
--第一个参数 子表
--第二个参数 元表（爸爸）
setmetatable(myTable, meta)

--获取元表
getmetatable(myTable)
```



### 特定操作

1.__tostring

```lua
meta2 = {
	--当子表要被当做字符串使用时 会默认调用这个元表中的tostring方法
	__tostring = function(t)
		return t.name
	end
}
myTable2 = {
	name = "gcb"
}
--设置元表函数
--第一个参数 子表
--第二个参数 元表（爸爸）
setmetatable(myTable2, meta2)

print(myTable2)
```

2. __call

```lua
meta3 = {
	--当子表要被当做字符串使用时 会默认调用这个元表中的tostring方法
	__tostring = function(t)
		return t.name
	end,
	--当子表被当做一个函数来使用时 会默认调用这个__call中的内容
	--当希望传参数时 一定要记住 默认第一个参数 是调用者自己
	__call = function(a, b)
		print(a)
		print(b)
		print("gcbaaaa")
	end
}
myTable3 = {
	name = "gcb2"
}
--设置元表函数
--第一个参数 子表
--第二个参数 元表（爸爸）
setmetatable(myTable3, meta3)
--把子表当做函数使用 就会调用元表的 __call方法
myTable3(1)
```

3. 运算符重载

```lua
meta4 = {
	--相当于运算符重载 当子表使用+运算符时 会调用该方法
	--运算符+
	__add = function(t1, t2)
		return t1.age + t2.age
	end,
	--运算符-
	__sub = function(t1, t2)
		return t1.age - t2.age
	end,
	--运算符*
	__mul = function(t1, t2)
		return 1
	end,
	--运算符/
	__div = function(t1, t2)
		return 2
	end,
	--运算符%
	__mod = function(t1, t2)
		return 3
	end,
	--运算符^
	__pow = function(t1, t2)
		return 4
	end,
	--运算符==
	__eq = function(t1, t2)
		return true
	end,
	--运算符<
	__lt = function(t1, t2)
		return true
	end,
	--运算符<=
	__le = function(t1, t2)
		return false
	end,
	--运算符..
	__concat = function(t1, t2)
		return "567"
	end

}
```

4. __index

```lua
meta6Father = {
	age = 1
}
meta6Father.__index = meta6Father

meta6 = {
	--age = 1
}
--__index的赋值 写在表外面来初始化
meta6.__index = meta6
--meta6.__index = {age = 2}

myTable6 = {}
setmetatable(meta6, meta6Father)
setmetatable(myTable6, meta6)
--得到元表的方法
print(getmetatable(myTable6))

--__index 当子表中 找不到某一个属性时 
--会到元表中 __index指定的表去找属性
print(myTable6.age)
--rawget 当我们使用它是 会去找自己身上有没有这个变量
--myTable6.age = 1
print(rawget(myTable6, "age"))
```

5. __newindex

```lua
--newIndex 当赋值时，如果赋值一个不存在的索引
--那么会把这个值赋值到newindex所指的表中 不会修改自己
meta7 = {}
meta7.__newindex = {}
myTable7 = {}
setmetatable(myTable7, meta7)
myTable7.age = 1
print(myTable7.age)
--rawset 该方法 会忽略newindex的设置 只会该自己的变量
rawset(myTable7, "age", 2)
print(myTable7.age)
```



##  lua的oop编程

### 封装

```lua
--面向对象 类 其实都是基于 table来实现
--元表相关的知识点
Object = {}
Object.id = 1

function Object:Test()
	print(self.id)
end

--冒号 是会自动将调用这个函数的对象 作为第一个参数传入的写法
function Object:new()
	--self 代表的是 我们默认传入的第一个参数
	--对象就是变量 返回一个新的变量
	--返回出去的内容 本质上就是表对象
	local obj = {}
	--元表知识 __index 当找自己的变量 找不到时 就会去找元表当中__index指向的内容
	self.__index = self
	setmetatable(obj, self)
	return obj
end
```



###  继承

```lua
--写一个用于继承的方法
function Object:subClass(className)
	-- _G知识点 是总表 所有声明的全局标量 都以键值对的形式存在其中
	_G[className] = {}
	--写相关继承的规则
	--用到元表
	local obj = _G[className]
	self.__index = self
	--子类 定义个base属性 base属性代表父类
	obj.base = self
	setmetatable(obj, self)
end

Object:subClass("Person")

local p1 = Person:new()
print(p1.id)
p1.id = 100
print(p1.id)
p1:Test()
```

### 多态

```lua
--相同行为 不同表象 就是多态
--相同方法 不同执行逻辑 就是多态
Object:subClass("GameObject")
GameObject.posX = 0;
GameObject.posY = 0;
function GameObject:Move()
	self.posX = self.posX + 1
	self.posY = self.posY + 1
	print(self.posX)
	print(self.posY)
end

GameObject:subClass("Player")
function Player:Move()
	--base 指的是 GameObject 表（类）
	--这种方式调用 相当于是把基类表 作为第一个参数传入了方法中
	--避免把基类表 传入到方法中 这样相当于就是公用一张表的属性了
	--我们如果要执行父类逻辑 我们不要直接使用冒号调用
	--要通过.调用 然后自己传入第一个参数 
	self.base.Move(self)
end

local p1 = Player:new()
p1:Move()
p1:Move()
--目前这种写法 有坑 不同对象使用的成员变量 居然是相同的成员变量
--不是自己的
local p2 = Player:new()
p2:Move()
```



## 自带库

### os

```lua
--系统时间
print(os.time())
--自己传入参数 得到时间
print(os.time({year = 2014, month = 8, day = 14}))

--os.date("*t")
local nowTime = os.date("*t")
for k,v in pairs(nowTime) do
	print(k,v)
end
```

![image-20220721010439891](C:\Users\86157\AppData\Roaming\Typora\typora-user-images\image-20220721010439891.png)

### 数学运算

```lua
--math
--绝对值
print(math.abs(-11))
--弧度转角度
print(math.deg(math.pi))
--三角函数 传弧度
print(math.cos(math.pi))

--向下向上取整
print(math.floor(2.6))
print(math.ceil(5.2))

--最大最小值
print(math.max(1,2))
print(math.min(4,5))

--小数分离 分成整数部分和小数部分
print(math.modf(1.2))

--随机数
--先设置随机数种子
math.randomseed(os.time())--设置随机种子，自带种子是固定的
print(math.random(100))
print(math.random(100))
--开方
print(math.sqrt(4))
```

![image-20220721010958996](C:\Users\86157\AppData\Roaming\Typora\typora-user-images\image-20220721010958996.png)

### 路径

```lua
--lua脚本加载路径
print(package.path)
package.path = package.path .. ";C:\\"
print(package.path)
```



## lua垃圾处理

+ 关键字——collectgarbage（）

### 命令

```lua
test = {id = 1, name = "123123"}
--垃圾回收关键字
--collectgarbage
--获取当前lua占用内存数 K字节 用返回值*1024 就可以得到具体的内存占用字节数
print(collectgarbage("count"))
--lua中的机制和C#中垃圾回收机制很类似 解除羁绊 就是变垃圾
test = nil
--进行垃圾回收 理解有点像C#的 GC
collectgarbage("collect")

print(collectgarbage("count"))

--lua中 有自动定时进行GC的方法
--Unity中热更新开发 尽量不要去用自动垃圾回收
```

![image-20220721011412356](C:\Users\86157\AppData\Roaming\Typora\typora-user-images\image-20220721011412356.png)