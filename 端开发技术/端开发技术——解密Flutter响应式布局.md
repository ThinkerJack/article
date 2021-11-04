![](https://img-blog.csdnimg.cn/38fbbdcb183a4cb4b51ed03edc91a9fe.png)![](https://img-blog.csdnimg.cn/20201206225556843.png)

Flutter是一个跨平台的应用开发框架，支持各种屏幕大小的设备，它可以在智能手表这样的小设备上运行，也可以在电视这样的大设备上运行。使用相同的代码来适应不同的屏幕大小和像素密度是一个挑战。

Flutter响应式布局的设计没有硬性的规则。在本文中，我将向您展示在设计响应式布局时可以遵循的一些方法。

在使用Flutter构建响应式布局之前，我想说明一下Android和iOS是如何处理不同屏幕大小的布局的。

# 1. Android的方法

为了处理不同的屏幕尺寸和像素密度，在Android中使用了以下概念:

## 1.1 ConstraintLayout

Android UI设计中引入的一个革命性的东西是ConstraintLayout。它可以用于创建灵活的、响应性强的UI设计，以适应不同的屏幕大小和尺寸。它允许您根据与布局中其他视图的空间关系来指定每个视图的位置和大小。

但这并不能解决大型设备的问题，在大型设备中，拉伸或只是调整UI组件的大小并不是利用屏幕面积的最优雅的方式。在屏幕面积很小的智能手表，调整组件以适应屏幕大小可能会导致奇怪的UI。

## 1.2 Alternative layouts

要解决上述问题，您可以为不同大小的设备使用alternative layouts。例如，你可以在平板电脑等设备上使用分屏视图来提供良好的用户体验，并明智地使用大屏幕。

![Image for post](https://img-blog.csdnimg.cn/20201206225556980.png)

在Android中，你可以为不同的屏幕大小定义不同的布局文件，Android框架会根据设备的屏幕大小自动处理这些布局之间的切换。

## 1.3 Fragments

使用Fragment，你可以将你的UI逻辑提取到单独的组件中，这样当你为大屏幕尺寸设计多窗格布局时，你不必单独定义逻辑。您可以重用为每个片段定义的Fragment。

## 1.4 Vector graphics

Vector graphics使用XML创建图像来定义路径和颜色，而不是使用像素位图。它可以缩放到任何大小。在Android中，你可以使用VectorDrawable来绘制任何类型的插图，比如图标。

# 2. iOS的方法

iOS用于定义响应式布局的方式如下

## 2.1 Auto Layout

Auto Layout可用于构建自适应界面，您可以在其中定义用于控制应用程序内容的规则（称为约束）。 当检测到某些环境变化（称为特征）时，“Auto Layout”会根据指定的约束条件自动重新调整布局。

## 2.2 Size classes

Size类的特点是会根据其大小自动分配给内容区域。 iOS 会根据内容区域的Size类别动态地进行布局调整。在iPad上，size类也适用。

## 2.3 一些UI 组件

还有一些其他的UI嘴贱你可以用来在iOS上构建响应式UI，像UIStackView, UIViewController，和UISplitViewController。

# 3. Flutter是如何自适应的

即使你不是Android或iOS的开发者，到目前为止，你应该已经了解了这些平台是如何处理响应式布局的。

在Android中，要在单个屏幕上显示多个UI视图，请使用Fragments，它们类似于可在应用程序的Activity中运行的可重用组件。

*您可以在一个Activity中运行多个Fragment，但是不能在一个应用程序中同时运行多个Activity。*

在iOS中，为了控制多个视图控制器，使用了UISplitViewController，它在分层界面中管理子视图控制器。

现在我们来到Flutter

Flutter引入了widget的概念。它们像积木一样拼凑在一起构建应用程序画面。

*记住，在Flutter中，每个屏幕和整个应用程序也是一个widget!*

widget本质上是可重用的，因此在Flutter中构建响应式布局时，您不需要学习任何其他概念。

## 3.1 Flutter的响应式概念

正如我前面所说的，我将讨论开发响应式布局所需的重要概念，然后你来选择使用什么样的方式在你的APP上实现响应式布局。

### 3.1.1 MediaQuery

你可以使用MediaQuery来检索屏幕的大小(宽度/高度)和方向(纵向/横向)。

下面是例子

```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Size screenSize = MediaQuery.of(context).size;
    Orientation orientation = MediaQuery.of(context).orientation;

    return Scaffold(
      body: Container(
        color: CustomColors.android,
        child: Center(
          child: Text(
            'View\n\n' +
                '[MediaQuery width]: ${screenSize.width.toStringAsFixed(2)}\n\n' +
                '[MediaQuery orientation]: $orientation',
            style: TextStyle(color: Colors.white, fontSize: 18),
          ),
        ),
      ),
    );
  }
}
```

![Image for post](https://img-blog.csdnimg.cn/20201206225557120.png)

### 3.1.2 LayoutBuilder

使用LayoutBuilder类，您可以获得BoxConstraints对象，该对象可用于确定小部件的maxWidth和maxHeight。

*请记住:MediaQuery和LayoutBuilder之间的主要区别在于，MediaQuery使用屏幕的完整上下文，而不仅仅是特定小部件的大小。而LayoutBuilder可以确定特定小部件的最大宽度和高度。*

下面是例子

```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Size screenSize = MediaQuery.of(context).size;

    return Scaffold(
      body: Row(
        children: [
          Expanded(
            flex: 2,
            child: LayoutBuilder(
              builder: (context, constraints) => Container(
                color: CustomColors.android,
                child: Center(
                  child: Text(
                    'View 1\n\n' +
                        '[MediaQuery]:\n ${screenSize.width.toStringAsFixed(2)}\n\n' +
                        '[LayoutBuilder]:\n${constraints.maxWidth.toStringAsFixed(2)}',
                    style: TextStyle(color: Colors.white, fontSize: 18),
                  ),
                ),
              ),
            ),
          ),
          Expanded(
            flex: 3,
            child: LayoutBuilder(
              builder: (context, constraints) => Container(
                color: Colors.white,
                child: Center(
                  child: Text(
                    'View 2\n\n' +
                        '[MediaQuery]:\n ${screenSize.width.toStringAsFixed(2)}\n\n' +
                        '[LayoutBuilder]:\n${constraints.maxWidth.toStringAsFixed(2)}',
                    style: TextStyle(color: CustomColors.android, fontSize: 18),
                  ),
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

![Image for post](https://img-blog.csdnimg.cn/20201206225557248.png)
PS:当你在构建一个小部件，想知道他的宽度是多少时，使用这个组件，你可以根据子组件可用高/宽度来进行判断，构建不同的布局

### 3.1.3 OrientationBuilder

要确定widget的当前方向，可以使用OrientationBuilder类。

*记住:这与你使用MediaQuery检索的设备方向不同。*

下面是例子

```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Orientation deviceOrientation = MediaQuery.of(context).orientation;

    return Scaffold(
      body: Column(
        children: [
          Expanded(
            flex: 2,
            child: Container(
              color: CustomColors.android,
              child: OrientationBuilder(
                builder: (context, orientation) => Center(
                  child: Text(
                    'View 1\n\n' +
                        '[MediaQuery orientation]:\n$deviceOrientation\n\n' +
                        '[OrientationBuilder]:\n$orientation',
                    style: TextStyle(color: Colors.white, fontSize: 18),
                  ),
                ),
              ),
            ),
          ),
          Expanded(
            flex: 3,
            child: OrientationBuilder(
              builder: (context, orientation) => Container(
                color: Colors.white,
                child: Center(
                  child: Text(
                    'View 2\n\n' +
                        '[MediaQuery orientation]:\n$deviceOrientation\n\n' +
                        '[OrientationBuilder]:\n$orientation',
                    style: TextStyle(color: CustomColors.android, fontSize: 18),
                  ),
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

![Image for post](https://img-blog.csdnimg.cn/20201206225557407.png)

portrait (纵向) landscape（横向）

PS：看了下OrientationBuilder的源码注释

widget的方向仅仅是其宽度相对于高度的一个系数。如果一个[Column]部件的宽度超过了它的高度，它的方向是横向的，即使它以垂直的形式显示其子元素。

这是译者的代码

```
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

/// Copyright (C), 2020-2020, flutter_demo
/// FileName: orientationBuilder_demo
/// Author: Jack
/// Date: 2020/12/6
/// Description:

class OrientationBuilderDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Orientation deviceOrientation = MediaQuery.of(context).orientation;

    return Scaffold(
      body: Column(
        children: [

          Expanded(
            flex: 1,
            child: Container(
              color: Colors.greenAccent,
              child: OrientationBuilder(
                builder: (context, orientation) => Center(
                  child: Text(
                    'View 1\n\n' +
                        '[MediaQuery orientation]:\n$deviceOrientation\n\n' +
                        '[OrientationBuilder]:\n$orientation',
                    style: TextStyle(color: Colors.white, fontSize: 18),
                  ),
                ),
              ),
            ),
          ),
          Expanded(
            flex: 2,
            child: OrientationBuilder(
              builder: (context, orientation) => Container(
                color: Colors.white,
                child: Center(
                  child: Text(
                    'View 2\n\n' +
                        '[MediaQuery orientation]:\n$deviceOrientation\n\n' +
                        '[OrientationBuilder]:\n$orientation',
                    style: TextStyle(color: Colors.greenAccent, fontSize: 18),
                  ),
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201206225557549.png)

想必你已经理解了OrientationBuilder的方向定义，如果一个小部件的宽大于高，他就是横向的，如果高大于宽，他就是横向的，仅此而已。

### 3.1.4 Expanded and Flexible

在Row或Column中特别有用的小部件是 Expanded 和 Flexible。当Expanded 使用在一个Row、Column或Flex中，Expanded 可以使它的子Widget自动填充可用空间，与之相反，Flexible 的子widget不会填满整个可用空间。

例子如下。

```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: SafeArea(
        child: Column(
          children: [
            Row(
              children: [
                ExpandedWidget(),
                FlexibleWidget(),
              ],
            ),
            Row(
              children: [
                ExpandedWidget(),
                ExpandedWidget(),
              ],
            ),
            Row(
              children: [
                FlexibleWidget(),
                FlexibleWidget(),
              ],
            ),
            Row(
              children: [
                FlexibleWidget(),
                ExpandedWidget(),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

class ExpandedWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Expanded(
      child: Container(
        decoration: BoxDecoration(
          color: CustomColors.android,
          border: Border.all(color: Colors.white),
        ),
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Text(
            'Expanded',
            style: TextStyle(color: Colors.white, fontSize: 24),
          ),
        ),
      ),
    );
  }
}

class FlexibleWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Flexible(
      child: Container(
        decoration: BoxDecoration(
          color: CustomColors.androidAccent,
          border: Border.all(color: Colors.white),
        ),
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Text(
            'Flexible',
            style: TextStyle(color: CustomColors.android, fontSize: 24),
          ),
        ),
      ),
    );
  }
}
```



![Image for post](https://img-blog.csdnimg.cn/20201206225557662.png)

PS:与[expand]不同的是，[Flexible]不需要子widget填充剩余的空间，第一个例子，expanded虽然有填充空余空间的功能，不过expanded组件和flexible组件的flex都是1,相当于将纵轴分成两半，expanded所拥有的全部空间就是纵轴的一半，实际他已经填充了。

### 3.1.5 FractionallySizedBox

FractionallySizedBox widget将其子元素的大小调整为可用空间的一小部分。它在Expanded 或Flexible  widget中特别有用。



```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: SafeArea(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          children: [
            Row(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                FractionallySizedWidget(widthFactor: 0.4),
              ],
            ),
            Row(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                FractionallySizedWidget(widthFactor: 0.6),
              ],
            ),
            Row(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                FractionallySizedWidget(widthFactor: 0.8),
              ],
            ),
            Row(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                FractionallySizedWidget(widthFactor: 1.0),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

class FractionallySizedWidget extends StatelessWidget {
  final double widthFactor;
  FractionallySizedWidget({@required this.widthFactor});

  @override
  Widget build(BuildContext context) {
    return Expanded(
      child: FractionallySizedBox(
        alignment: Alignment.centerLeft,
        widthFactor: widthFactor,
        child: Container(
          decoration: BoxDecoration(
            color: CustomColors.android,
            border: Border.all(color: Colors.white),
          ),
          child: Padding(
            padding: const EdgeInsets.all(16.0),
            child: Text(
              '${widthFactor * 100}%',
              style: TextStyle(color: Colors.white, fontSize: 24),
            ),
          ),
        ),
      ),
    );
  }
}
```

PS:当你想让你的widget，占据当前屏幕宽度和高度的百分之多少时，使用这个组件，想在Row和Column组件中使用百分比布局时，需要在FractionallySizedBox外包裹一个expanded或flexible

### 3.1.6 AspectRatio

可以使用AspectRatio小部件将子元素的大小调整为特定的长宽比。首先，它尝试布局约束允许的最大宽度，并通过将给定的高宽比应用于宽度来决定高度。

```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: SafeArea(
        child: Column(
          children: [
            AspectRatioWidget(ratio: '16 / 9'),
            AspectRatioWidget(ratio: '3 / 2'),
          ],
        ),
      ),
    );
  }
}

class AspectRatioWidget extends StatelessWidget {
  final String ratio;

  AspectRatioWidget({@required this.ratio});

  @override
  Widget build(BuildContext context) {
    return AspectRatio(
      aspectRatio: Fraction.fromString(ratio).toDouble(),
      child: Container(
        decoration: BoxDecoration(
          color: CustomColors.android,
          border: Border.all(color: Colors.white),
        ),
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Center(
            child: Text(
              'AspectRatio - $ratio',
              style: TextStyle(color: Colors.white, fontSize: 24),
            ),
          ),
        ),
      ),
    );
  }
}
```

![Image for post](https://img-blog.csdnimg.cn/20201206225557772.png)

我们已经研究了大多数重要的概念，为建立一个响应式布局Flutter app，除了最后一个。

在构建一个示例响应式应用程序时，让我们学习最后一个概念。

## 3.2 创建一个响应式APP

现在，我们将应用上一节中描述的一些概念。与此同时，您还将学习为大屏幕构建布局的另一个重要概念，即分屏视图(一个屏幕上显示多个页面)。

响应式布局：在不同大小的屏幕上使用不同的布局。
我们将建立一个名叫Flow的聊天应用程序。

app主要由两个部分组成:

- **HomePage** (`PeopleView`, `BookmarkView`, `ContactView`)

- **ChatPage** (`PeopleView`, `ChatView`)![在这里插入图片描述](https://img-blog.csdnimg.cn/20201206225557953.png)

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201206225558317.png)

对于大屏幕，我们将显示包含MenuWidget和DestinationView的分屏视图。您可以看到，在Flutter中创建分屏视图是非常容易的，您只需使用一行将它们并排放置，然后为了填满整个空间，只需使用Expanded widget包装两个视图。您还可以定义扩展小部件的flex属性，这将允许您指定每个小部件应该覆盖屏幕的多少部分(默认flex设置为1)。

但是，如果您现在移动到一个特定的屏幕，然后在视图之间切换，那么您将丢失页面的上下文，也就是说您将始终返回到第一个页面，即“聊天”。为了解决这个问题，我使用了多个回调函数来返回所选页面到主页。实际上，您应该使用状态管理技术来处理此场景。由于本文的唯一目的是教您构建响应式布局，所以我不讨论任何状态管理的复杂性。

![](https://img-blog.csdnimg.cn/c66cc07b674c424ba11ec6825e22a640.png)

![](https://img-blog.csdnimg.cn/46f9ed15f914479ab130d47e9578e721.png)
