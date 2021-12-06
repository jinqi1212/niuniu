

jupyter notebook  

# 1.if 条件语句

```python
if 语句用于判断某个条件是否成立。如果成立，则执行语句内的程序；否则跳过if语句，执行后面的内容，语法如下

if 条件表达式
	语句块
```

示例

```python
print('请输入学生考试成绩')
score = int(input())
print(score >= 60)
if score >=60:
    print('合格')

输出结果
请输入学生考试成绩
124235
True
合格

```

## 条件表达式与关系运算符

示例

```python
print(10 == 9)
False
print(10 != 9)
True
print(10 >= 9)
True
print(10 < 9)
False
```

## if-else条件语句

```python
语法
if 条件表达式
	语句块1
else：
	语句块2
```

示例

```python
print('请输入学生考试成绩')
score = int(input())
if score >= 90:
    print('优秀')
elif score >= 70:
    print('良好')
elif score >= 60:
    print('合格')python
else:
    print('需要努力')
    
    
请输入学生考试成绩
123124
优秀
```

# 2.Python循环

## 2.1 while循环

```python
语法
while 条件表达式：
	循环操作语句
```

示例

```python
count = 0
while(count < 5):
    count = count + 1
    print(count)
print('循环结束')

1
2
3
4
5
循环结束
```

```python
i = 1
sum = 0
while i <= 5:
    print('请输入第%d门课程的考试成绩' % i)
    sum = sum + int(input())
    i = i+1
avg=sum/(i-1)
print('5门课程的平均成绩是%d'% avg)

请输入第1门课程的考试成绩
1
请输入第2门课程的考试成绩
2
请输入第3门课程的考试成绩
3
请输入第4门课程的考试成绩
4
请输入第5门课程的考试成绩
5
5门课程的平均成绩是3
```

```python
import random
random_num =[]
while(9 not in random_num):
    random_num.append(random.randint(1,10))
print(random_num,len(random_num))

[1, 3, 2, 8, 8, 10, 10, 9] 8
# 往空列表中添加随机数，直到添加的数为9，则终止
```

### 2.1.2 字符串的格式化输出

| 替换符 | 描述           |
| ------ | -------------- |
| %d     | 格式化整型     |
| %s     | 格式化字符串   |
| %f     | 格式化浮点数字 |

示例：

```python
num=5
numStr="5"
numF=5.55
print("第%d名"% num)
print("第%s名"% numStr)
print("浮点数是: %f"% numF)
print("第一个数字%d,第二个字符串%s,第三个是浮点数%f" %(num,numStr,numF))

第5名
第5名
浮点数是: 5.550000
第一个数字5,第二个字符串5,第三个是浮点数5.550000
```

```python
num={"first":1,"second":"tow"}
print("第%(first)d名和第%(second)s名"% num)

第1名和第tow名
```

```python
s1 = "i am %s,i am %d years old" %('jeck',26)
s2 = "i am %(name)s,i am %(age)d years old" % {'name':'jeck','age':26}
s3 = "i am %(name)+10s,i am %(age)d years old, i am %(height).2f"%{'name':'jeck','age':26,'height':1.7512}
s4 = "原数：%d,八进制：%o，十六进制:%x" %(15,15,15)
s5 = '百分比显示: %.2f %%'%(0.7777777*100)
print(s1)
print(s2)
print(s3)
print(s4)
print(s5)

i am jeck,i am 26 years old
i am jeck,i am 26 years old
i am       jeck,i am 26 years old, i am 1.75
原数：15,八进制：17，十六进制:f
百分比显示: 77.78 %
```

```python
f1 = "i am {0}，i am {1}years old".format('jeck',26)
f2 = "i am (name),i am {age}years old".format(**{'name':'jeck','age':26})
f3 = "--{name:*^10s}-- =={age:<10.2f}==".format(name='jeck',age=26.457)
f4 = "原数:{:d},二进制:{:b},八进制:{:o},十六进制x:{:x},十六进制X:{:X}".format(15,15,15,15,15)
f5 = "原数:{:2F},百分号表示{:2%},原数:{:d},自动分割表示{:,}".format(0.75,0.75856,10000000,10000000)
print(f1)
print(f2)
print(f3)
print(f4)
print(f5)

i am jeck，i am 26years old
i am (name),i am 26years old
--***jeck***-- ==26.46     ==
原数:15,二进制:1111,八进制:17,十六进制x:f,十六进制X:F
原数:0.750000,百分号表示75.856000%,原数:10000000,自动分割表示10,000,000
```

### 2.1.3 while 循环嵌套

```python
j=1
prompt='请输入学生姓名'
while j <=2:
    sum=0
    i=1
    name=input(prompt)
    while i<=5:
        print('请输入第%d门课程的考试成绩'% i)
        sum=sum+int(input())
        i=i+1
    avg=sum/(i-1)
    print('%s的5门课程的平均成绩是:%d'%(name,avg))
    j=j+1
print('学生成绩输入完成')

请输入学生姓名xx
请输入第1门课程的考试成绩
1
请输入第2门课程的考试成绩
2
请输入第3门课程的考试成绩
3
请输入第4门课程的考试成绩
4
请输入第5门课程的考试成绩
5
xx的5门课程的平均成绩是:3
请输入学生姓名yy
请输入第1门课程的考试成绩
2
请输入第2门课程的考试成绩
3
请输入第3门课程的考试成绩
4
请输入第4门课程的考试成绩
5
请输入第5门课程的考试成绩
6
yy的5门课程的平均成绩是:4
学生成绩输入完成
```

## 2.2 for 循环

```python
语法
for 变量 in 集合：
	语句块
```

```python
for letter in 'Python':
    print('Current letter %s' % letter)

Current letter P
Current letter y
Current letter t
Current letter h
Current letter o
Current letter n    
# 语句把python字符串的字符逐个遍历，把字符复制给变量letter，然后执行for对应的语句块
```

```python
fruits=["西瓜","苹果","葡萄"]
for fruit in fruits:
    print(fruit)

西瓜
苹果
葡萄
```

```python
print(list(range(0,5)))
print(list(range(0,5,2)))

[0, 1, 2, 3, 4]
[0, 2, 4]
```

```python
for i in range (0,5):
    print('上海欢迎您')
  
上海欢迎您
上海欢迎您
上海欢迎您
上海欢迎您
上海欢迎您
```

### 2.2.1for循环实例

```python
示例：（接收某个学生三门课程的考试成绩，计算输出平均成绩。）
subjects=('Python','MySQL','Linux')
sum=0
for i in subjects:
    print('请输入%s考试成绩'%i)
    score=int(input())
    sum+=score
avg= sum/len(subjects)
print('小明的平均成绩是%d'% avg)

请输入Python考试成绩
231
请输入MySQL考试成绩
123
请输入Linux考试成绩
43
小明的平均成绩是132
```

### 2.2.2 运算逻辑符

| 运算符 | 名称   | 描述                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| and    | 逻辑与 |                                                              |
| or     | 逻辑或 |                                                              |
| not    | 逻辑非 | 求反运算，如果操作数值为True，则表达式值为False，反之则为True |

```python
print(not True)
print(True and False)
print(True or False)

False
False
True
```

###         2.2.3 for 循环嵌套

```python
students=['小明','小张']
subjects=('Python','MySQL','Linux')
for student in students:
    sum=0
    for subject in subjects:
        print ('请输入%s的%s考试成绩:'%(student,subject))
        score=int(input())
        sum+=score
    avg=sum/len(subjects)
    print('%s的平均成绩是%d'%(student,avg))
print('计算完成')

请输入小明的Python考试成绩:
123455
请输入小明的MySQL考试成绩:
1345436
请输入小明的Linux考试成绩:
24536
小明的平均成绩是497809
请输入小张的Python考试成绩:
22534
请输入小张的MySQL考试成绩:
2345
请输入小张的Linux考试成绩:
25346
小张的平均成绩是16741
计算完成
```

## 3.1 循环控制

### break循环

示例：（对输出平均成绩的代码进行修改，当成绩无效是，使用break退出循环。）

```python
students=['小明','小张']
subjects=('Python','MySQL','Linux')
for student in students:  # 外层循环
    sum=0
    for subject in subjects:  # 内层循环
        print ('请输入%s的%s考试成绩:'%(student,subject))
        score=int(input())
        if score < 0 or score > 100:
            print('输入的成绩需要大于0小于100，循环退出')
            break   # break 退出内层循环
        sum+=score
    avg=sum/len(subjects)
    print('%s的平均成绩是%d'%(student,avg))
    
请输入小明的Python考试成绩:
12
请输入小明的MySQL考试成绩:
12
请输入小明的Linux考试成绩:
12
小明的平均成绩是12
请输入小张的Python考试成绩:
344
输入的成绩需要大于0小于100，循环退出
小张的平均成绩是0
```

### continue语句

continue的作用和break不同，他不是结束整个循环，而是跳出当前一轮的设于语句，重新测试循环状态，准备进入下一轮循环。

示例：

```python
students=['小明','小张']
subjects=('Python','MySQL','Linux')
for student in students:
    sum=0
    i=0
    while(i<len(subjects)):
        print('请输入%s的%s考试成绩:'%(student,subjects[i]))
        score=int(input())
        if(score<0 or score>100):
            print('输入的成绩需要大于0且小于100,重新输入')
            continue
        sum+=score
        i=i+1
    avg=sum/len(subjects)
    print('%s的平均成绩是%d' %(student,avg))

请输入小明的Python考试成绩:
1415
输入的成绩需要大于0且小于100,重新输入
请输入小明的Python考试成绩:
12
请输入小明的MySQL考试成绩:
34
请输入小明的Linux考试成绩:
45
小明的平均成绩是30
```

## 4.循环综合案例

需求描述

（1） 显示操作的菜单，有3个选项，分别用字母N、E、Q表示

（2）N 表示输入新的用户名和密码

（3）E 表示使用用户名和密码登录

（4）Q表示退出程序

编写功能

```python
kgc={}
prompt='''
    (N)ew User Login
    (E)ntering User Login
    (Q)uit
Enter choice:'''
while True:
    choice=input(prompt).strip()[0].lower()
    # 接受键盘输入的字符串
    # 使用strip()函数去掉字符串前后的空格，
    # 然后获取输入字符串的第一个非空的字符。
    # 函数lower() 的作用是把字符变成小写
    print('\n--You picked:[%s]'% choice)
    if choice not in 'neq':
        print('--invaild option,try again--')
    else:
        if choice=='n':
            prompt1='login desired:'
            while True:
                # 当输入n时进行到代码块，使用while True不停循环，
                name=input(prompt1)
                if name in kgc:
                    prompt1='--name taken,try another:'
                    continue
                # 首先判断字典kgc中是不是已经存在了用户名，如果存在
                #则执行continue语句继续下次循环，让用户重新输入
                #用户名；不存在则执行break语句，退出while循环
                # 然后在输入对应的密码，把用户名和密码保存到字典中
                else:
                    break
            pwd=input('password')
            kgc[name]=pwd
        elif choice == 'e':
            #进入字符e对应的功能输入用户名name和密码pwd后，
            #通过输入的用户名在字典kgc中查找对应的密码password
            #判断字典中的密码和用户输入的密码是否相同，如果相同，
            # 输入欢迎文字；如果不通，输入登入失败的文字。
            name = input('login:')
            pwd=input('password:')
            password=kgc.get(name)
            if password == pwd:
                print('--Welcome back--',name)
            else:
                print('--Login incorrect--')
        else:
            print('quit')
            break
            
            


    (N)ew User Login
    (E)ntering User Login
    (Q)uit
Enter choice:n

--You picked:[n]
login desired:jiniqi
password123123

    (N)ew User Login
    (E)ntering User Login
    (Q)uit
Enter choice:e

--You picked:[e]
login:jinqi
password:123123
--Login incorrect--

    (N)ew User Login
    (E)ntering User Login
    (Q)uit
Enter choice:q

--You picked:[q]
quit
```

9*9乘法表

```python
for i in range (1,10):
    for j in range(1,i+1):
        print('%d*%d=%d' %(j,i,i*j),end="\t")
    print()
```

