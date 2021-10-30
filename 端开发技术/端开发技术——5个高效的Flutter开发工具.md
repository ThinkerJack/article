![](https://img-blog.csdnimg.cn/38fbbdcb183a4cb4b51ed03edc91a9fe.png)
# 1. 你是否需要更好，更简洁的日志?

![](https://img-blog.csdnimg.cn/img_convert/186815b8d09ed942c4681ec86cad60c4.png)

当你在开发Flutter应用程序时，难以理解的日志是一个大问题，因为没有快速的方法来根据问题的严重程度过滤你的日志。抛出异常或记录一条简单的调试消息?他们看起来都一样。

如果你的Flutter app需要更好的日志系统，**Logger** 软件包绝对是个好东西。

**Logger**包地址：https://pub.dev/packages/logger

它受到Java分级日志的启发，允许您向日志添加级别。

日志级别，目前有：

```dart
logger.v("Add more detailed debug messages, "
    "can contain sensitive information, never enable it in production");

logger.d("Fine grained information to debug an application");

logger.i("Track the flow of the application");

logger.w("A potential but expected problem");

logger.e("A real failure that may impact the application state");
```

由于某些原因，另外一个特别的是

```dart
logger.wtf("WTF logs??")
```

[![DDnGHx.png](https://img-blog.csdnimg.cn/img_convert/ecf2ee03a4ea398566fee3948f15e503.png)](https://imgchr.com/i/DDnGHx)
不仅如此，你还可以晃动你的设备来查看屏幕上的日志。(PS：需要导入[logger_flutter](https://pub.dev/packages/logger_flutter)包)

# ![](https://img-blog.csdnimg.cn/img_convert/186815b8d09ed942c4681ec86cad60c4.png)2. API还没有从后端准备好，或者根本没有API ?应用程序靠自己硬编数据?

如果你还在艰难的coding,全是自己硬编数据因为后台没有准备好他们的API或者根本没有任何API,如果你仍然希望UI有意义,您可以使用**faker**包——Jesper Hakansson为应用程序生成有意义的数据。

受Python包faker和Ruby包ffaker的启发，这个包可以提供各种类型的数据，从虚假的人名到虚假的日期，甚至是随机的虚假url。

只需创建一个简单的对象，像这样-

```dart
var faker = new Faker();
```

下面是使用faker对象的例子

```dart
faker.date.month();
faker.conference.name();
faker.company.position();
faker.lorem.sentences(8);
faker.internet.httpsUrl();
faker.currency.name();
faker.sport.name()
```

在这个包下还有更多种类的数据可用，这是自己硬编数据的一个很好的替代品，当项目变得更复杂时，自己硬编数据是很难替换的。

**faker**包地址：https://pub.dev/packages/faker/example

![](https://img-blog.csdnimg.cn/img_convert/f946a78619c9b1dcaee29c33f2b114a8.png)

# 3. 当API返回的数据结构复杂，你需要快速构建model?

虽然我在2018年已经分享过这篇解析复杂JSON的文章，在今天它仍然非常流行。

https://medium.com/flutter-community/parsing-complex-json-in-flutter-747c46655f51

值得一提的是，这篇文章是对Dart解析json的一个很好的理论回顾，但我不建议在构建实际复杂项目时进行手动解析。

为什么不建议?

.手动操作肯定要花很长时间。

.而且你更容易犯错误。

我更建议使用转换器工具或解析器，与手动解析相比，它只需几秒钟就能完成。

当涉及到JSON序列化时，你可以在Flutter文档中找到一些推荐的方法。

当然，推荐之一是代码生成库，它将为您生成编码样板。但这仍然需要一些初始设置，而我并不喜欢。

所以，我的首选工具一直是[quicktype.io](https://app.quicktype.io/)。一群开源开发者维护的在线工具。

只需进入网站，选择Dart作为输出语言。

将JSON粘贴到左侧，Dart model类和JSON序列化逻辑将很快在右侧创建。

添加这个类到你的flutter项目，你就可以使用了。

![](https://img-blog.csdnimg.cn/img_convert/794f5af83f17a9d3084252d3dc9746f8.gif)

![](https://img-blog.csdnimg.cn/img_convert/7f252c2d956d5dfc0146670cccc3dbc9.png)

# 4. 从一个运行着的模拟器/设备预览你的应用程序

作为一名Android开发人员，仅仅为不同的屏幕大小创建xml就需要花费好几天的时间，因为Android设备有不同的形状和大小，而且重要的是你需要让你的应用程序在不同的设备上表现一致。iOS开发人员的情况也没有什么不同，苹果公司的iPhone屏幕大小不一。有时，我们还必须支持平板电脑或iPad设备。

这是否意味着，我需要下载大量的模拟器或为我的团队购买不同的手机，以便在不同的设备上测试我们的应用的UI ?

去年，在Flutter interactive 2019, Zoey Fan和Chris Sells谈到了Flutter Octopus，在那里你可以同时在多个平台和设备调试你的应用程序。

![](https://img-blog.csdnimg.cn/img_convert/a875bb12cfeeed8c61d5494050b745a5.png)

这对于观察你的应用在不同设备上的性能是很有用的。但是你真的会设置这么多设备仅仅用来来检查UI的响应性吗?

![](https://img-blog.csdnimg.cn/img_convert/e7885332823c6035a767ddbce52f1660.gif)

我不这么想

来挽救我们的的是Alois Daniel的Flutter Device Preview。 超好用的工具，可让您从单个运行的模拟器/设备上预览不同大小的设备中的应用程序。

![](https://img-blog.csdnimg.cn/img_convert/669ad80bee89d69d9bc5e7be7582e510.gif)

轻松预览在不同的屏幕大小和平台的应用程序，从普通的手机大小到平板电脑，甚至手表屏幕大小。这是检查你的应用程序有没有溢出的好方法。不仅如此，还有其他很酷的功能

★改变你的应用程序的方向，并预览你的应用程序在不同方向上的响应能力。

★更新配置，如文本缩放因子，应用的主题，地区

★能够进行截图，便于你分享给你的团队。

所有这些，不影响应用程序的状态!

**device_preview** 包地址：https://pub.dev/packages/device_preview

# 5. 使用测试版本学习,使用稳定版本工作

如果你使用Flutter中构建应用程序，你很有可能使用稳定的Flutter版本来开发和部署你的应用程序。谁会冒险在一个实验性的flutter版本上开发一个客户项目，对吗?

![](https://img-blog.csdnimg.cn/img_convert/8852caf6a5508863d83610f65a939f6e.gif)

但是，你是一个爱尝试的的开发人员，你在你的客户或公司项目之外创建项目，你很想尝试新的beta版本，并尝试使用新特性。

但这就意味着，卸载当前的稳定版，再安装测试版，又要花费大量的时间去下载新版本的资源。

而当你重新在客户项目上工作时，你将不得不卸载测试版，并重新安装稳定版。

![](https://img-blog.csdnimg.cn/img_convert/a61e65d55937b359f6fa6426cb6a168b.gif)
无奈

所以，另一个来拯救你的工具 — **Flutter Version Manager by Leo Farias.**

您可以使用这个工具来管理多个flutter版本，而不必每次在你切换的时候下载这些版本。这只是一个一次性的设置，你一次下载所有的版本像这样-

```
fvm install beta
```


或者指定的版本

```
 fvm install <version>
```

只需一条命令就可以在不同版本之间切换，就像这样

```
fvm use stable
```

你可以为你的每个项目指定一个flutter版本。

```
cd Documents/FlutterProjects/ExperimentalProject
fvm use beta
```

or

```
cd Documents/FlutterProjects/ClientProject
fvm use stable
```

在你安装fvm之后唯一改变的是你所有的命令都会稍微修改一下。

就像 `flutter doctor` , 变成`fvm flutter doctor`

这是很容易记住的。

**FVM**包地址：https://pub.dev/packages/fvm


