# 模型（Models）

模型（`Models`）的构造函数是编译我们定义的`Schema`。这些模型（`models`）实例代表可以从我们的数据库中保存和检索文档。所有文档在数据库中的创建与检索都是通过这些模型（`models`）处理。

## 编译你的第一个模型（Model）

```js
var schema = new mongoose.Schema({ name: 'string', size: 'string' });
var Tank = mongoose.model('Tank', schema);
```

第一个参数是你的模型在集合中唯一的名称。Mongoose自动搜索你的模型名称的多个版本。因此，对于上面的例子，模型Tank是用于数据库中的Tanks集合。创建了一个`schema`副本`.model()`函数。确保`schema`在调用`.model()`之前添加了所有你想要的东西。

## 构建文档（Constructing Documents）



