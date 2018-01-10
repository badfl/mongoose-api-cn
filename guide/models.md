# 模型（Models）

模型（`Models`）的构造函数是编译我们定义的`Schema`。这些模型（`models`）实例代表可以从我们的数据库中保存和检索文档。所有文档在数据库中的创建与检索都是通过这些模型（`models`）处理。

## 编译你的第一个模型（Model）

```js
var schema = new mongoose.Schema({ name: 'string', size: 'string' });
var Tank = mongoose.model('Tank', schema);
```

第一个参数是你的模型在集合中唯一的名称。Mongoose自动搜索你的模型名称的多个版本。因此，对于上面的例子，模型Tank是用于数据库中的Tanks集合。创建了一个`schema`副本`.model()`函数。确保`schema`在调用`.model()`之前添加了所有你想要的东西。

## 构建文档（Constructing Documents）

文档是我们的模型实例，创建它们并保存到数据库非常简单：

```js
var Tank = mongoose.model('Tank', yourSchema);

var small = new Tank({ size: 'small' });
small.save(function (err) {
  if (err) return handleError(err);
  // saved!
})

// or

Tank.create({ size: 'small' }, function (err, small) {
  if (err) return handleError(err);
  // saved!
})
```

请注意除非你创建的模型（`Model`）连接打开否则不会创建/移除tank。每个模型（`Model`）都有个相应的链接。当你使用`mongoose.model()`，你的模型（`Model`）将使用`mongoose`默认连接。

```js
mongoose.connect('localhost', 'gettingstarted');
```

如果您创建自定义链接，请使用`connection.model()`方法创建。

```js
var connection = mongoose.createConnection('mongodb://localhost:27017/test');
var Tank = connection.model('Tank', yourSchema);
```

## 查询（Querying）























