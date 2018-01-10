# Schemas

> 如果你还没有开始，请花一分钟时间阅读快速开始，了解Mongoose是如何工作的。如果你是从3.x迁移到4.x，请花点时间阅读一下迁移指南

## 定义你的Schema

Mongoose中所有的东西都是以Schema开始。每个Schema映射到一个MongoDB集合（collection），并定义该集合（collection）中文档的形式。

```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var blogSchema = new Schema({
  title:  String,
  author: String,
  body:   String,
  comments: [{ body: String, date: Date }],
  date: { type: Date, default: Date.now },
  hidden: Boolean,
  meta: {
    votes: Number,
    favs:  Number
  }
});
```

_如果你稍后想添加额外的键（keys），使用Schema\#add方法_

每个键（key）在我们的blogSchema的文档中定义了一个属性，这些属性将被转换成`SchemaType`。例如，我们定义了一个`title`将被转换为`String`类型的`SchemaType`，定义的`date`并将其转换成`Date`类型的`SchemaType`。键（`keys`）也可以指定成对象（`object`）包含更多键/属性（key/type）（例如上面的“`meta`”属性）。

允许使用的`SchemaTypes`有：

* **String**
* **Number**
* **Date**
* **Buffer**
* **Boolean**
* **Mixed**
* **ObjectId**
* **Array**

阅读更多关于它们 [点击这里](/guide/schemas/types.md)

Schemas不仅定义了文档与属性的结构，还定义了文档的实例方法（instance methods），静态模型方法（static Model methods），复合索引（compound indexes）和文档生命周期钩子回调中间件。

## 创建一个模型（Model）

要使用我们的`schema`定义，需要转换之前定义的`blogSchema`成为我们可以使用的模型（`Model`），因此，我们通过`mongoose.model(modelName,schema);`

```js
var Blog = mongoose.model('Blog', blogSchema);
// ready to go!
```

## 实例方法（Instance Methods）

























