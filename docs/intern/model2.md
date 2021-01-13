## 多对多的关系

```ruby
ont-to-one， 人 To 身份证     # 因为一个人只能有一张身份证
one-to-many, 游戏 <=> 英雄 班级 <=> 学生 #  
many-to-many,  老师 <=> 学生     # 比如老师是一个tabel, 有很多老师爹名字， 学生是一个tabel, 下面也有很多学生名字
                                #  因为老师可以教很多学生，学生也可以有很多老师
```


- one-to-many 是最好理解的
- 很多时候，one-to-one, 从现实考虑，是没有存在的意义



- many-to-many: 
  - 需要中间表































