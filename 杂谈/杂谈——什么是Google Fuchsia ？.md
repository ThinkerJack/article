![](https://img-blog.csdnimg.cn/1006d68dd9bc42b2af325cc49eb1e06b.png)Google正在开发一个新的操作系统：借助Fuchsia OS，该技术小组放弃了Linux体系结构，转而依靠**自行开发的微内核Zircon**。Fuchsia 不仅可以替代台式机操作系统Chrome操作系统，而且可以替代专为移动设备设计的Android。尽管事实上，Android在当今市场上几乎是无与伦比的。

Google Fuchsia是未来的操作系统吗？我们仔细研究了该项目。

## 什么是Google Fuchsia ？

Fuchsia 不仅是红色和蓝色之间的一种颜色，还是Google自2016年以来一直在公众面前开发的模块化，基于权限的**实时操作系统**的名称。该系统使用C，C ++， Dart，Go和Rust，并在现代64位Intel ARM处理器上运行。

事实

实时操作系统（RTOS）是一种能够响应事件并立即或在预定时间内提供处理结果的操作系统。

Fuchsia OS的源代码已获得**开源许可证**（包括BSD，MIT和Apache许可证），并且可以由Google公共[Git存储库中的](https://fuchsia.googlesource.com/?format=HTML)任何人查看和下载。这是有关该项目的综合[文档](https://fuchsia.googlesource.com/fuchsia/+/refs/heads/master/docs/)。

根据文档，Fuchsia OS同样适用于智能手机，平板电脑，笔记本电脑和台式计算机。自2017年5月起，**Armadillo**已成为具有图形用户界面的触摸优化用户界面（UI）。谷歌正在为Fuchsia OS开发一个桌面UI，标题为**Capybara**。从那以后，有传言称Google正在努力替代几乎无与伦比的Android。

## Fuchsia OS如何工作？

Google在开发Fuchsia OS方面开辟了新天地。可以说，该公司从过去的错误中吸取了教训，尤其是在更新和修改Android和Chrome OS的局限性和问题方面。与已建立的Google操作系统的主要区别：Fuchsia OS从头到尾都是模块化的。这不仅反映在模块化系统体系结构中，而且反映在对应用程序是什么的全新理解中。

### 模块化应用设计

Google Fuchsia基于模块化设计，打破了应用程序的概念。软件单元称为*软件包*。*软件包*是一个被选中的文件—包括元数据、清单文件和可执行元素。后者在Google术语中称为*组件*。

**Fuchsia 组件**最接近我们今天所说的应用程序。每个组件执行特定任务，并且可以与其他组件组合以编程一个更复杂的应用程序。组件由清单文件以及相关的代码组成。组件始终在自己的[沙箱中](https://www.ionos.com/digitalguide/websites/web-development/what-is-sandboxing/)运行，通过名称空间访问对象，并通过导出目录发布它们。Fuchsia OS专注于两种类型的组件：*模块*（*modules* ）和*代理*（*agents*）。

***agents***组件在后台工作，并为其他组件提供服务。*agents*由另一个组件或系统调用-例如，响应某些触发（例如推送通知或其他屏幕处理）。

**modules**是具有用户界面的组件，这些组件在前台执行，对用户可见。操作系统中的每个模块都是为特定任务而设计的，并进行了相应的标记，以便可以在需要时自动对其进行访问。这是使用模块的功能完成的，可以使用所谓的*动词*和*名词*来描述。

每个模块都包括一个**verbs** 列表，表示模块可以执行的工作，以及一个**nouns** 列表，表示正在使用的实体。根据谷歌术语，实体包括作为结构化数据对象存在的任何唯一可识别的人、地点、事物、事件或概念，这些数据对象可以被引用和检索、呈现、操作或共享。

**因此，在实际中**，使用实时操作系统Fuchsia的方式如下：用户执行操作后，Fuchsia OS会自动为该任务确定适当的模块。所需的动作被翻译成动词和名词的组合。然后，系统检索所有支持所需动词的模块的列表，并在下一步中根据还可以处理所需名词的模块进行过滤。

相关的模块可以分组到所谓的**stories**中。**stories**根据当前的需求组合不同的动作和任务，使用户能够根据自己的想法和需求组装复杂的应用程序。 

概要

=借助Fuchsia OS的模块化应用程序概念，Google将重点从应用程序转移到动作和内容。Fuchsia 的任务由所谓的**stories**中的一组组件来处理，而不是当前使用的应用程序的经典操作系统，该组件通过模块访问当前所需的资源。

下图说明了Fuchsia OS应用程序开发背后的模块化概念。

[![Google操作系统Fuchsia OS的模块化结构](https://img-blog.csdnimg.cn/20201211111146753.png)](https://img-blog.csdnimg.cn/20201211111146753.png)Fuchsia OS的应用程序开发基于模块化结构。

### 模块化系统架构

Fuchsia OS的系统架构也基于模块化方法。操作系统由四个或多或少的**独立级别组成**，每个**级别**都有其自己的任务：Zircon，Garnet，Peridot和Topaz。

#### Zircon

Zircon（以前为Magenta）是新的Google操作系统的基础，但严格来说，它不是Fuchsia OS的一部分，也可以与其他操作系统一起使用。

Zircon包含**Fuchsia OS**的**内核**，设备管理器，最核心的第一层设备驱动程序以及底层系统库（如libc和launchpad）。此外，Zircon还提供FIDL（Fuchsia 接口定义语言），这是一种用于进程间通信的协议。FIDL是独立于编程语言的，但是与流行的编程语言（例如C，C ++，Dart，Go和[Rust）具有联系](https://www.ionos.com/digitalguide/websites/web-development/rust-programming-language/)。

作为Fuchsia OS的基础，Zircon提供了对后续级别的硬件访问，在共享硬件资源上创建了软件抽象，并充当了低级软件开发的平台。Zircon是[Project Little Kernel（LK）](https://github.com/littlekernel/lk/wiki/Introduction)的结果，该[项目](https://github.com/littlekernel/lk/wiki/Introduction)充当Android的引导程序。

#### Garnet

Garnet是基于Zircon的第一款针对Fuchsia 的系统层。提供了设备级别的各种系统服务以及网络，媒体和图形服务，例如，用于软件安装，系统管理以及与其他系统的通信。Garnet包含图形渲染器Escher，程序包管理和更新系统**Amber**以及文本和代码编辑器[Xi](https://github.com/xi-editor/xi-editor)。

#### Peridot

Peridot是Fuchsia OS的操作系统级别，根据当前用户要求在其上管理和编译模块化应用程序（请参见上文）。Peridot的核心成分是Ledger和Maxwell。

- **Ledger**：Ledger是基于云的存储系统（分布式存储系统），它为每个Fuchsia组件（模块或代理）提供单独的数据存储。这在不同设备之间同步。这使用户可以在当前Fuchsia 的设备上继续停留在其他Fuchsia 的设备上的位置。
- **Maxwell**：通过Maxwell，Google在Fuchsia OS中集成了一个组件，该组件将给用户提供了人工智能。就像Fuchsia 一样，Maxwell具有模块化设计。AI系统由一系列代理组成，这些代理分析用户的行为及其所使用的内容，在后台确定合适的信息，并将建议转发给操作系统-例如，应加载哪些模块或故事以适合用户在特定时间的行为。Google语言助手也是AI组件的一部分，该组件将在Fuchsia项目的框架内以代码**Kronk的**形式进一步开发。

 注意

到目前为止，Kronk是Fuchsia OS唯一未作为开源项目开发的组件。

#### Topaz

Topaz是Fuchsia OS的系统级别，用户可以在其中与操作系统进行交互。在此显示以下级别定义的组件的用户界面：带主屏幕的图形用户界面（取决于设备Armadillo或Capybara）以及模块的可视前端。Google的跨平台开源移动应用程序框架[**Flutter**](https://flutter.dev/)也已在此系统级别集成。因此，可以假定Fuchsia OS用户将来也将能够运行和使用其他系统的应用程序，例如Android或iOS应用程序。

[![Fuchsia OS的模块化系统架构](https://img-blog.csdnimg.cn/20201211111146859.png)](https://img-blog.csdnimg.cn/20201211111146859.png)Fuchsia OS的四个系统级别：Zircon， Garnet， Peridot， and Topaz

## Fuchsia OS的优缺点一目了然

按照模块化方法，Fuchsia OS的开发人员已将系统体系结构划分为具有特殊任务的各个区域。这不仅提高了代码的可读性，而且影响**了操作系统**的**适应性和更新**。除其他外，Google解决了Android长期以来一直在努力的更新问题。

 事实

Android生态系统正在努力解决更新问题。查看官方[分发仪表板可以](https://developer.android.com/about/dashboards/index.html)看到：操作系统的新版本正在缓慢传播。这是竞争对手苹果不会面临的问题。尽管Apple硬件和软件来自同一来源，可以直接进行修改，但每个Android更新必须首先由各种硬件制造商实施。

此外，模块化系统架构可满足Google销售合作伙伴的需求，他们希望根据自己的想法来适应或扩展Fuchsia OS。

硬件制造商可以与自己的产品交换操作系统的各个级别，而不会影响其他级别的功能。例如，三星可以用自己开发的TouchWiz风格的用户界面代替Topaz。亚马逊可以放弃Peridot和Google Language Assistant，而为Fuchsia OS配备基于Alexa的基于AWS的应用程序模块。

在这两种情况下，设备制造商都可以提供**个性化的Fuchsia OS版本，**而不会影响Zircon和Garnet功能或这些层的正式更新周期。

| 好处                                                         | 缺点                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| Fuchsia OS的模块化系统架构使Google可以比Android更快地推出安全更新。 | Google使Ledger成为Fuchsia OS的核心组件。Ledger控制跨多个设备的应用程序同步，从而将系统紧密地绑定到云。 |
| 由于采用了模块化设计，硬件制造商可以用自己的模块替换Fuchsia OS的各个系统级别，而不会影响其他级别的功能。 |                                                              |

## 发展状况

Fuchsia OS正在慢慢成形，但仍未准备好投放市场。Google甚至尚未宣布正式发布日期。据媒体报道，第一批硬件测试已经进行。作为首家测试Fuchsia操作系统的设备制造商，华为已成功在Honor Play上启动了新操作系统。该智能手机配备了华为麒麟970芯片，该芯片还用于该制造商的其他设备中，例如Mate 10，Mate 20和Mate 20 Pro。

## Fuchsia OS演示

Fuchsia OS可以在开发阶段早期编译为APK（Android软件包）并安装在Android智能手机和平板电脑上。该[曼努埃尔Goulão在mgoulao.github.io“>Fuchsia OS演示版Fuchsia OS演示](https://mgoulao.github.io/fuchsia-web-demo/)节目是什么样子。

如果在浏览器中访问Fuchsia OS演示，则会看到一个网站，其中显示了操作系统的启动屏幕。这为用户提供了背景图像和当前时间。此外，还有三个按钮可用：一个用于打开Wi-Fi设置的按钮，一个用于注册用户的登录按钮以及一个来宾登录。

该演示仅允许您注册为访客。

[![Armadillo – Fuchsia OS用于移动设备的图形用户界面：开始屏幕](https://img-blog.csdnimg.cn/20201211111147228.png)](https://img-blog.csdnimg.cn/20201211111147228.png)Armadillo –为触摸屏优化的Fuchsia OS图形用户界面/来源：https://mgoulao.github.io/fuchsia-web-demo/

注册用户可以访问**Fuchsia OS**的**主屏幕**，该屏幕在一页上显示所有信息。

主屏幕上最突出的元素是屏幕中央的窗口，其中包含Google搜索栏，Google语言向导和设备上安装的应用程序。

[![Armadillo – Fuchsia OS用于移动设备的图形用户界面：主屏幕](https://img-blog.csdnimg.cn/20201211111147428.png)](https://img-blog.csdnimg.cn/20201211111147428.png)借助Fuchsia OS，Google放弃了具有多个屏幕的设计，这在Android或iOS中是常见的，而是在主屏幕上显示所有内容。资料来源：https://mgoulao.github.io/fuchsia-web-demo/

如果您启动一个应用程序（仅使该演示作为虚拟对象可用），您会看到Google选择了基于**窗口的**用户界面。

[![Armadillo – Fuchsia OS用于移动设备的图形用户界面：主屏幕上作为Windows的应用程序](https://img-blog.csdnimg.cn/20201211111147587.png)](https://img-blog.csdnimg.cn/20201211111147587.png)启动的应用程序在单独的窗口中执行，并在主屏幕上以图块形式显示给用户。资料来源：https://mgoulao.github.io/fuchsia-web-demo/

单击主屏幕中间的用户图像会打开一个菜单，其中包含常用**设置**。

[![Armadillo – Fuchsia OS用于移动设备的图形用户界面：设置](https://img-blog.csdnimg.cn/20201211111147736.png)](https://img-blog.csdnimg.cn/20201211111147736.png)只需单击即可访问常用设置，例如WIFI和蓝牙设置，音量和亮度。资料来源：https://mgoulao.github.io/fuchsia-web-demo/

参考资料：

https://www.theverge.com/2020/12/8/22163225/google-fuchsia-os-call-contributors-mailing-list-governance

https://arstechnica.com/gadgets/2020/12/googles-secretive-fuchsia-os-is-open-for-contributions/

https://www.ionos.com/digitalguide/server/tools/fuchsia-os/

![](https://img-blog.csdnimg.cn/c66cc07b674c424ba11ec6825e22a640.png)

![](https://img-blog.csdnimg.cn/46f9ed15f914479ab130d47e9578e721.png)
