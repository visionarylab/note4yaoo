---
title: log-dev-summary
tags: [dev, log, repeat]
created: '2019-04-22T03:42:22.447Z'
modified: '2020-07-14T10:28:11.443Z'
---

# log-dev-summary

## dev-summary

- 现在写的代码能够稳定执行至少6个月吗？
  - 若不能，则设计有问题，或技术选型有问题
- 不要省事直接浏览别人的例子及结论
  - 15年的project到19年方法api就不一致了，自己编译更透彻
- 不要省事直接搜索问题的唯一解
  - layout与paint谁更占性能，测试实践更可靠，无唯一解，看情况
- 开发工作很多时候是用同一语言的不同框架，或用不同语言，在不同的平台将相同功能重复实现
  - 静下心来深入一个专题，总结现有方案
- 技术选型或框架选型时，对开发者友好和对用户友好的取舍
  - java的简单与功能丰富对开发者更友好，c++的高性能对用户友好
- 对于黑盒类的技术方案，不要花过多时间，如某些css属性
- 参考现有ui解决方案：dom密集操作、状态数据频繁更新
- 流行typescript库很多都用的class，所以是否用class可参考现有成熟方案的选择

## dev-tricks

- 少用if-else，多用卫语句
  - 先对可能的条件进行检验，程序的主逻辑在验证之后才开始运行
- 文档生成的解决方案还是基于markdown更方便
  - 参考 `react-markdown-loader` , 可以自动读取md内容，根据模板生成demo插入页面
- console.log打印对象时打印的是引用，一旦后面有修改，当你查看打印出的对象属性时就是查看后面修改过后的
  - 建议使用 `console.log(JSON.stringify(obj))`
  - 若obj的属性值也是对象，则打印的对象也是最终值，不是之前的
- debug时尽量使用单元测试或实现单独功能的页面，在原来复杂的源码中不便于分析生命周期顺序
  - 准备好单独的boilerplate项目或单独的unit test文件

## 技术前景与趋势

- realtime/实时
- dynamic/动态
- 3d/三维
- automation/自动化ai
- performance/算法优化

## 开发原则

- learn by practice/实用为先/使用为先
- 不要花费过多时间进行工具选择
  - 工具只是解决问题的捷径
  - 在解决业务问题后，可以花更多时间深入工具原理与抽象自己的工具

## pieces

- 开发模式/dev-framework
  - Foundation Framework: build a framework first, then build app on it 
    - 已有的开发框架选择多，框架api一般更稳定，易维护
    - 需要学习，修改难度较大，实际用到的api少时会造成代码臃肿
- Harvested Framework：start by not trying to build a framework but app, then pay attention to duplication when build other apps
    - 效率更低
- 监听器的使用    
  - 将业务逻辑系统用事件驱动方式拆分，既能使代码逻辑更清晰，又能自主掌控逻辑的同步和异步执行
  - 在业务中很多场景都可以比喻为事件，比如用户注册，可能要求注册之后发送验证信息，或者创建订单之后需要发送订单详情邮件之类的，还有就是批量处理时，可以拆成一个批量输入命令，然后触发一个事件，事件处理一个任务，这个事件触发也可以在接口或者其它地方触发，但是事件监听是同一套，不用做任何修改，如果一块逻辑已经过时，那直接去掉监听即可，代码上可能只需要修改一行即可
- java network library comparison
  - HttpURLConnection
      - HttpURLConnection是java的标准类，什么都没封装，用起来太原始，不方便，比如重访问的自定义，以及一些高级功能等
      - 从Java 9开始，通过JEP 110, HTTP/2 Client API proposal提供了对HTTP 2.0和WebSocket客户端的编程支持，以HttpClient替换HttpURLConnection/HttpsURLConnection
      - 但是该模块仍然属于沙箱试验，Java 10仍然未能正式发布。从Java 11开始，JEP 110, HTTP/2 Client API终于正式发布，模块名java.net.http
  - Apache HttpClient
      - 在jdk标准库不给力的情况下，Apache HttpComponents HttpClient通常是最佳的HTTP Client library选择。但这个库当前还不支持HTTP/2，支持HTTP/2的版本还处于beta阶段（2018.09.23），因此并不适合用于Android APP中使用，20190722发布的HttpComponents HttpClient 5.0-beta5添加了对http/2协议的支持
      - 在早期版本的Android中，Android SDK中集成了Apache的HttpClient模块，HttpClient就是一个增强版的HttpURLConnection，它只是关注于如何发送请求、接收响应，以及管理HTTP连接
      - 如果做好封装或者使用android-async-http，Afinal，Xutils也能挺简单的完成http请求，但是Android6.0已经放弃了HttpClient，不是系统自带的了
  - OkHttp
      - 由于当前Apache HttpComponents HttpClient版本并不支持 HTTP/2, 而HTTP/2对于移动客户端而言，无论是从握手延迟、响应延迟，还是资源开销看都有相当吸引力。因此这就给了高层次封装且支持HTTP/2 的 http client lib 足够的生存空间，其中最典型的要数OkHttp
      - OKHttp类似于HttpUrlConnection，是基于传输层实现应用层协议的网络框架，而不止是一个Http请求应用的库
      - 默认情况下，OKHttp会自动处理常见的网络问题：像二次连接、SSL的握手问题
      - 从Android4.4开始HttpURLConnection的底层实现采用的是okHttp
      - OkHttp基于NIO 和 Okio，Okio是基于IO和NIO基础上做的一个更简单、高效处理数据流的一个库
  - Volley
      - 是谷歌官方13年I/O大会推出的，volley在设计的时候是将具体的请求客户端做了下封装：HurlStack，也就是说可以支持HttpUrlConnection, HttpClient, OkHttp
      - 也有缺陷，比如不支持post大量数据，所以不适合上传文件。Volley设计的初衷本身也就是为频繁的、数据量小的网络请求而生
      - volley是一个简单的异步http库，仅此而已。缺点是不支持同步，这点会限制开发模式；不能post大数据，所以不适合用来上传文件
  - android-async-http
      - 与volley一样是异步网络库，但volley是封装的httpUrlConnection，它是封装的httpClient，而android平台不推荐用HttpClient了，所以这个库已经不适合android平台了
  - Retrofit
      - 基于OkHttp封装的一套RESTful网络请求框架
      - Retrofit 的封装可以说是很强大，里面涉及到一堆的设计模式，你可以通过注解直接配置请求，你可以使用不同的http客户端，虽然默认是用 Khttp ，可以使用不同Json Converter来序列化数据，同时提供对RxJava的支持
- 阿里飞冰 ice和ant design 区别
  - ice是个项目开发与管理平台，生成的项目的确是没有交互和业务逻辑，这些需要手工编码完成
  - ice前端使用的是阿里内部的fusion库，而不是antd
  - 在ice体系里，组件不受限，既可以用ice提供的组件也可以使用ant的组件，还有更多社区组件
  - 飞冰面向设计师推出iceland，能直接从设计到代码
  - 面向开发者端我们提供了iceworks工具，iceworks是与物料体系打通的关键，所有物料资源，包括iceland上设计师生产的，都会无缝打通
- 考虑禁商用的license
  - 策略：社区版开源且免费商用，专业版/加强版开源且免费非商用，商用收取技术服务费，参考ag-grid的模块
  - GPL：虽然可以商用，但二次开发的源码也要开源
  - Dual Licensing
    - Ideally, any two open-source projects should be able to share their source code with each other. 
    - However, if the two projects use incompatible licenses, then this may not be possible. 
    - For example, code developed for the Linux operating system, which uses the GPL, cannot be used by the Apache web server project because the GPL specifies additional requirements that are incompatible with the Apache license. 
    - To avoid this problem, some open-source projects have chosen to make their source code available under a dual-licensing scheme that gives developers a choice as to which license they will be bound by.

## code-engineering 

- It’s contradictory to design a component with the intention of reusing it globally, then modify that component in just one specific part of the product.
- `AnotherBodyOne > SomeNewBodyOne > BodyOne > Text`
    - fraught with maintenance issues. You'll constantly be trying to hunt down where some override happens and how to modify something in the chain without breaking everything else.
    - Another approach to incremental building is to introduce a v1 of your reuseable components, and do not allow any modification. Do the best that you can to stick to that system. Your team will quickly learn what works and what does not, and you can iterate and build a v2. Then it becomes a matter of migrating from v1 to v2.
- strict vs flexible component api (e.g. H1 vs Text)
    - we only permit layout-related props for the most part, because we found that whitespace and position at a page level is impossible to have reusable (e.g. you wouldn't hardcode a bottom margin on a button). Box and Flex components are how we do that.
    - There are a few other things we expose, such as textAlign on typography components, but that's about it. We're probably on the extreme here, but I really think overexposing the style props is dangerous.
    - It's the same concern as low-level vs high-level API.I've generally survived with being pretty restrictive for high-level components, but save myself some effort by having a handful (not many, Box & Text only usually) of low-level components that are more permissive.Users would only ever use high-level components, and have the surety they won't 'break' rules due to a restrictive styling API.
- ref
    - https://spectrum.chat/styled-system/general/opinion-do-you-prefer-more-strict-or-more-flexible-base-components~c1299d13-241d-41ec-882a-5051e8420822

## 动态链接库 dll

- 大多数操作系统将解析外部引用（比如库）作为加载过程的一部分，可执行文件包含一个叫做import directory的表，该表的每一项包含一个库的名字。根据表中记录的名字，装载程序在硬盘上搜索需要的库，然后将其加载到内存中预先不确定的位置，之后根据加载库后确定的库的地址更新可执行程序。可执行程序根据更新后的库信息调用库中的函数或引用库中的数据。这种类型的动态加载称为装载时加载，被包括Windows和Linux的大多数系统采用，最复杂的工作之一就是 **加载时链接**。
- 有些操作系统可能在运行时解析引用。在这些系统上，可执行程序调用操作系统API，将库的名字，函数在库中的编号和函数参数一同传递。操作系统负责立即解析然后代表应用调用合适的函数。这种动态链接叫做 **运行时链接** 。因为每个调用都会有系统开销，运行时链接要慢得多，对应用的性能有负面影响。
- 可以动态链接的库，在Windows上是dynamic link library (DLL)，在UNIX或Linux上是Shared  Library。库文件是预先编译链接好的可执行文件，存储在计算机的硬盘上。大多数情况下，同一时间多个应用可以使用一个库的同一份拷贝，操作系统不需要加载这个库的多个实例。  
- Windows和Linux的加载时链接是由操作系统来完成的，格式在不同的系统下有不同的区别，但是原理还是一样的。linux下文件的类型是不依赖于其后缀名的，但一般来讲：
  - .o是目标文件, 相当于windows中的.obj文件
  - .so为共享库, 是shared object, 用于动态连接的, 和dll差不多
  - .a为静态库, 是好多个.o合在一起, 用于静态连接
  - .la为libtool自动生成的一些共享库，主要记录了一些配置信息。
- 通常把一些公用函数制作成函数库, 供其它程序使用，函数库分为静态库和共享库
- 程序函数库简单的说就是一个文件包含了一些编译好的代码和数据，这些编译好的代码和数据可以供其他的程序使用。程序函数库可以使整个程序更加模块化，更容易重新编译，而且更方便升级。程序函数库可分为3种类型：静态函数库（static libraries）、共享函数库（shared libraries）和动态加载函数库（dynamically loaded libraries）。
- 静态函数库是在程序执行前就加入到目标程序中去了；而共享函数库则是在程序启动的时候加载到程序中，它可以被不同的程序共享；动态加载函数库则可以在程序运行的任何时候动态的加载
- 静态函数库实际上就是简单的一个普通的目标文件的集合，一般来说习惯用“.a”作为文件的后缀, 静态库函数允许程序员把程序link起来而不用重新编译代码，节省了重新编译代码的时间。
- 共享函数库中的函数是在当一个可执行程序在启动的时候被加载。每个共享函数库都有个特殊的名字，称作“soname”。Soname名字命名必须以“lib”作为前缀，然后是函数库的名字，然后是“.so”，最后是版本号信息。不过有个特例，就是非常底层的C库函数都不是以lib开头这样命名的。当可执行程序需要在自己的程序中列出这些他们需要的共享库函数的时候，它只要用soname就可以了
- 动态加载的函数库Dynamically loaded (DL) libraries是一类函数库，它可以在程序运行过程中的任何时间加载，们特别适合在函数中加载一些模块和plugin扩展模块的场合。Linux系统下，DL函数库与其他函数库在格式上没有特殊的区别，创建的时候是标准的object格式。主要的区别就是 这些函数库不是在程序链接的时候或者启动的时候加载，而是通过一个API来打开一个函数库，寻找符号表，处理错误和关闭函数库。通常C语言环境下，需要包含这个头文件。
- 动态链接库在unix下，习惯以 .so 为文件名结尾（通常还以 lib 开头）。而Windows下是以 . DLL 为文件后缀。如果需要运行时主动加载一个动态链接库，windows下可以使用 LoadLibrary 这个 kernel API (在 kernel32.dll 中)；unix 下是用 dlopen 。Windows 下找到 dll 中导出符号的地址，可以用 GetProcAddress ，而 unix 也有对应的 api。这些相互对应的api，似乎预示着对等的功能，但事实上是有区别的。
- DLL 事实上和 EXE 文件一样，同属 PE 格式的执行文件。对于隐式的引用外部符号，需要把外部符号所在的位置写在 PE 头上。PE 加载器将从 PE 头上找到依赖的符号表，并加载依赖的其它 DLL 文件。
- so 文件大多为 elf 执行文件格式。当它们需要的外部符号，可以不写明这些符号所在的位置。也就是说，通常 so 文件本身并不知道它依赖的那些符号在哪些 so 里面。这些符号是由调用 dlopen 的进程运行时提供的。而 unix 下的执行文件本身会暴露自己静态链接的符号，（可以是自己本身实现的，或者是从静态库 .a 文件里链入的）。dlopen 将把这些符号通报给 dlopen 加载的 .so 文件，最终完成动态链接。

## JavaFX 框架 前景 观点

- 参考
  - https://www.zhihu.com/question/305434657
  - https://www.zhihu.com/question/266195521
- 优点
  - 跨平台
  - 支持通过 fxml 和 css 来编写界面
  - 提供WebView组件
  - 借助 ExcelsiorJET 能够将 JavaFX 的应用 aot
- 缺点
  - 跨平台时可能出现一些行为不一致
  - 样式过度依赖css，很多东西都无法依赖代码来指定
  - 原生组件不算丰富
  - 对于系统原生功能支持不够，譬如没有提供支持触控板手势的API
  - 没有热加载，所以不够直观，而且api不是那么直观
- 参考
  - 旧的swing项目当然不会轻易更换框架，而新的项目没人再选择Java了。FXML、硬件加速、MVVM思想都很好，但是这些别人也有，而且成熟得比Java早，何必要换成Java？Java要是真想在GUI翻身，还得像electron那样拿出点顺应潮流的东西、别人还没做好的东西。我觉得在WebAssembly是个方向。
  - 我很看好JAVAFX，我看好一切跨平台GUI方案，包括Qt（QML），这才是应该长期发展的技术。很多人扯H5的跨平台GUI方案，你要真的纯粹用H5，不跟本地软硬件资源有任何交互，只跟服务器端增删改查，我感觉也折腾不出什么激动人心的产品，还不如人家用Chrome直接访问呢。
  - 我这里只说PC端跨平台GUI，移动端我估计会在微信小程序上实现UI的大统一，毕竟小程序为Android和IOS提供了统一的软硬件资源框架（包括摄像头，蓝牙等硬件资源），同时又为用户提供了即用即走的便利性（免安装），还为开发者节省了大量的登陆逻辑和安全风险。
  - Electron的本质是一套用NodeJS控制的Chrominum，单纯用Electron估计也就只能做一个披着应用程序边框和标题栏的网页，跟Chrome建立桌面图标有点类似。真正开发一套商业或者工业级的企业程序，不调用个把dll/so估计是不现实的，而NodeJS调用dll或者so的开发体验和运行效率，要远远低于JNI，就更别提Qt这种原生态C++了。
  - 我理想中的跨平台GUI项目选型：移动端无一例外微信小程序解决；PC端，工程师熟悉JS就用Electron，不过要做好在NodeJS平台调用dll/so的基础功课。三种框架的开发体验Electron>JAVAFX>Qt，客户体验Qt>JAVAFX>Electron，平衡下来我觉得JAVAFX还算较好的选择
  - 如今的JavaFX也不过是袭人故技，用FXML布局，Java实现业务逻辑。性能上不如duilib，开发速度上又不如Web。虽然jdk11 已经能把javafx 独立出来了，但仍无可避免jre带来的臃肿体积。重点是由于不流行 **学的人少** ，根本没公司愿意用。而且由于浏览器性能越来越强，Web单页应用如火如荼，React, Vue都妇孺皆知了，重点是效果完全不输原生应用
  - Oracle的JDK在中文输入的场景一直做得很烂。特别是用搜狗输入法的时候，有很多意料之外的行为。包括JavaFX和Swing都有问题。目前基于Java的成熟的商业应用，都会包含自己魔改过的JRE。典型例子就是Jetbrains加的产品。之前是直接借助系统JDK运行的，但后来发生了滚动条失灵、中文输入法无法输入等问题后，就捆绑了基于OpenJDK的自家的Jetbreans JRE。
  - wps office 2019 addons文件夹包含软件各个组件，几乎都是html实现的，.kuip文件包含主题样式
  - wps未使用qml

## jackson-core源码结构

- JsonParser、JsonGenerator提供顶层读写抽象类、JsonFactory提供工厂方法
- io包提供输入输出方法：跳过特殊字符、encode/decode、mergedStream、utf8->utf32
- json包提供读写具体实现
- async提供非阻塞的异步读写方法
- format包提供数据格式匹配方法
- filter提供数据过滤方法
- sym包提供特殊符号的处理方法
- type包提供泛型处理方法
- util包提供各种工具类

### jackson-core处理json

- ObjectMapper提供解析器和生成器的入口
- JsonParser提供底层json解析器
- JsonGenerator提供底层json生成器
- JsonParser的工作原理
- 将JSON分解成一系列的token，然后迭代token解析，token类型由JsonToken中一系列的常量来表示
- 如果token指向的是字段名称，JsonParser的getCurrentName()方法返回当前字段的名称。
- 如果token指向的是字符串字段值，getValueAsString()方法以字符串的形式返回当前token的值，JsonParser还有更多相似的方法，如getText()

## easyexcel 源码结构

- ExcelReader、ExcelWriter、ExcelFactory提供顶层读写具体类
- analysis包提供解析03、07格式excel的方法
- write包提供生成excel的方法
- annotation提供注解
- context包提供读写相关上下文
- event提供事件监听器
- metadata包提供spreadsheet模型抽象
- modelbuild提供将字符串转换成bean的方法
- parameter提供生成excel所需参数
- support提供枚举类
- util提供各种工具类
- constant提供常量

## SAX解析XML方法执行顺序

1. startDocument()：开始处理文档；
2. startElement(String uri, String localName, String qName, Attributes attributes)：处理元素的开始；
3. characters(char[] ch, int start, int length)：用来读取文本内容；
4. endElement(String uri, String localName, String qName)：元素处理结束；
5. endDocument()：文档处理结束
- 参考 
  - 在开始处理标签后，如 `<books>` 或 `</title>` 后，会立即调用一次characters()方法，并且在ide里面debug时无法直接追踪  
  - 若两个xml标签之间无间隔，则不会调用characters()方法，如 `<title>aa</title><author>bb</author>`

### jdk xml解析 sax方式 方法顺序

- sax中DefaultHandler解析XML的总体过程   

startDocument --> 具体读到某个node（非根node和根node）的解析过程 --> endDocument  

- 解析XML非根node的顺序  

startElement --> characters --> endElement --> characters    
(endElement后会再调用一次characters方法)    

- 解析XML根node的顺序

startElement --> characters --> endElement  

## XML的生成

- SAX parsing is for reading documents, not writing them. You can write XML with the XMLStreamWriter.
- Generating XML via Java (https://www.techrepublic.com/article/generating-xml-via-java/)
- Using the StringBuffer class
- Using DOM
- Using SAX
- Using a custom XmlWriter class

## xlsx Excel2007 常用标签结构

- sheet1.xml 
  - worksheet
      - dimension： ref=A1:D9，存放的是sheet的行列数
      - sheetViews：
      - sheetFormatPr:
      - cols：子元素col存放各列宽度
      - sheetData：存放所有单元格数据
          - row： 存放行信息，r="1" s="1" customFormat="1" ht="29" customHeight="1" spans="1:4"
              - c：存放列信息，r="A1" s="1" t="s"
                  - v：存放单元格数据， `<v>0</v>` ，文本字符串用的是sharedStrings.xml中的索引
      - pageMargins
      - headerFooter

## xlsx Excel2007 格式解析 

- Excel2007是使用XML格式来存储的，把一个excel文件(test.xlsx)后缀改为.zip，解压后的结构
- [Content_Types].xml：列出Excel解压后各个XML文件名及其类型
- xl文件夹
  - workbook.xml：列出Workbook包含的所有sheets，sheet用索引标识
  - sharedStrings.xml：Excel将各个sheet中字符型单元格的值存放在sharedStrings.xml中用于共享
  - styles.xml：存放每个单元格的样式
  - worksheets文件夹
      - sheet1.xml：存放单张sheet中所有单元格数据，其中文本型单元格数据用索引值表示
  - _rels文件夹
      - workbook.xml.rels.xml：定义了workbook中sheet1索引、styles索引、sharedStrings索引
  - theme文件夹
      - theme1.xml：定义workbook的样式
- _rels文件夹
  - .rels：描述workbook与docProps中文件的关系
- docProps文件夹：整个excel文档的元信息
  - core.xml：描述文件的创建时间、修改时间、创建者、修改者、主题
  - app.xml ：描述文档的其他属性如文档类型、版本、是否只读、是否共享、安全属性，还包括创建该文档的软件

## apache poi

- poi Class SharedStringsTable
  - Table of strings shared across all sheets in a workbook.
  - When displaying text in the spreadsheet, the cell table will just contain an index into the string table as the value of a cell, instead of the full string.
- poi各jar包作用
  - poi-version.jar：用于操作.xls文件；依赖于commons-logging, commons-codec, log4j；
  - poi-scratchpad-version.jar：用于操作.ppt、.doc、.vsd、.pub、.msg文件；依赖于poi；
  - poi-ooxml-version.jar、poi-ooxml-schemas-version.jar：用于操作.xlsx、.pptx、docx文件；依赖于poi, dom4j，xmlbeans, stax-api-1.0.1；
  - 操作Excel主要是指ss包、xssf包；

## xml的解析方式

- 基于dom
  - 将整个xml加载到内存中，形成文档对象，所有对xml操作都对内存中文档对象进行，几乎所有开发语言都支持
  - Tree model parser (Object based) (Tree of nodes).
  - DOM is read and write (can insert or delete nodes).
  - Backward and forward search is possible for searching the tags, making it easy to navigate 
  - 优点
      - 允许应用程序对数据和结构做出更改
      - 方便在树结构中导航，获取和操作任意部分的数据
  - 缺点
      - 需要加载整个XML文档来构造层次结构，内存消耗大，容易溢出

- 基于sax
  - 基于事件/流的方式，在解析XML文档时触发一系列的事件，当发现给定tag时激活一个回调方法，边解析边处理，边释放内存资源
  - push模式，由解析器调用事件处理器，一旦解析器开始执行，就会迭代每个xml元素直到结束，无法控制何时如何解析    
  - Event based parser (Sequence of events).
  - SAX is read only i.e. can’t insert or delete the node.
  - SAX reads the XML file from top to bottom and backward navigation is not possible.
  - 优点
      - 只在读取数据时检查数据，不需要保存在内存中，内存消耗小
      - 效率和性能较高，能解析大于系统内存的文档。
      - 不需要等待所有数据都被处理，分析就能立即开始。
      - 可以在某个条件得到满足时停止解析，不必解析整个文档。
  - 缺点
      - 需要应用程序自己负责TAG的处理逻辑（例如维护父/子关系等），文档越复杂程序就越复杂
      - 单向导航，无法定位文档层次，很难同时访问同一文档的不同部分数据，不支持XPath

- 基于stax
  - 基于事件/流的方式
  - pull模式，由事件处理器控制解析器何时解析下一个元素

- 其他
  - SAX解析器当接收到XML文件内容，服务器端解析器SAXParser自动开始解析，自动解析过程中调用处理器相应方法处理所有元素，这是推模式
  - StAX解析器需要手动通过next触发文档解析事件，在客户端代码中获取当前事件，从而调用相应事件处理方法
  - StAX方式解析xml的效率好于SAX 
      - SAX无选择性的，所有事件都会处理的解析方式，解析器控制事件的调用；StAX由用户自主控制需要处理事件类型以及事件的调用
      - 使用Stax进行数据解析时，随时终止解析
      - StAX has NO Support for Schema Validation
      - StAX Allows Subparsing / Delegation
      - StAX has Support for XML Writing, SAX does not have support for writing XML
      - http://tutorials.jenkov.com/java-xml/sax-vs-stax.html
  - JAXP是sun官方推出的解析xml的api，同时支持 DOM SAX StAX
  - JDOM与DOM有一些不同，JDOM仅使用具体类而不使用接口，这在某些方面简化了API，但是也限制了灵活性，还大量使用了Collections类
  - DOM4j最初是JDOM的一个分支，后来开发了许多超出基本XML文档表示的功能，包括集成的XPath支持、XML Schema支持以及用于大文档或流化文档的基于事件的处理，还提供了构建文档表示的选项
  - XML PULL是Android内置的xml解析技术，采用StAX方式解析xml，需要客户端程序手动完成解析，XmlPullParser存放解析方法next()，用于解析器解析下一事件
  - [四种生成和解析XML文档的方法详解](https://www.cnblogs.com/lanxuezaipiao/archive/2013/05/17/3082949.html )
  - [XML文档DOM、SAX、STAX解析方式详解](https://blog.csdn.net/zhongkelee/article/details/51737710  )
