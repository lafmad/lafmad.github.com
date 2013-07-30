---
title: 第十一章困惑 外键 及 反转relationships表
layout: post
guid: urn:uuid:7ef37791-dd7e-49b5-a490-346912ab3f1b
tags:
  - rails
  - railstutorail 学习笔记
---


[简书版](http://jianshu.io/p/d4AcLx)


不知道有谁学到11章时和我一样困惑的，所谓的对调两列的位置，组建成reverse_ralationships表究竟是什么意思。毕竟表根本没变就是原来那个表阿，已经完整的体现了用户间关系。谁是关注谁是被关注根本没变，追人的没突然变成被追啊，携带信息完全一样。

没错，真相就是：**其实表就是原来的表，根本没变。表没有反转，反转的是外键，从而反转查询方向。因为Users表和relationships表通过外键一一对应，所以把表重命是为了另设外键。根本就没有任何将表进行反转的处理**。你把User.rb中的reverse_relationships 都改成 same_relationships 试试，结果一样。取名reverse, 其实是外键和查询方向的reverse。



***
##先说外键
***

#第十章的user.microposts比较简单, 生成micropost时无须指定外键，因为micopost 模型中就是user_id，只要正确定义了用户和微博之间的关联关系（has_many,belongs_to）,使用user.microposts.build创建新微薄时，rails 会自动将micropost中的user_id赋值为相应的user.id。**



>运行验证一下，rails console --sandbox:  
`1.9.3-p429 :001 > User.first.microposts.build`  
  **会新建一个micropost，micropost的user_id属性自动赋值为 user.id （此例为User.first.id="1"），其他属性为nil，待给参数**  
`User Load (0.5ms)  SELECT "users".* FROM "users" LIMIT 1`  
`=> #<Micropost id: nil, content: nil, user_id: 1, created_at: nil, updated_at: nil> `  


###而relationship表中没有叫user_id 的，只有对应User的follower_id和followed_id,所以User表必须通过指定的外键和relationship表一一对应。
书中先指定的外键是follower_id,(**你完全可以先指定followed_id**)，那么使用 user.relationships.build(followed_id: ...)建立relationship时，被设为外键的follower_id 会被自动赋对应的 user.id值，而followed_id是你给的参数，从而得到relationship表中的一行具体的relationship
***
>`1.9.3-p429 :002 > User.first.relationships`  
  **会列出 User.first 的所有的 follower_id =1的 relationships表**  
`User Load (0.4ms)  SELECT "users".* FROM "users" LIMIT 1`  
`Relationship Load (46.7ms)  SELECT "relationships".* FROM "relationships" WHERE "relationships"."follower_id" = 1`  
`=> [#<Relationship id: 21, follower_id: 1, followed_id: 2, created_at: "2013-07-21 13:52:10", updated_at: "2013-07-21 13:52:10">]`  
****

>`1.9.3-p429 :003 > User.first.relationships.build`  
  **会新建一个relationship, 其中follower_id 是User指定的外键，被赋值User.first.id，而followed_id则是nil，待给参数**  
>`User Load (0.4ms)  SELECT "users".* FROM "users" LIMIT 1 `  
>`=> #<Relationship id: nil, follower_id: 1, followed_id: nil, created_at: nil, updated_at: nil> `  
***
>`1.9.3-p429 :004 > User.first.relationships.build(followed_id: 2)`  
> **想让用户1关注用户2，传入参数。注意没save,relationship_id为nil。要save用User.first.relationships.create!(followed_id: 2))**  
>`User Load (0.4ms)  SELECT "users".* FROM "users" LIMIT 1`  
>`=> #<Relationship id: nil, follower_id: 1, followed_id: 2, created_at: nil, updated_at: nil> `  




###relationship表建立后，就可以通过  

`has_many:followeds,through: :relationships`  
使用followed_id 生成 user.followeds 数组。为了好听，书中用  
`has_many:followed_users, through: :relationships, source: :followed` 把user.followeds改成了 user.followed_users  

user.followed_users 通过relationships表将 follower_id =(user.id) 所有对应的 followed_id 从数据库中找出生成数组。即该user的“关注的人”列表。  
（例如下面我找User.first所有关注的人，即查询follower_id = 1 对应的 followed_id)  

>运行rails console --sandbox:  
>`1.9.3-p429 :005 > User.first.followed_users`  
  **得到了User.first 的所有关注的人（我这只有一个，User.id=2的, 说明User1 只关注了 User2)**  
>`User Load (0.4ms)  SELECT "users".* FROM "users" LIMIT 1`  
>`User Load (0.4ms)  SELECT "users".* FROM "users" INNER JOIN "relationships" ON "users"."id" = "relationships"."followed_id" WHERE "relationships"."follower_id" = 1`  
>`=> [#<User id: 2, name: "Rails Tutorial", email: "example@railstutorial.org", created_at: "2013-07-21 10:50:11", updated_at: "2013-07-21 10:50:11", password_digest: "$2a$.....", remember_token: "9c2eccc....."]`  
***


***
###困惑的revese_relationships表
***

上面说明了指定了follower_id为外键的情况

#所以User.rb模型中这两句的意思是
`has_many :relationships,foreign_key:"follower_id",dependent: :destroy`  
对于relationships表，User_id固定对应follower_id，所以使用user.relationships得到的是所有 follower_id值为user_id的 relationship数组

  
`has_many :followed_users, through: :relationships, source: :followed`  
通过表查询对应的followed_id拥有了很多followed_users。所以使用user.followed_users可得到该user的followed_users数组，即在追哪些人。  


下面说怎么通过关系表（**再次强调，就是一张表**） 查找出该user所有的“粉丝”列表。  

通过调换 followed_id为外键（所以通过表查询的方向就反过来了，现在固定的是followed_id，来查询表中对应的follower_id数组。(比如对于user2,  user.followers则通过relationships表 将 followed_id =2 对应的所有 follower_id 找出来，即user2的粉丝数组)  

###所以User.rb模型中这两句的意思是
`has_many :same_relationships, foreign_key: "followed_id",class_name:  "Relationship",dependent:   :destroy`  
对于same_relationships表（呵呵，不用reverse试试）,User_id固定对应于followed_id,所以使用user.same_relationships得到的是所有 followed_id值为user_id的 **relationship数组（没reverse啥事）**  


`has_many :followers, through: :same_relationships, source: :follower`  
通过表查询对应的follower_id拥有了很多followers.所以使用user.followers可得到该user的followers数组，即粉丝团）  

（**外键和表一一对应，所以表得改名,否则查询关系就冲突了，user.relationships 不知道user_id赋值给谁查询。**)  



***

###(其实认真的看看下面4句中的SELECT语句就明白了，全是通过relationship表查询数据库，变的只是查询的外键值）  
>`1.9.3-p429 :006 > user2 = User.find(2)`  
>`1.9.3-p429 :007 > user2.relationships`  
>`Relationship Load (0.2ms)  SELECT "relationships".* FROM "relationships" WHERE "relationships"."follower_id" = 2`  
>`=> [#<Relationship id: 24, follower_id: 2, followed_id: 1, created_at: "2013-07-29 13:29:56", updated_at: "2013-07-29 13:29:56">] `
***
 >`1.9.3-p429 :008 > user2.same_relationships`  
>`Relationship Load (30.8ms)  SELECT "relationships".* FROM "relationships" WHERE "relationships"."followed_id" = 2`  
>`=> [#<Relationship id: 21, follower_id: 1, followed_id: 2, created_at: "2013-07-21 13:52:10", updated_at: "2013-07-21 13:52:10">]`
***
>`1.9.3-p429 :009 > user2.followers`  
> `User Load (0.3ms)  SELECT "users".* FROM "users" INNER JOIN "relationships" ON "users"."id" = "relationships"."follower_id" WHERE "relationships"."followed_id" = 2`  
>`=> [#<User id: 1, name: "lafmad", email: "inaircastle@gmail.com", created_at: "2013-07-16 14:01:47", updated_at: "2013-07-20 03:14:16", password_digest: "$2a$10$....", remember_token: "tRLqtITZxX..."] `
***
>`1.9.3-p429 :010 > user2.followed_users`  
`User Load (0.5ms)  SELECT "users".* FROM "users" INNER JOIN "relationships" ON "users"."id" = "relationships"."followed_id" WHERE "relationships"."follower_id" = 2`  
`=> [#<User id: 1, name: "lafmad", email: "inaircastle@gmail.com", created_at: "2013-07-16 14:01:47", updated_at: "2013-07-20 03:14:16", password_digest: "$2a$10$m5bBDpsDXDv......", remember_token: "tRLqtIT..."]`





***

写完了我是明白多一点了，如果有读者的话，希望没把你搞的更糊涂。文章是以肯定的语气写的，因为我电脑上它确实是这么运行的，但也有可能在错误的解释正确的结果。  


沉住气，也许忽然间一回头就明白了（然后又糊涂了，然后又明白了，嗯嗯，就是这样)。  






***

以上

***

