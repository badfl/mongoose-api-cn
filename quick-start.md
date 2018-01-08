# 入门

首先确定你已经安装了Mongodb和Node.js

接下来使用命令行安装Mongoose npm

```
$ npm install mongoose
```

首先需要在你的项目中引入mongoose，然后在我们本地运行MongoDB打开连接到test数据库。

```js
// getting-started.js
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');
```

我们有一个在本地主机运行的挂起连接的test数据库，我们连接成功或发生连接错误需要得到一个通知。

```js
var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  // we're connected!
});
```

一旦我们的连接打开，我们的回调将被调用。为简洁起见，我们假设**以下所有代码都位于此回调中**。

在Mongoose中，一切都是从Schema衍生的，让我们来参考它，并定义我们的kitten。

```js
var kittySchema = mongoose.Schema({
    name: String
});
```

到目前为止还不错，我们新建了一个Schema属性name，这是一个String类型。下一步将我们的Schema编译成Model

```js
var Kitten = mongoose.model('Kitten', kittySchema);
```

model是我们构造文件中的一个类。在这种情况下，每个文档将是一个kitten，在schema中声明一个属性和行为。让我们创建一个kitten文档，代表我们在外面人行道上遇到的小家伙儿。

```js
var silence = new Kitten({ name: 'Silence' });
console.log(silence.name); // 'Silence'
```

小猫（kitten）可以喵喵叫，那么让我们来看看如何为我们的文档添加“说（speak）”功能：

```
// NOTE: methods must be added to the schema before compiling it with mongoose.model()
kittySchema.methods.speak = function () {
  var greeting = this.name
    ? "Meow name is " + this.name
    : "I don't have a name";
  console.log(greeting);
}

var Kitten = mongoose.model('Kitten', kittySchema);
```

方法被添加到methods的原型上，编译成模型原型并在每个文档实例中公开：

```
var fluffy = new Kitten({ name: 'fluffy' });
fluffy.speak(); // "Meow name is fluffy"
```

我们有个会说话的小猫（Kitten）！但是我们没有保存任何东西给MongoDB。每个文档可以通过调用其save方法保存到数据库中，如果发生错误或者任何问题第一个参数将会回调。

```
fluffy.save(function (err, fluffy) {
  if (err) return console.error(err);
  fluffy.speak();
});
```

说完以后我们想要看到所有的小猫（kittens）

