---
title: mongoDB 总结
date: 2018-05-15 16:23:09
tags:
- mongoDB
categories:
- mongoDB
permalink: mongodb-note
---

# MongoDB

## 和 SQL 的区别

| SQL术语/概念 | MongoDB术语/概念 | 解释/说明 |
| --- | --- | --- |
| database | database | 数据库 |
| table | collection | 数据库表/集合 |
| row | document | 数据记录行/文档 |
| column | field | 数据字段/域 |
| index | index | 索引 |
| table joins |  | 表连接,MongoDB不支持 |
| primary key | primary key | 主键,MongoDB自动将_id字段设置为主键 |

## 数据类型

| 数据类型 | 描述 |
| --- | --- |
| String | 字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的 |
| Integer | 整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位 |
| Boolean | 布尔值。用于存储布尔值（真/假） |
| Double | 双精度浮点值。用于存储浮点值 |
| Min/Max keys | 将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比 |
| Array | 用于将数组或列表或多个值存储为一个键 |
| Timestamp | 时间戳。记录文档修改或添加的具体时间 |
| Object | 用于内嵌文档 |
| Null | 用于创建空值 |
| Symbol | 符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言 |
| Date | 日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date | 对象，传入年月日信息 |
| Object ID | 对象 ID。用于创建文档的 ID |
| Binary Data | 二进制数据。用于存储二进制数据 |
| Code | 代码类型。用于在文档中存储 JavaScript 代码 |
| Regular expression | 正则表达式类型。用于存储正则表达式 |

## 常用命令

**mongod**

启动数据库

> 使用默认参数 `mongod --config /usr/local/etc/mongod.conf`

**show dbs**

查看当前服务实例上所有的数据库

**use 数据库名称**

如果数据库不存在，则创建数据库，否则切换到指定数据库

**db**

查看当前所处的数据库

**show collections**

查看当前数据库中所有的集合

**db.createCollection("集合名称")**

创建集合

**db.集合名称.insert({数据文档})**

插入的每一条文档会自动帮我们生成一个_id字段,它是mongodb自动维护的,不需要我们关心

**db.集合名称.find()**

查询指定集合中所有的数据
可以通过 `db.集合名称.find().pretty()` 美化输出格式
默认是查询所有，可以通过：db.集合名称.find({查询条件}) 按条件查询集合中的数据

**db.集合名称.update({更新条件}, {要更新的字段})**

更新指定集合数据,注意点,要更新的字段一定要这样写 `{$set:{字段的名称:字段的值}}`

**db.集合名称.remove({删除条件})**

删除指定集合中的数据

**exit**

退出当前操作

**cls**

清屏

> 更新和删除时一般都需要带条件,除非是全部更新与全部删除,不过全部更新与全部删除这样很危险,实际操作过程中很少

# mongoose

## 概念

![IMG_1027](http://fairyever.qiniudn.com/IMG_1027.PNG)

## 基础操作

### 连接数据库

基础用法

```
mongoose.connect(url, options);
// 例如
mongoose.connect('mongodb://localhost/db1');
// 带有用户名和密码
mongoose.connect('mongodb://username:password@host:port/database?options...');
```

可选参数 `options`

| key | 含义 |
| --- | --- |
| db | 数据库设置 |
| server | 服务器设置 |
| replset | 副本集设置 |
| user | 用户名 |
| pass | 密码 |
| auth | 鉴权选项 |
| mongos | 连接多个数据库 |
| promiseLibrary | 用户定义promise |

示例代码

```
var options = {
  db: { native_parser: true },
  server: { poolSize: 5 },
  replset: { rs_name: 'myReplicaSetName' },
  user: 'myUserName',
  pass: 'myPassword'
}
mongoose.connect(uri, options);
```

如果要连接多个数据库，只需要设置多个url以,隔开，同时设置mongos为true

```
mongoose.connect('urlA,urlB,...', {
  mongos : true 
})
```

> `mongoose.connect` 返回的是 `Promise`

### 断开连接

```
mongoose.disconnect()
```

## Schema

### 支持的基本类型

* String
* Number
* Date
* Buffer
* Boolean
* Mixed
* ObjectId
* Array

### SchemaType

type属性指定SchemaType类型，不同的SchemaType类型还有其他不同的属性配置

```
var schema2 = new Schema({
  test: {
    type: String,
    lowercase: true
  }
});
```

公有配置

* **required** 必选验证器
* **default** 默认值。Any或function，如果该值是一个函数，则该函数的返回值将用作默认值
* **select** boolean值, 指定是否被投影
* **validate** 验证器
* **get** get方法，using Object.defineProperty()
* **set** set方法 using Object.defineProperty()
* **alias** 别名

[官方文档](http://mongoosejs.com/docs/schematypes.html)

### 初始化参数

safe: 用来设置安全模式. 实际上,就是定义入库时数据的写入限制. 比如写入时限等

```
//使用安全模式. 表示在写入操作时,如果发生错误,也需要返回信息.
var safe = true;
new Schema({ .. }, { safe: safe });

// 自定义安全模式. w为写入的大小范围. wtimeout设置写入时限. 如果超出10s则返回error
var safe = { w: "majority", wtimeout: 10000 };
new Schema({ .. }, { safe: safe });
```

toObject: 用来表示在提取数据的时候, 把documents 内容转化为Object内容输出. 一般而言只需要设置getters为true即可

```
var schema = new Schema({ name: String });
schema.path('name').get(function (v) {
  return v + ' is my name';
});
schema.set('toObject', { getters: true });
var M = mongoose.model('Person', schema);
var m = new M({ name: 'Max Headroom' });
console.log(m); // 返回obj
```

toJSON： 该是和toObject一样的使用. 通常用来把 documents 转化为Object. 但是, 需要显示使用toJSON()方法

```
var schema = new Schema({ name: String });
schema.path('name').get(function (v) {
  return v + ' is my name';
});
schema.set('toJSON', { getters: true, virtuals: false });
var M = mongoose.model('Person', schema);
var m = new M({ name: 'Max Headroom' });
console.log(m.toObject()); // { _id: 504e0cd7dd992d9be2f20b6f, name: 'Max Headroom' }
console.log(m.toJSON()); // { _id: 504e0cd7dd992d9be2f20b6f, name: 'Max Headroom is my name' }
// since we know toJSON is called whenever a js object is stringified:
console.log(JSON.stringify(m)); // { "_id": "504e0cd7dd992d9be2f20b6f", "name": "Max Headroom is my name" }
```

### 设置索引

方法1

```
var animalSchema = new Schema({
  name: String,
  type: String,
  tags: { type: [String], index: true } 
});
```

方法2

```
animalSchema.index({ name: 1, type: -1 });
```

> 1 表示正序, -1 表示逆序

## methods

### 定义

```
// 定义一个schema
var freshSchema = new Schema({ name: String, type: String });

// 添加一个fn. 
animalSchema.methods.findSimilarTypes = function (cb) {
  //这里的this指的是具体document上的this
  //this.model 返回Model对象
  return this.model ('Animal').find({ type: this.type }, cb);
}
```

### 使用

```
var Animal = mongoose.model('Animal', animalSchema);
var dog = new Animal({ type: 'dog' });
```

### 静态方法

```
// 给model添加一个findByName方法
animalSchema.statics.findByName = function (name, cb) {
  //这里的this 指的就是Model
  return this.find({ name: new RegExp(name, 'i') }, cb);
}

var Animal = mongoose.model('Animal', animalSchema);
Animal.findByName('fido', function (err, animals) {
  console.log(animals);
});
```

## 虚拟属性

```
//schema 添加虚拟属性
personSchema.virtual('fullName').get(function(){
    return this.first+" "+this.last;
})
//调用
bad.fullName;
```

上面的代码和下面的代码效果相同

```
//schema基本内容
var personSchema = new Schema({
  name: {
    first: String,
    last: String
  }
});

// 生成Model
var Person = mongoose.model('Person', personSchema);

//现在我们有个需求,即,需要将first和last结合输出.
//一种方法是,使用methods来实现
//schema 添加方法
personSchema.methods.getName = function(){
    return this.first+" "+this.last;
}

// 生成一个doc
var bad = new Person({
    name: { first: 'jimmy', last: 'Gay' }
});

//调用
bad.getName();
```

> 该属性是直接设置在Schema上的. 但是,需要注意的是,VR 并不会真正的存放在db中. 他只是一个提取数据的方法

## Model

model的创建实际上就是方法的copy. 将schema上的方法,copy到model上. 只是copy的位置不一样, 一部分在prototype上, 一部分在constructor中

```
var schema = new mongoose.Schema({ name: 'string', size: 'string' });
var Tank = mongoose.model('Tank', schema);
```

> 这里,我们一定要搞清楚一个东西. 实际上, mongoose.model里面定义的第一个参数,比如’Tank’, 并不是数据库中的, collection. 他只是collection的单数形式, 实际上在db中的collection是’Tanks’

## model 的子文档操作

mongoose提供了children字段. 让我们能够轻松的在表间建立关系

```
var childSchema = new Schema({ name: 'string' });

var parentSchema = new Schema({
  children: [childSchema]   //指明sub-doc的schema
});
//在创建中指明doc
var Parent = mongoose.model('Parent', parentSchema);
var parent = new Parent({ children: [{ name: 'Matt' }, { name: 'Sarah' }] })
parent.children[0].name = 'Matthew';
parent.save(callback);
```

现在, 我们就已经创建了3个table. 一个parent 包含了 两个child 另外,如果我们想要查询指定的doc。 则可以使用 id()方法

```
var doc = parent.children.id(id);
```

子文档的CRUD, 实际上就是数组的操作, 比如push,unshift,remove,pop,shift等

```
parent.children.push({ name: 'Liesl' });
```

mongoose还给移除提供了另外一个方法–remove

```
var doc = parent.children.id(id).remove();
```

> 如果你忘记添加子文档的话，可以在外围添加, 但是字段必须在Schema中指定
> `var newdoc = parent.children.create({ name: 'Aaron' });`

## document

### 创建

使用实例创建

```
var Tank = mongoose.model('Tank', yourSchema);
var small = new Tank({ size: 'small' });
small.save(function (err) {
  if (err) return handleError(err);
  // saved!
})
```

使用类直接创建

```
var Tank = mongoose.model('Tank', yourSchema);
Tank.create({ size: 'small' }, function (err, small) {
  if (err) return handleError(err);
  // saved!
})
```

### 查询

方式1

callback: 使用回调函数, 即, query会立即执行,然后返回到回调函数中

```
Person.findOne({ 'name.last': 'Ghost' }, 'name occupation', function (err, person) {
  if (err) return handleError(err);
  // get data
})
```

query: 使用查询方法,返回的是一个Query对象. 该对象是一个Promise, 所以可以使用 chain 进行调用.最后必须使用exec(cb)传入回调进行处理. cb 是一个套路, 第一个参数永远是err. 第二个就是返回的数据

```
Tank.find({ size: 'small' }).where('createdDate').gt(oneYearAgo).exec(callback);
```

下面是两种等价的写法

```
// With a JSON doc
Person.
  find({
    occupation: /host/,
    'name.last': 'Ghost',
    age: { $gt: 17, $lt: 66 },
    likes: { $in: ['vaporizing', 'talking'] }
  }).
  limit(10).
  sort({ occupation: -1 }).
  select({ name: 1, occupation: 1 }).
  exec(callback);
  
// Using query builder
Person.
  find({ occupation: /host/ }).
  where('name.last').equals('Ghost').
  where('age').gt(17).lt(66).
  where('likes').in(['vaporizing', 'talking']).
  limit(10).
  sort('-occupation').
  select('name occupation').
  exec(callback);
```

Query Helpers

添加 query helper functions,跟定义在Schema实例方法一样，但是返回query对象作为mongoose queries使用（说句白了就是封装mongoose查询方法）

```
animalSchema.query.byName = function(name) {
  return this.find({ name: new RegExp(name, 'i') });
};

var Animal = mongoose.model('Animal', animalSchema);
Animal.find().byName('fido').exec(function(err, animals) {
  console.log(animals);
});
```

### 删除

reomve操作仅在通过回调时执行。 要强制执行没有回调，您必须先调用remove（），然后使用exec（）方法执行它。
我们可以在document上执行remove方法也可以在Model上。

```
Model.find().remove({ name: 'Anne Murray' }, callback)
Model.remove({ name: 'Anne Murray' }, callback)
//没有添加回调情况
Model.find().remove({ name: 'Anne Murray' }).remove(callback)
Model.remove({ name: 'Anne Murray' }).exce(callback)
```

### 更新

使用Model.update([(conditions, doc, [options], [callback])]
不返回更新对象到应用程序。如果要更新数据库中的单个文档并将其返回到应用程序，请改用findOneAndUpdate

参数

* **conditions** 就是query. 通过query获取到指定doc
* **doc** 就是用来替换doc内容的值.
* **options** 这块需要说一些下.
    * **safe** (boolean) 是否开启安全模式 (default for true)
    * **upsert** (boolean) 如果没有匹配到内容,是否自动创建 ( default for false)
    * **multi** (boolean) 如果有多个doc,匹配到,是否一起更改 ( default for false)
    * **overwrite** (boolean) 匹配到指定doc,是否覆盖 (default for false)
    * **runValidators** (boolean) 表示是否用来启用验证. 实际上,你首先需要写一个验证. 关于如果书写,验证大家可以参考下文, validate篇(default for false)
    * **new**（使用findOneAndUpdate时才有参数）：bool - 如果为true，则返回修改后的文档而不是原始文件。 默认为false
    
```
Model.update({age:18}, { $set: { name: 'jason borne' }}, {multi:true}, function (err, raw) {
  if (err) return handleError(err);
  console.log('raw 就是mongodb返回的更改状态的falg ', raw);
  //比如: { ok: 1, nModified: 2, n: 2 }
});
```
# 注意事项

数据库名可以是满足以下条件的任意UTF-8字符串

* 不能是空字符串（"")
* 不得含有' '（空格)、.、$、/、\和\0 (空字符)
* 应全部小写
* 最多64字节

有一些数据库名是保留的，可以直接访问这些有特殊作用的数据库

* **admin** 从权限的角度来看，这是"root"数据库。要是将一个用户添加到这个数据库，这个用户自动继承所有数据库的权限。一些特定的服务器端命令也只能从这个数据库运行，比如列出所有的数据库或者关闭服务器。
* **local** 这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合
* **config** 当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息。

文档中的键/值对是有序的

文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)

MongoDB区分类型和大小写

MongoDB的文档不能有重复的键

文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符

文档键命名规范：

* 键不能含有\0 (空字符)。这个字符用来表示键的结尾
* .和$有特别的意义，只有在特定环境下才能使用
* 以下划线"_"开头的键是保留的(不是严格要求的)

合法的集合名

* 集合名不能是空字符串""
* 集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾
* 集合名不能以"system."开头，这是为系统集合保留的前缀
* 用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$

