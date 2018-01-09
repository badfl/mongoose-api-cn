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

每个键（key）在我们的blogSchema的文档中定义了一个属性，这些属性将被转换成`Schema Type`。

