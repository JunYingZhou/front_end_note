Flutter基础

## 一、Dart基础

**安装fluttersdk**,通过国内镜像安装

- url:https://flutter.cn/community/china#清华大学-tuna-协会，并设置环境变量（防止网络问题）

<img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250104225300554.png" alt="image-20250104225300554" style="zoom: 25%;" /><img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250104225417143.png" alt="image-20250104225417143" style="zoom: 80%;" />

- 将下载好的flutter文件目录下的bin目录设置环境变量，然后在命令提示符中输入flutter开始下载一些依赖

<img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250104225821891.png" alt="image-20250104225821891" style="zoom: 80%;" /><img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250104230257934.png" alt="image-20250104230257934" style="zoom:67%;" />

- 查看版本号，并输入flutter doctor安装资源

  <img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250104230424952.png" alt="image-20250104230424952" style="zoom:67%;" /><img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250104230557036.png" alt="image-20250104230557036" style="zoom:50%;" />

2、编译模式

Dart 的 JIT（Just-In-Time）编译和 AOT（Ahead-Of-Time）编译是其两种主要的编译模式，分别用于不同的场景。以下是它们的对比和特点：

------

**1. JIT（Just-In-Time）编译**

**特点**

- **即时编译**：在程序运行时，将 Dart 代码动态地编译为机器码。
- **开发友好**：主要用于开发阶段，支持快速的调试和热重载。
- **灵活性高**：允许动态反射、运行时类型检查等功能。
- **性能较慢**：由于需要在运行时编译代码，启动时间稍长，运行性能不如 AOT。

**使用场景**

- 开发阶段

  ：

  - 支持 **Hot Reload**，开发者可以快速看到代码修改的效果。
  - 在调试时更加高效。

**适用平台**

- Dart 的 JIT 编译主要在开发环境下使用，例如：
  - Flutter 应用的开发阶段（`flutter run` 默认使用 JIT）。

------

**2. AOT（Ahead-Of-Time）编译**

**特点**

- **提前编译**：在程序发布之前，将 Dart 代码编译为高效的机器码。
- **高性能**：启动时间快，运行时性能接近原生应用。
- **移除动态功能**：为了优化性能，一些动态特性（如反射）可能会被限制。
- **文件体积更大**：由于包含预编译的机器码，生成的二进制文件体积可能较大。

**使用场景**

- 生产环境

  ：

  - 用于发布高性能的生产级应用。
  - 提供更流畅的用户体验。

**适用平台**

- Dart 的 AOT 编译适用于生成生产环境的可执行文件，例如：
  - Flutter 应用的发布阶段（`flutter build` 命令）。
  - Dart CLI 工具的发布。

------

**对比总结**

| **特性**     | **JIT**                  | **AOT**                          |
| ------------ | ------------------------ | -------------------------------- |
| **编译时间** | 运行时即时编译           | 预先编译                         |
| **性能**     | 较慢的启动时间和运行性能 | 启动快，运行效率高               |
| **文件体积** | 较小（无预编译的机器码） | 较大（包含机器码）               |
| **调试支持** | 支持动态反射和热重载     | 不支持动态反射，适合优化后的代码 |
| **适用场景** | 开发阶段                 | 生产阶段                         |

------

**示例：Flutter**

- **开发阶段**（JIT 模式）：

  ```powershell
  flutter run
  ```

  - 支持热重载。
  - 适合快速迭代开发。

- **生产阶段**（AOT 模式）：

  ```powershell
  flutter build apk
  flutter build ios
  ```

  - 生成高性能的应用程序包。

------

选择 JIT 还是 AOT，取决于您是在开发阶段还是生产阶段。Dart 的双模式编译使得它在开发和部署之间能够灵活切换！

## 二、Flutter基础

### 1、创建flutter项目

- 在androidstudio中的plugins安装flutter插件，就可以创建一个flutter项目

- 但是会有国内下载慢的情况，请根据：[Flutter配置Gradle镜像，解决国内下载慢问题_flutter国内镜像-CSDN博客](https://blog.csdn.net/qianxiamuxin/article/details/134322224)

- 项目文件目录

  ​	![image-20250105153118112](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250105153118112.png)

### 2、Flutter的小组件

Flutter 中的 **Widget** 是构建用户界面的基本单元。Flutter 的一切界面元素都是由 Widget 构建的，无论是简单的按钮、文本，还是复杂的布局。

以下是 Flutter Widgets 的核心概念和分类：

------

**1. Widget 的特点**

- **不可变性**：Widget 是不可变的（immutable），其属性一旦定义就不能更改。要更新界面，Flutter 会销毁旧的 Widget 并重新构建新的 Widget。
- **树形结构**：所有 Widget 构成了一棵 Widget 树，Flutter 使用这棵树来管理和渲染界面。
- **组合性**：Widget 是高度可组合的，通过嵌套其他 Widget 可以创建复杂的 UI。

------

**2. Widget 的分类**

**a) 基础 Widgets**

- 布局相关

  ：

  - `Container`：一个多用途的容器，可设置边距、填充、边框、背景色等。
  - `Row` 和 `Column`：分别用于水平和垂直方向的布局。
  - `Stack`：用于堆叠布局，允许 Widget 重叠。
  - `Expanded` 和 `Flexible`：在布局中控制子 Widget 的伸缩行为。

- 文本和图像

  ：

  - `Text`：显示文字。
  - `RichText`：显示富文本（多样式文字）。
  - `Image`：显示图像。

**b) 输入 Widgets**

- `TextField`：用于文本输入。

- `Checkbox`：复选框。

- `Radio`：单选按钮。

- `Switch`：开关。

- `Slider`：滑块。

- Button ：按钮。
  
   系列：

  - `ElevatedButton`：具有浮起效果的按钮。
- `TextButton`：扁平按钮。
  - `IconButton`：图标按钮。
  - `FloatingActionButton`：悬浮按钮。

**c) 布局 Widgets**

- 容器 Widgets

  ：

  - `Padding`：为子 Widget 添加填充。
  - `Center`：将子 Widget 居中显示。
  - `Align`：控制子 Widget 的对齐方式。
  - `SizedBox`：指定大小的盒子。

- 列表 Widgets

  ：

  - `ListView`：滚动列表。
  - `GridView`：网格布局。
  - `SingleChildScrollView`：单个子 Widget 的滚动视图。

**d) 可交互 Widgets**

- `GestureDetector`：监听手势（点击、滑动、长按等）。
- `InkWell`：带涟漪效果的点击区域。
- `Draggable` 和 `DragTarget`：用于实现拖拽功能。

**e) 功能性 Widgets**

- `Scaffold`：提供应用的基本布局结构，如 AppBar、Drawer、FloatingActionButton 等。
- `AppBar`：顶部导航栏。
- `BottomNavigationBar`：底部导航栏。
- `TabBar` 和 `TabBarView`：用于多页面切换的标签栏。
- `Drawer`：侧边栏。
- `SnackBar`：临时显示消息。
- `Dialog` 和 `AlertDialog`：弹出对话框。

------

**3. Widget 生命周期**

Flutter 中的 Widgets 分为以下两类：

- 有状态（StatefulWidget）

  ：

  - 拥有状态，可以在运行时改变。
  - 需要实现 `createState` 方法返回一个 `State` 对象。
  - 常用于动态界面（例如计时器、用户输入等）。

- 无状态（StatelessWidget）

  ：

  - 不依赖状态，构造后不变。
  - 用于静态界面（例如标题、文本等）。

------

**4. 示例代码**

**简单界面**

```dart
dartCopy codeimport 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Flutter Widgets')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('Hello, Flutter!'),
              ElevatedButton(
                onPressed: () {
                  print('Button Pressed');
                },
                child: Text('Click Me'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

------

**5. Widget 的使用技巧**

- **热重载**：在开发时通过热重载实时查看 UI 修改效果。
- **Flutter Inspector**：用来调试和优化 Widget 树。
- **组合优先**：通过组合简单 Widgets 构建复杂 UI，而非从零实现。

### 3、样式和字体

- 修改字体的样式：

```dart
          title: const Text(
            '解谜之印',
            style: TextStyle(
                fontSize: 20.0,
                fontWeight: FontWeight.bold,
                letterSpacing: 2.0,
                color: Colors.white,
                fontFamily: 'RubikVinyl' 
            ),
          ),
```

- 字体

  可在https://fonts.google.com/download/next-steps中搜索自己想要的字体，新建一个font文件夹，将下载好的字体放到其中，并在yaml文件中进行配置

  <img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250105181330825.png" alt="image-20250105181330825" style="zoom: 50%;" />

### 4、StatelessWidget

在 Flutter 中，`StatelessWidget` 是一种用于创建不可变的 UI 组件的基类。它的特点是：一旦创建，**状态不可改变**。如果组件的状态需要改变，你应该使用 `StatefulWidget`。

**`StatelessWidget` 的特点**

1. **不可变性**：
   - 一旦组件被构建，它的属性和外观将保持不变。
   - 通常用于显示静态内容或通过外部传递的数据更新显示。
   
2. **性能更高**：
   
   - 因为不需要管理状态，`StatelessWidget` 的构建和重新渲染效率更高。
   
3. **无状态逻辑**：
   
   - 组件的内容完全依赖于传递给它的参数。
   
4. ### **生命周期**

   `StatelessWidget` 的生命周期只有一个方法：

   1. `build()`

      ：

      - 必须实现的方法，用于定义 UI。

      - 每次组件需要重绘时都会调用。

        ```dart
        @override
        Widget build(BuildContext context) {
          return Text('Hello StatelessWidget');
        }
        ```

        

------

**如何定义一个 `StatelessWidget`**

创建一个 `StatelessWidget` 的步骤如下：

```dart
dartCopy codeimport 'package:flutter/material.dart';

class MyStatelessWidget extends StatelessWidget {
  // 接受外部参数
  final String title;

  // 构造函数
  MyStatelessWidget({required this.title});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: Text(
          '这是一个 StatelessWidget 示例',
          style: TextStyle(fontSize: 18),
        ),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: MyStatelessWidget(title: '欢迎页面'),
  ));
}
```

------

**构成解析**

1. **`final` 属性**：
   - 在 `StatelessWidget` 中，所有属性通常是 `final`，因为它们在整个生命周期中是不可变的。
   - 例：`final String title;`
2. **`build` 方法**：
   - 核心方法，用于描述 UI。
   - 每当 Flutter 框架需要渲染该组件时，它会调用 `build` 方法。
3. **使用传参更新内容**：
   - 数据通过构造函数传递，外部数据变化时重新构建组件即可更新内容。

------

**使用场景**

1. 显示静态内容，比如：
   - 标题、按钮、图片等。
   - 非交互性组件。
2. 内容随父组件状态变化但自身不需要管理状态。

### 5、图像&静态资源

在 Flutter 中，`NetworkImage` 和 `AssetImage` 都是用于加载图片的类。两者的主要区别在于图片的来源和用途：

**1. `NetworkImage`**

用于加载**网络上的图片**。

**特点**

- 图片来自网络 URL。
- 在需要动态获取远程图片的场景下使用。
- 会根据网络状态加载，可能会有延迟。

**示例**

```dart
import 'package:flutter/material.dart';

class NetworkImageExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("NetworkImage 示例")),
      body: Center(
        child: Image.network(
          'https://example.com/your-image.jpg',
          loadingBuilder: (BuildContext context, Widget child, ImageChunkEvent? loadingProgress) {
            if (loadingProgress == null) return child;
            return Center(
              child: CircularProgressIndicator(
                value: loadingProgress.expectedTotalBytes != null
                    ? loadingProgress.cumulativeBytesLoaded / (loadingProgress.expectedTotalBytes ?? 1)
                    : null,
              ),
            );
          },
          errorBuilder: (BuildContext context, Object error, StackTrace? stackTrace) {
            return Text('图片加载失败');
          },
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: NetworkImageExample()));
```

**常见属性**

- `loadingBuilder`：提供加载过程中的自定义效果（如进度条）。
- `errorBuilder`：处理图片加载失败时显示的内容。

------

**2. `AssetImage`**

用于加载**本地资源文件中的图片**。

**特点**

- 图片保存在项目目录的 `assets` 文件夹中。
- 需要在 `pubspec.yaml` 文件中声明资源路径。
- 不依赖网络，更快更稳定。

**配置步骤**

1. **将图片放入 `assets` 文件夹**（可以自定义文件夹路径）。
    示例路径：`assets/images/your-image.png`

2. **在 `pubspec.yaml` 中声明**：

   ```yaml
   flutter:
     assets:
       - assets/images/your-image.png
   ```

3. **使用 `AssetImage` 或 `Image.asset` 加载**：

**示例**

```dart
import 'package:flutter/material.dart';

class AssetImageExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("AssetImage 示例")),
      body: Center(
        child: Image.asset('assets/images/your-image.png'),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: AssetImageExample()));
```

------

**对比总结**

| 特性           | `NetworkImage`                          | `AssetImage`                   |
| -------------- | --------------------------------------- | ------------------------------ |
| **来源**       | 网络 URL                                | 本地资源                       |
| **优点**       | 动态加载，适合展示远程图片              | 本地加载，速度快，无需网络依赖 |
| **缺点**       | 依赖网络，可能加载失败或速度慢          | 需要提前打包到应用中           |
| **使用场景**   | 头像、API 返回的图片                    | 图标、背景图、固定资源         |
| **加载时效果** | 支持 `loadingBuilder` 和 `errorBuilder` | 无特殊效果                     |

### 6、Icon&Button

在 Flutter 中，`Icon` 和 `Button` 是常用的 UI 组件，分别用于显示图标和交互式按钮。以下是它们的详细介绍与示例：

------

**1. Icon**

`Icon` 是一个用于显示图标的组件，通常与 `Icons` 类配合使用。

**特点**

- 显示矢量图标，具有高性能和良好的扩展性。
- Flutter 提供了大量内置的图标，通过 `Icons` 类访问。
- 可以自定义大小、颜色和样式。

**基本用法**

```dart
import 'package:flutter/material.dart';

class IconExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Icon 示例")),
      body: Center(
        child: Icon(
          Icons.favorite, // 使用内置图标
          color: Colors.red, // 设置颜色
          size: 50.0, // 设置大小
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: IconExample()));
```

**常见属性**

- `Icons`：内置图标类，包含大量常用图标（如 `Icons.home`、`Icons.search`）。
- `size`：图标的大小。
- `color`：图标的颜色。
- `semanticLabel`：用于无障碍功能的文本描述。

------

**2. Button**

Flutter 提供了多种按钮组件，满足不同的交互需求。

**2.1 ElevatedButton**

- 一个凸起的按钮，具有阴影效果，常用于强调的操作。

```dart
import 'package:flutter/material.dart';

class ElevatedButtonExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("ElevatedButton 示例")),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            print("按钮被点击！");
          },
          child: Text("Elevated Button"),
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: ElevatedButtonExample()));
```

**2.2 TextButton**

- 一个没有阴影的扁平按钮，常用于辅助操作。

```dart
import 'package:flutter/material.dart';

class TextButtonExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("TextButton 示例")),
      body: Center(
        child: TextButton(
          onPressed: () {
            print("TextButton 被点击！");
          },
          child: Text("Text Button"),
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: TextButtonExample()));
```

**2.3 IconButton**

- 一个仅包含图标的按钮，常用于操作栏或列表项。

```dart
import 'package:flutter/material.dart';

class IconButtonExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("IconButton 示例")),
      body: Center(
        child: IconButton(
          icon: Icon(Icons.thumb_up),
          color: Colors.blue,
          onPressed: () {
            print("IconButton 被点击！");
          },
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: IconButtonExample()));
```

**2.4 FloatingActionButton**

- 一个浮动按钮，常用于突出主要操作。

```dart
import 'package:flutter/material.dart';

class FloatingActionButtonExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("FloatingActionButton 示例")),
      body: Center(child: Text("点击按钮试试")),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          print("FloatingActionButton 被点击！");
        },
        child: Icon(Icons.add),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: FloatingActionButtonExample()));
```

------

**图标与按钮的组合**

图标可以与按钮组合，形成更丰富的交互效果。

```dart
import 'package:flutter/material.dart';

class IconWithButtonExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("图标与按钮组合")),
      body: Center(
        child: ElevatedButton.icon(
          onPressed: () {
            print("带图标的按钮被点击！");
          },
          icon: Icon(Icons.send, color: Colors.white),
          label: Text("发送"),
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: IconWithButtonExample()));
```

------

**对比总结**

| 特性         | Icon                             | Button                                       |
| ------------ | -------------------------------- | -------------------------------------------- |
| **用途**     | 显示静态或装饰性图标             | 提供用户交互功能                             |
| **常见实现** | `Icon`, `ImageIcon`              | `ElevatedButton`, `TextButton`, `IconButton` |
| **支持交互** | 不支持（可通过外部包裹按钮实现） | 支持点击、悬停、长按等交互                   |

### 7、Container&Padding

在 Flutter 中，`Container` 和 `Padding` 都是常用的布局组件，它们用于控制子组件的布局和间距。尽管它们有一些重叠的功能，但它们在用途和性能上有所不同。

**1. Container**

`Container` 是一个通用的布局容器，可以同时处理许多布局需求，如尺寸、边距、内边距、对齐等。

**特点**

- 允许对子组件设置宽度、高度、边距、内边距、对齐方式、背景颜色等。
- 是一个功能强大的通用布局容器，适用于多种布局场景。

**常见属性**

- `width`、`height`：设置容器的宽高。
- `padding`：设置容器的内边距，通常与 `EdgeInsets` 配合使用。
- `margin`：设置容器的外边距，通常与 `EdgeInsets` 配合使用。
- `decoration`：设置容器的装饰，例如边框、背景色、阴影等。
- `alignment`：设置容器内子组件的对齐方式。

**示例**

```
dartCopy codeimport 'package:flutter/material.dart';

class ContainerExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Container 示例")),
      body: Center(
        child: Container(
          width: 200,
          height: 100,
          padding: EdgeInsets.all(16),
          margin: EdgeInsets.all(10),
          decoration: BoxDecoration(
            color: Colors.blue,
            borderRadius: BorderRadius.circular(8),
            boxShadow: [BoxShadow(color: Colors.black26, blurRadius: 8)],
          ),
          alignment: Alignment.center,
          child: Text(
            "我是一个 Container",
            style: TextStyle(color: Colors.white, fontSize: 16),
          ),
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: ContainerExample()));
```

------

**2. Padding**

`Padding` 是一个专门用于设置内边距（即子组件与其父组件之间的空间）的组件。它仅仅是调整子组件与其边界之间的距离。

**特点**

- 只用于设置内边距，不能设置其他布局属性（如宽度、高度等）。
- 主要用于为子组件提供间距。

**常见属性**

- `padding`：设置内边距，通常使用 `EdgeInsets` 来指定不同方向的边距。

**示例**

```
dartCopy codeimport 'package:flutter/material.dart';

class PaddingExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Padding 示例")),
      body: Center(
        child: Padding(
          padding: EdgeInsets.all(16), // 设置内边距
          child: Container(
            color: Colors.blue,
            child: Text(
              "我是一个带有 Padding 的 Container",
              style: TextStyle(color: Colors.white),
            ),
          ),
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: PaddingExample()));
```

------

**Container 与 Padding 的对比**

| 特性         | `Container`                                | `Padding`                          |
| ------------ | ------------------------------------------ | ---------------------------------- |
| **功能**     | 多功能的容器，可以设置尺寸、边距、装饰等   | 专门用于设置内边距                 |
| **主要用途** | 用于容纳和装饰子组件，支持更多的布局和样式 | 仅用于调整子组件与父组件之间的间距 |
| **性能**     | 相对更重，包含更多功能                     | 性能更轻，专注于内边距             |
| **常用场景** | 布局、装饰、设置尺寸、对齐等               | 只为子组件添加间距                 |

**性能考虑**

- 如果只需要设置内边距，使用 `Padding` 是更优的选择，因为它的性能开销较小。
- `Container` 可以提供更多的功能，但在只需要内边距时不应过度使用它。

**总结**

- 如果你需要灵活的布局和多样的装饰，选择 `Container`。
- 如果你仅仅需要设置内边距，`Padding` 会更加简洁和高效。

### 8、Rows

<img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250112213320860.png" alt="image-20250112213320860" style="zoom:67%;" />

在 Flutter 中，`Row` 是一个常用的布局组件，用于水平排列子组件。`Row` 会将它的子组件沿水平方向依次排列，并允许你控制它们之间的间距、对齐方式等。

**Row 组件**

`Row` 是一个**水平线性布局**，默认情况下，它的子组件会根据可用的空间水平排列。

**常见属性**

- `children`: 一个 `List<Widget>`，包含 `Row` 的子组件。
- `mainAxisAlignment`: 用于控制子组件在主轴（水平轴）上的对齐方式。
- `crossAxisAlignment`: 用于控制子组件在交叉轴（垂直轴）上的对齐方式。
- `mainAxisSize`: 控制主轴的空间占用，默认是 `MainAxisSize.max`，即尽可能占用最大空间。
- `textDirection`: 设置 `Row` 中子组件的文本方向，通常用于支持不同语言的布局。
- `verticalDirection`: 控制子组件排列的垂直方向，可以设置为 `VerticalDirection.up` 或 `VerticalDirection.down`。

**常见的对齐方式**

- `MainAxisAlignment`: 控制主轴（水平方向）的对齐方式。
  - `MainAxisAlignment.start`: 子组件从左边开始排列。
  - `MainAxisAlignment.center`: 子组件居中排列。
  - `MainAxisAlignment.end`: 子组件从右边开始排列。
  - `MainAxisAlignment.spaceBetween`: 子组件之间均匀分布，第一个和最后一个子组件紧靠父容器的两端。
  - `MainAxisAlignment.spaceAround`: 子组件之间有相等的间距，每个子组件的两端也会留有间距。
  - `MainAxisAlignment.spaceEvenly`: 子组件之间和子组件与父容器两端的距离相等。
- `CrossAxisAlignment`: 控制交叉轴（垂直方向）的对齐方式。
  - `CrossAxisAlignment.start`: 子组件顶部对齐。
  - `CrossAxisAlignment.center`: 子组件垂直居中对齐。
  - `CrossAxisAlignment.end`: 子组件底部对齐。
  - `CrossAxisAlignment.stretch`: 子组件拉伸，填满交叉轴的空间。

**示例**

**基础 Row 示例**

```dart
import 'package:flutter/material.dart';

class RowExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Row 示例")),
      body: Center(
        child: Row(
          children: [
            Icon(Icons.star, size: 50, color: Colors.orange),
            Icon(Icons.star, size: 50, color: Colors.orange),
            Icon(Icons.star, size: 50, color: Colors.orange),
          ],
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: RowExample()));
```

**主轴对齐：MainAxisAlignment**

```dart
import 'package:flutter/material.dart';

class MainAxisAlignmentExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("MainAxisAlignment 示例")),
      body: Center(
        child: Row(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            Icon(Icons.star, size: 50, color: Colors.orange),
            Icon(Icons.star, size: 50, color: Colors.orange),
            Icon(Icons.star, size: 50, color: Colors.orange),
          ],
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: MainAxisAlignmentExample()));
```

**交叉轴对齐：CrossAxisAlignment**

```dart
import 'package:flutter/material.dart';

class CrossAxisAlignmentExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("CrossAxisAlignment 示例")),
      body: Center(
        child: Row(
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            Icon(Icons.star, size: 50, color: Colors.orange),
            Container(width: 20),
            Icon(Icons.star, size: 100, color: Colors.orange),
            Container(width: 20),
            Icon(Icons.star, size: 75, color: Colors.orange),
          ],
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: CrossAxisAlignmentExample()));
```

**Row 与 Expanded**

`Row` 中的子组件如果超出了父容器的宽度，可以使用 `Expanded` 来让子组件占据可用的剩余空间。

```dart
import 'package:flutter/material.dart';

class ExpandedRowExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Expanded 示例")),
      body: Center(
        child: Row(
          children: [
            Expanded(
              child: Container(
                color: Colors.red,
                height: 50,
                child: Center(child: Text("Box 1")),
              ),
            ),
            Expanded(
              child: Container(
                color: Colors.green,
                height: 50,
                child: Center(child: Text("Box 2")),
              ),
            ),
            Expanded(
              child: Container(
                color: Colors.blue,
                height: 50,
                child: Center(child: Text("Box 3")),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

void main() => runApp(MaterialApp(home: ExpandedRowExample()));
```

**总结**

- **`Row`** 组件用于水平排列子组件。
- **`MainAxisAlignment`** 用于控制主轴（水平方向）的对齐。
- **`CrossAxisAlignment`** 用于控制交叉轴（垂直方向）的对齐。
- **`Expanded`** 可以让子组件占据可用空间，防止溢出。
- `Row` 是一个非常强大的布局工具，适用于大多数水平排列需求。

### 9、Column

在 Flutter 中，`Column` 是一种用于垂直布局的组件（Widget）。它会将其子组件按从上到下的顺序进行排列。`Column` 常用于创建包含多个子组件的垂直布局，比如表单、按钮列表等。

以下是 `Column` 的基本使用方法和常见属性：

------

基本使用

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Column Example'),
        ),
        body: Column(
          mainAxisAlignment: MainAxisAlignment.center, // 主轴（垂直方向）对齐方式
          crossAxisAlignment: CrossAxisAlignment.center, // 副轴（水平方向）对齐方式
          children: [
            Text('Item 1'),
            Text('Item 2'),
            ElevatedButton(
              onPressed: () {},
              child: Text('Button'),
            ),
          ],
        ),
      ),
    );
  }
}
```

------

常用属性

1. **`mainAxisAlignment`**

控制主轴（垂直方向）上的子组件对齐方式。

- `MainAxisAlignment.start`: 从顶部开始对齐（默认）。
- `MainAxisAlignment.center`: 居中对齐。
- `MainAxisAlignment.end`: 从底部对齐。
- `MainAxisAlignment.spaceBetween`: 子组件均匀分布，首尾没有空隙。
- `MainAxisAlignment.spaceAround`: 子组件均匀分布，首尾有一半的空隙。
- `MainAxisAlignment.spaceEvenly`: 子组件均匀分布，空隙相等。

2. **`crossAxisAlignment`**

控制副轴（水平方向）上的子组件对齐方式。

- `CrossAxisAlignment.start`: 从左边开始对齐。
- `CrossAxisAlignment.center`: 水平居中对齐（默认）。
- `CrossAxisAlignment.end`: 从右边对齐。
- `CrossAxisAlignment.stretch`: 拉伸子组件以填满水平空间。

3. **`mainAxisSize`**

决定 `Column` 在主轴方向上的大小。

- `MainAxisSize.max`: 占满父组件的高度（默认）。
- `MainAxisSize.min`: 根据子组件的高度自动调整。

4. **`children`**

接受一个子组件列表，用于定义 `Column` 中的内容。

------

示例：带间距的垂直布局

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
    Container(color: Colors.red, height: 50, width: 50),
    Container(color: Colors.green, height: 50, width: 50),
    Container(color: Colors.blue, height: 50, width: 50),
  ],
)
```

------

### 10、Expanded

在 Flutter 中，`Expanded` 是一个非常常用的组件，用于扩展其子组件以填充父组件的可用空间。它通常在 `Row`、`Column` 或 `Flex` 布局中使用，帮助实现子组件在主轴方向上的灵活布局。

------

`Expanded` 的核心功能

- 它会占据父组件主轴方向上的剩余空间。
- 当有多个 `Expanded` 子组件时，它们会按照比例共享剩余空间。

------

基本用法

以下是一个简单的例子，展示了如何使用 `Expanded` 来调整组件的宽度或高度。

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Expanded Example'),
        ),
        body: Column(
          children: [
            Container(
              color: Colors.red,
              height: 100,
            ),
            Expanded(
              child: Container(
                color: Colors.green,
              ),
            ),
            Container(
              color: Colors.blue,
              height: 100,
            ),
          ],
        ),
      ),
    );
  }
}
```

在这个例子中：

- 红色和蓝色的容器有固定的高度（`100`）。
- 绿色的容器使用 `Expanded`，会占用剩余的垂直空间。

------

多个 `Expanded` 的比例分配

你可以使用 `flex` 属性来定义多个 `Expanded` 子组件之间的比例关系。默认值是 `1`。

```dart
Column(
  children: [
    Expanded(
      flex: 2,
      child: Container(color: Colors.red),
    ),
    Expanded(
      flex: 1,
      child: Container(color: Colors.green),
    ),
    Expanded(
      flex: 3,
      child: Container(color: Colors.blue),
    ),
  ],
)
```

在这个例子中：

- 红色容器占据总高度的 2/6。
- 绿色容器占据总高度的 1/6。
- 蓝色容器占据总高度的 3/6。

------

与 `Spacer` 的结合使用

如果需要在布局中插入空白区域，可以结合 `Spacer` 使用，它实际上是一个带 `flex` 的空 `Expanded`。

```dart
Column(
  children: [
    Container(color: Colors.red, height: 50),
    Spacer(flex: 1),
    Container(color: Colors.green, height: 50),
    Spacer(flex: 2),
    Container(color: Colors.blue, height: 50),
  ],
)
```

在这个例子中：

- 第一个空白区域的大小是总剩余空间的 1/3。
- 第二个空白区域的大小是总剩余空间的 2/3。

------

注意事项

1. **适用场景**
   - `Expanded` 只能用于 `Row`、`Column` 或其他类似的 Flex 布局中。
   - 它不适用于非 Flex 布局的父组件。
2. **嵌套使用**
   - 如果需要限制子组件的最小或最大尺寸，可以结合 `Flexible` 或 `SizedBox` 一起使用。

------

### 11、StatefulWidget

在 Flutter 中，`StatefulWidget` 是一种可以维护状态并根据状态变化更新 UI 的组件。它由两个部分组成：

1. **`StatefulWidget` 类**：定义组件本身。
2. **`State` 类**：负责维护状态和实现逻辑。

**StatefulWidget 的核心结构**

```dart
import 'package:flutter/material.dart';

class MyStatefulWidget extends StatefulWidget {
  // 构造函数、可接收外部参数
  const MyStatefulWidget({Key? key}) : super(key: key);

  // 创建状态类
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  // 定义状态变量
  int counter = 0;

  // 更新状态的方法
  void incrementCounter() {
    setState(() {
      counter++;
    });
  }

  // 构建 UI
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('StatefulWidget Example')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Counter value: $counter'),
            ElevatedButton(
              onPressed: incrementCounter,
              child: Text('Increment'),
            ),
          ],
        ),
      ),
    );
  }
}
```

------

**生命周期**

`StatefulWidget` 和 `State` 有完整的生命周期管理，便于开发者处理状态和资源。

**`StatefulWidget` 生命周期**

`StatefulWidget` 的生命周期只有一个常用方法：

- `createState()`：创建状态类的实例。

**`State` 生命周期**

`State` 类有以下生命周期方法：

1. **`initState`**：

   - 初始化状态。
   - 仅调用一次。
   - 用于初始化数据、设置监听等操作。

   ```dart
   @override
   void initState() {
     super.initState();
     print('State initialized');
   }
   ```

2. **`didChangeDependencies`**：

   - 当依赖项发生变化时调用。
   - 比如 `InheritedWidget` 更新时会触发。

   ```dart
   @override
   void didChangeDependencies() {
     super.didChangeDependencies();
     print('Dependencies changed');
   }
   ```

3. **`build`**：

   - 必须实现的方法，返回组件的 UI。
   - 每次调用 `setState`，`build` 都会被重新执行。

   ```dart
   @override
   Widget build(BuildContext context) {
     return Container();
   }
   ```

4. **`setState`**：

   - 用于更新状态并触发界面重建。

   ```dart
   void increment() {
     setState(() {
       counter++;
     });
   }
   ```

5. **`didUpdateWidget`**：

   - 当父组件重新构建并传递新的数据时调用。
   - 用于对比新旧 `widget` 并执行逻辑。

   ```dart
   @override
   void didUpdateWidget(MyStatefulWidget oldWidget) {
     super.didUpdateWidget(oldWidget);
     print('Widget updated');
   }
   ```

6. **`deactivate`**：

   - 在状态被暂时移除时调用。

   ```dart
   @override
   void deactivate() {
     super.deactivate();
     print('State deactivated');
   }
   ```

7. **`dispose`**：

   - 在组件销毁时调用。
   - 用于释放资源、取消监听等。

   ```dart
   @override
   void dispose() {
     super.dispose();
     print('State disposed');
   }
   ```

------

**使用场景**

`StatefulWidget` 常用于需要动态更新的数据或交互场景，例如：

1. **计数器**：用户点击按钮，数字动态增加。
2. **表单输入**：用户输入数据并动态验证。
3. **动画效果**：通过状态切换实现动画。

------

**注意事项**

1. **状态更新需使用 `setState`**：
   - 只有通过 `setState` 更新状态，Flutter 才会重新调用 `build` 方法。
   - 避免在不必要的地方频繁调用 `setState`，以提升性能。
2. **避免过多逻辑放在 `build` 方法**：
   - `build` 方法应尽量保持简洁。
   - 将复杂逻辑提取到其他方法或组件中。
3. **资源释放**：
   - 在 `dispose` 方法中释放资源（如监听、控制器等），以避免内存泄漏。

------

**完整示例**

以下是一个使用 `StatefulWidget` 实现计数器的完整示例：

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CounterPage(),
    );
  }
}

class CounterPage extends StatefulWidget {
  @override
  _CounterPageState createState() => _CounterPageState();
}

class _CounterPageState extends State<CounterPage> {
  int counter = 0;

  void incrementCounter() {
    setState(() {
      counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter Example')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('You have pressed the button this many times:'),
            Text('$counter', style: TextStyle(fontSize: 24)),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: incrementCounter,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

------

### 12、ListView

在 Flutter 中，`List` 是一个常见的组件，用于展示一系列的数据项。`ListView` 是 Flutter 中最常用的列表组件，用于构建垂直、水平的滚动列表。`ListView` 提供了多种属性和方法，以下是一些常用的属性和方法的介绍。

1. `ListView` 组件的常用属性

1.1 `children`

- **类型**: `List<Widget>`
- **描述**: `children` 是一个列表，它包含了你想在列表中展示的所有子项（`Widget`）。这个属性适用于不需要动态加载数据的静态列表。

```dart
ListView(
  children: [
    ListTile(title: Text('Item 1')),
    ListTile(title: Text('Item 2')),
    ListTile(title: Text('Item 3')),
  ],
);
```

1.2 `builder`

- **类型**: `IndexedWidgetBuilder`
- **描述**: `builder` 是一个惰性加载的构建方法，通常与动态列表结合使用。它按需构建列表项，适用于列表项较多时的性能优化。

```dart
ListView.builder(
  itemCount: 10,
  itemBuilder: (context, index) {
    return ListTile(title: Text('Item $index'));
  },
);
```

1.3 `itemCount`

- **类型**: `int`
- **描述**: 定义列表中项的数量。这个属性通常与 `builder` 配合使用，告诉 `ListView` 要显示多少项。

```dart
ListView.builder(
  itemCount: 10, // 列表项的数量
  itemBuilder: (context, index) {
    return ListTile(title: Text('Item $index'));
  },
);
```

1.4 `scrollDirection`

- **类型**: `Axis`
- **描述**: 控制列表的滚动方向。`Axis.vertical` 表示垂直滚动，`Axis.horizontal` 表示水平滚动。

```dart
ListView(
  scrollDirection: Axis.horizontal, // 水平滚动
  children: [
    Container(color: Colors.red, width: 100, height: 100),
    Container(color: Colors.green, width: 100, height: 100),
  ],
);
```

1.5 `padding`

- **类型**: `EdgeInsets`
- **描述**: 控制列表的内边距。

```dart
ListView(
  padding: EdgeInsets.all(10), // 给列表设置全边距
  children: [
    ListTile(title: Text('Item 1')),
    ListTile(title: Text('Item 2')),
  ],
);
```

1.6 `shrinkWrap`

- **类型**: `bool`
- **描述**: 如果为 `true`，则列表会根据内容大小调整其高度；否则，`ListView` 将占满所有可用空间。这个属性常用于嵌套列表。

```dart
ListView(
  shrinkWrap: true, // 列表根据内容调整大小
  children: [
    ListTile(title: Text('Item 1')),
    ListTile(title: Text('Item 2')),
  ],
);
```

1.7 `reverse`

- **类型**: `bool`
- **描述**: 如果为 `true`，列表的滚动方向会反转，通常用于将列表倒序显示。

```dart
ListView(
  reverse: true, // 列表倒序
  children: [
    ListTile(title: Text('Item 1')),
    ListTile(title: Text('Item 2')),
  ],
);
```

2. `ListView` 组件的常用方法

2.1 `scrollTo`

- **描述**: `ListView` 组件本身并没有直接提供 `scrollTo` 方法，但我们可以使用 `ScrollController` 来控制滚动。

```dart
ScrollController _controller = ScrollController();

ListView.builder(
  controller: _controller, // 绑定控制器
  itemCount: 10,
  itemBuilder: (context, index) {
    return ListTile(title: Text('Item $index'));
  },
);

// 滚动到特定位置
_controller.jumpTo(100.0); // 立即跳转到100的位置
```

2.2 `animateTo`

- **描述**: 用于平滑滚动到特定位置。`animateTo` 方法可以给定滚动目标的偏移量，并支持滚动动画。

```dart
_controller.animateTo(
  100.0, // 滚动到的位置
  duration: Duration(seconds: 1), // 动画时长
  curve: Curves.ease, // 动画效果
);
```

3. `ListTile` 组件的属性（常用于 `ListView` 中）

3.1 `leading`

- **类型**: `Widget`
- **描述**: `leading` 用于设置列表项前面的控件，例如图标、图片等。常用于放置 `Icon`、`Image` 等小部件。

```dart
ListTile(
  leading: Icon(Icons.check),
  title: Text('Item 1'),
);
```

3.2 `title`

- **类型**: `Widget`
- **描述**: 设置列表项的主内容，通常是一个 `Text` 小部件。

```dart
ListTile(
  title: Text('Item 1'),
);
```

3.3 `subtitle`

- **类型**: `Widget`
- **描述**: 设置列表项的副内容，通常是一个描述性文本。

```dart
ListTile(
  title: Text('Item 1'),
  subtitle: Text('This is the subtitle'),
);
```

3.4 `trailing`

- **类型**: `Widget`
- **描述**: 设置列表项后面的控件，通常用来放置操作按钮、复选框、开关等。

```dart
ListTile(
  title: Text('Item 1'),
  trailing: Icon(Icons.arrow_forward),
);
```

4. `ListView` 的常见子类

4.1 `ListView.builder`

- **描述**: 用于构建一个懒加载的列表，根据需求逐个构建列表项。

```dart
ListView.builder(
  itemCount: 10,
  itemBuilder: (context, index) {
    return ListTile(title: Text('Item $index'));
  },
);
```

4.2 `ListView.separated`

- **描述**: 用于构建一个带分隔符的列表。分隔符可以是任意小部件，如 `Divider` 或 `Padding`。

```dart
ListView.separated(
  itemCount: 10,
  itemBuilder: (context, index) {
    return ListTile(title: Text('Item $index'));
  },
  separatorBuilder: (context, index) {
    return Divider(); // 分隔符
  },
);
```

4.3 `ListView.custom`

- **描述**: 用于创建自定义的 `ListView`，通常用于需要高度定制化的布局。

```dart
ListView.custom(
  childrenDelegate: SliverChildBuilderDelegate(
    (context, index) {
      return ListTile(title: Text('Item $index'));
    },
    childCount: 10,
  ),
);
```

------

总结

`ListView` 是 Flutter 中非常强大的组件，具有多种属性和方法，可以灵活地构建不同类型的列表。常用的属性包括 `children`、`builder`、`itemCount`、`scrollDirection`、`padding` 等，方法包括控制滚动的 `animateTo`、`jumpTo`，以及通过 `leading`、`title`、`trailing` 定义 `ListTile` 的布局。

### 13、Card

在 Flutter 中，`Card` 是一个提供 **Material Design 风格**的容器组件，它可以用来实现圆角、阴影等常见的卡片效果，特别适合用来展示信息块。以下是对 `Card` 的深入讲解，包括其特性、属性、使用场景以及复杂案例。

------

**Card 的核心特性**

1. **圆角与阴影**
   - 默认情况下，`Card` 有轻微的圆角和阴影，符合 Material Design 风格。
   - 可以通过 `shape` 和 `elevation` 属性自定义。
2. **背景色**
   - 默认使用 Material 的 `surface` 颜色。
   - 可以通过 `color` 属性更改。
3. **裁剪行为**
   - 可以通过 `clipBehavior` 控制子组件是否超出卡片范围。
4. **自定义形状**
   - `Card` 支持通过 `ShapeBorder` 设置自定义形状，比如圆形、椭圆等。

------

**Card 属性详解**

| 属性                 | 类型                 | 描述                                                         |
| -------------------- | -------------------- | ------------------------------------------------------------ |
| `color`              | `Color`              | 卡片的背景颜色。                                             |
| `elevation`          | `double`             | 控制卡片的阴影深度，值越大阴影越明显，默认值为 `1.0`。       |
| `margin`             | `EdgeInsetsGeometry` | 控制卡片外部的边距，默认是 `EdgeInsets.all(4.0)`。           |
| `shape`              | `ShapeBorder`        | 自定义卡片的形状，比如 `RoundedRectangleBorder`、`CircleBorder` 等。 |
| `clipBehavior`       | `Clip`               | 控制子组件是否会被裁剪，默认值为 `Clip.none`。               |
| `borderOnForeground` | `bool`               | 决定边框是否绘制在前景，默认为 `true`。                      |
| `child`              | `Widget`             | 卡片的子组件，用于展示具体内容。                             |

------

**基础用法**

**1. 最简单的卡片**

```dart
Card(
  child: Padding(
    padding: const EdgeInsets.all(16.0),
    child: Text('Hello, Flutter!'),
  ),
)
```

- **效果**：展示一个简单的卡片，内部包含文字。

- 默认属性

  ：

  - `elevation = 1.0`
  - `margin = EdgeInsets.all(4.0)`

------

**2. 自定义卡片形状与阴影**

```dart
Card(
  elevation: 8.0, // 阴影深度
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(15.0), // 圆角
  ),
  child: Padding(
    padding: const EdgeInsets.all(16.0),
    child: Text('Custom shaped Card!'),
  ),
)
```

- **效果**：卡片具有更大的阴影和圆角。

------

**3. 设置背景颜色**

```dart
Card(
  color: Colors.blue[50],
  elevation: 4,
  child: Padding(
    padding: const EdgeInsets.all(16.0),
    child: Text('Card with custom color!'),
  ),
)
```

- **效果**：卡片背景颜色更改为浅蓝色。

------

**Card 的进阶用法**

**1. 在卡片中嵌套复杂组件**

```dart
Card(
  elevation: 6,
  margin: EdgeInsets.all(10),
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(10),
  ),
  child: Column(
    mainAxisSize: MainAxisSize.min,
    children: <Widget>[
      ListTile(
        leading: Icon(Icons.album, size: 50),
        title: Text('Card Title'),
        subtitle: Text('This is a subtitle'),
      ),
      ButtonBar(
        children: <Widget>[
          TextButton(
            onPressed: () {},
            child: Text('ACTION 1'),
          ),
          TextButton(
            onPressed: () {},
            child: Text('ACTION 2'),
          ),
        ],
      ),
    ],
  ),
)
```

- 应用场景

  ：

  - 卡片用于展示标题、副标题、图片、操作按钮等内容。
  - 非常适合用在列表视图或网格视图中。

------

**2. 使用 `clipBehavior` 裁剪内容**

```dart
Card(
  clipBehavior: Clip.antiAlias, // 裁剪子组件
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(15),
  ),
  child: Column(
    children: <Widget>[
      Image.network('https://via.placeholder.com/150'),
      Padding(
        padding: const EdgeInsets.all(16.0),
        child: Text('Card with clipped image!'),
      ),
    ],
  ),
)
```

- **效果**：图片会被裁剪成卡片的圆角形状。

------

**3. 动态生成卡片**

在卡片中动态生成内容，比如从列表数据中映射生成卡片组件。

```dart
final List<String> items = ['Apple', 'Banana', 'Cherry'];

ListView(
  children: items.map((item) {
    return Card(
      margin: EdgeInsets.all(10),
      child: ListTile(
        title: Text(item),
        leading: Icon(Icons.local_grocery_store),
      ),
    );
  }).toList(),
)
```

- **效果**：根据列表生成多个卡片，每个卡片中显示不同的内容。

------

**卡片布局的常见搭配**

1. **`ListView`** 卡片通常用于列表项，结合 `ListView` 显示。

2. **`GridView`** 在网格布局中使用卡片展示内容块。

3. **`InkWell`** 给卡片添加点击效果。

   ```dart
   Card(
     elevation: 4,
     child: InkWell(
       onTap: () {
         print('Card tapped!');
       },
       child: Padding(
         padding: const EdgeInsets.all(16.0),
         child: Text('Tap me!'),
       ),
     ),
   )
   ```

------

**完整示例：卡片结合列表和点击**

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  final List<String> items = ['Flutter', 'Dart', 'React', 'Node'];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Flutter Card Example')),
        body: ListView.builder(
          itemCount: items.length,
          itemBuilder: (context, index) {
            return Card(
              margin: EdgeInsets.all(10),
              elevation: 6,
              child: ListTile(
                leading: Icon(Icons.book),
                title: Text(items[index]),
                subtitle: Text('Learn more about ${items[index]}'),
                onTap: () {
                  print('${items[index]} tapped!');
                },
              ),
            );
          },
        ),
      ),
    );
  }
}
```

- 效果

  ：

  - 列表中展示了多个卡片，每个卡片可以响应点击事件。
  - 适合用来展示课程列表、产品列表等内容。

------

### 14、Stack

在 Flutter 中，`Stack` 是一个强大的布局组件，用于在屏幕上 **堆叠多个子组件**。子组件可以相互重叠，也可以通过指定位置属性来调整其在堆叠中的位置。`Stack` 常用于实现复杂的 UI 布局，比如带浮动按钮的图片、徽章角标等。

------

**Stack 的核心特性**

- **子组件堆叠**：`Stack` 的子组件按照声明顺序从底到顶排列，后添加的子组件会显示在前面的组件上。
- **定位布局**：通过 `Positioned` 或 `Align` 来精确控制子组件的位置。
- **灵活性**：支持结合其他布局组件构建复杂的布局。

------

**Stack 构造函数**

```dart
Stack({
  Key? key,
  AlignmentGeometry alignment = AlignmentDirectional.topStart, // 子组件的对齐方式
  TextDirection? textDirection,  // 文本方向（如 LTR 或 RTL）
  StackFit fit = StackFit.loose, // 子组件如何填充父组件
  Clip clipBehavior = Clip.hardEdge, // 子组件是否会被裁剪
  List<Widget> children = const <Widget>[], // 子组件列表
})
```

------

**重要属性解析**

| 属性            | 类型                | 说明                                                         |
| --------------- | ------------------- | ------------------------------------------------------------ |
| `alignment`     | `AlignmentGeometry` | 控制未定位子组件在 `Stack` 中的对齐方式，默认值为左上角对齐。 |
| `textDirection` | `TextDirection`     | 控制对齐和位置是否基于文本方向（如从左到右或从右到左）。     |
| `fit`           | `StackFit`          | 控制子组件是否填充 `Stack` 的可用空间，默认为 `StackFit.loose`。 |
| `clipBehavior`  | `Clip`              | 控制子组件是否裁剪在 `Stack` 的边界内，默认为 `Clip.hardEdge`。 |
| `children`      | `List<Widget>`      | 堆叠在 `Stack` 内的子组件列表。                              |

------

**基础用法**

**1. 简单的堆叠组件**

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Stack Example')),
        body: Center(
          child: Stack(
            children: [
              Container(
                width: 200,
                height: 200,
                color: Colors.blue,
              ),
              Container(
                width: 150,
                height: 150,
                color: Colors.red,
              ),
              Container(
                width: 100,
                height: 100,
                color: Colors.green,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

- **效果**：绿色、红色、蓝色的矩形从顶部到底部堆叠，形成嵌套效果。

------

**2. 使用 `Positioned` 定位子组件**

`Positioned` 可以控制子组件在 `Stack` 中的位置。

```dart
Stack(
  children: [
    Container(
      width: 200,
      height: 200,
      color: Colors.blue,
    ),
    Positioned(
      top: 50,
      left: 50,
      child: Container(
        width: 100,
        height: 100,
        color: Colors.red,
      ),
    ),
    Positioned(
      bottom: 20,
      right: 20,
      child: Container(
        width: 50,
        height: 50,
        color: Colors.green,
      ),
    ),
  ],
)
```

- 效果

  ：

  - 蓝色矩形作为背景。
  - 红色矩形距离顶部和左侧各 `50` 像素。
  - 绿色矩形距离底部和右侧各 `20` 像素。

------

**3. 使用 `alignment` 控制对齐方式**

```dart
Stack(
  alignment: Alignment.center, // 子组件居中对齐
  children: [
    Container(
      width: 200,
      height: 200,
      color: Colors.blue,
    ),
    Container(
      width: 100,
      height: 100,
      color: Colors.red,
    ),
  ],
)
```

- **效果**：红色矩形在蓝色矩形的正中心。

------

**Stack 的高级用法**

**1. 重叠图片与文本**

```dart
Stack(
  alignment: Alignment.bottomCenter,
  children: [
    Image.network(
      'https://via.placeholder.com/300',
      width: 300,
      height: 200,
      fit: BoxFit.cover,
    ),
    Container(
      color: Colors.black54,
      width: double.infinity,
      padding: EdgeInsets.all(10),
      child: Text(
        'Beautiful Scenery',
        style: TextStyle(color: Colors.white, fontSize: 16),
        textAlign: TextAlign.center,
      ),
    ),
  ],
)
```

- **效果**：图片底部覆盖一个半透明背景，显示文本。

------

**2. 动态徽章**

```dart
Stack(
  children: [
    Icon(
      Icons.shopping_cart,
      size: 100,
    ),
    Positioned(
      top: 5,
      right: 5,
      child: Container(
        padding: EdgeInsets.all(4),
        decoration: BoxDecoration(
          color: Colors.red,
          shape: BoxShape.circle,
        ),
        child: Text(
          '3',
          style: TextStyle(color: Colors.white, fontSize: 12),
        ),
      ),
    ),
  ],
)
```

- **效果**：购物车图标右上角显示一个红色的数量徽章。

------

**3. 全屏布局**

```dart
Stack(
  fit: StackFit.expand, // 子组件填满整个 Stack
  children: [
    Container(color: Colors.blue),
    Align(
      alignment: Alignment.topCenter,
      child: Text(
        'Top Text',
        style: TextStyle(color: Colors.white, fontSize: 24),
      ),
    ),
    Align(
      alignment: Alignment.bottomCenter,
      child: Text(
        'Bottom Text',
        style: TextStyle(color: Colors.white, fontSize: 24),
      ),
    ),
  ],
)
```

- **效果**：蓝色背景，顶部和底部各显示一行文字。

------

**注意事项**

1. **性能问题**
   - 当 `Stack` 中有多个复杂子组件时，可能会影响渲染性能。
   - 使用时尽量减少嵌套层级。
2. **裁剪行为**
   - 默认情况下，`Stack` 的子组件可能超出父组件边界。
   - 可以通过设置 `clipBehavior` 为 `Clip.antiAlias` 或 `Clip.hardEdge` 来裁剪内容。
3. **尺寸限制**
   - 如果 `Stack` 的父组件有固定尺寸，子组件可能会被裁剪或缩放。

------

**总结**

`Stack` 是 Flutter 中一个高度灵活的布局组件，适用于各种需要子组件重叠、精确定位的场景。常见的使用场景包括：

1. **复杂的 UI 组合**：如图文叠加、角标徽章。
2. **全屏布局**：如背景与内容层分离。
3. **自定义布局**：通过 `Positioned` 精确控制子组件位置。

通过结合 `alignment`、`Positioned` 和其他组件，可以实现多种多样的堆叠效果！

**总结**

`Card` 是一个功能强大、灵活的组件，能适应多种 UI 场景：

1. **显示简单文本**：可以用作信息展示的容器。
2. **包含复杂内容**：适合展示图片、文字、按钮等混合内容。
3. **动态生成**：结合数据驱动 UI，适合动态生成卡片内容。

通过自定义形状、阴影、裁剪等属性，`Card` 可以快速构建出符合设计要求的卡片式组件。





------

### 📚 15、Drawer（侧边栏）

`Drawer` 是 Flutter 提供的一个用于实现 **侧边栏菜单** 的组件，常用于 App 的主界面中进行页面导航、用户信息展示等。

------

🧱 1. 基本结构

```dart
Scaffold(
  appBar: AppBar(title: Text('示例')),
  drawer: Drawer(
    child: ListView(
      children: [
        DrawerHeader(...),
        ListTile(...),
        ListTile(...),
      ],
    ),
  ),
  body: ...,
)
```

------

🧭 2. Scaffold 中的 Drawer 属性

| 属性名                | 说明                       |
| --------------------- | -------------------------- |
| `drawer`              | 左侧抽屉                   |
| `endDrawer`           | 右侧抽屉                   |
| `drawerScrimColor`    | 抽屉展开时主界面的遮罩颜色 |
| `drawerEdgeDragWidth` | 允许拖拽打开抽屉的边界宽度 |
| `onDrawerChanged`     | 抽屉开合状态监听           |

------

🪟 3. DrawerHeader 与 UserAccountsDrawerHeader

✅ DrawerHeader（普通标题）

```dart
DrawerHeader(
  decoration: BoxDecoration(color: Colors.blue),
  child: Text('欢迎使用', style: TextStyle(color: Colors.white)),
)
```

👤 UserAccountsDrawerHeader（带头像和信息）

```dart
UserAccountsDrawerHeader(
  accountName: Text("张三"),
  accountEmail: Text("zhangsan@example.com"),
  currentAccountPicture: CircleAvatar(
    backgroundImage: NetworkImage("https://example.com/avatar.jpg"),
  ),
)
```

------

📋 4. 添加菜单项：ListTile

```dart
ListTile(
  leading: Icon(Icons.home),
  title: Text('首页'),
  onTap: () {
    Navigator.pop(context); // 关闭 Drawer
    // 执行跳转等操作
  },
)
```

常用属性：

| 属性       | 说明           |
| ---------- | -------------- |
| `leading`  | 左侧图标       |
| `title`    | 主要标题       |
| `subtitle` | 副标题（可选） |
| `trailing` | 右侧图标/文本  |
| `onTap`    | 点击回调函数   |

------

📐 5. 示例完整代码

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Drawer Demo',
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Drawer 示例')),
      drawer: Drawer(
        child: ListView(
          padding: EdgeInsets.zero,
          children: [
            UserAccountsDrawerHeader(
              accountName: Text("张三"),
              accountEmail: Text("zhangsan@example.com"),
              currentAccountPicture: CircleAvatar(
                backgroundImage: NetworkImage("https://example.com/avatar.jpg"),
              ),
            ),
            ListTile(
              leading: Icon(Icons.home),
              title: Text('首页'),
              onTap: () {
                Navigator.pop(context);
              },
            ),
            ListTile(
              leading: Icon(Icons.settings),
              title: Text('设置'),
              onTap: () {
                Navigator.pop(context);
              },
            ),
          ],
        ),
      ),
      body: Center(child: Text('主页面')),
    );
  }
}
```

------

📤 6. 打开/关闭 Drawer 的方法

手动打开：

```dart
Scaffold.of(context).openDrawer();
```

手动关闭：

```dart
Navigator.pop(context);
```

------

📌 7. 使用右侧 Drawer（endDrawer）

```dart
Scaffold(
  endDrawer: Drawer(
    child: Text('右侧抽屉'),
  ),
)
```

打开方式：

```dart
Scaffold.of(context).openEndDrawer();
```

------

🧠 8. 小贴士

- `Drawer` 也可以是任何 Widget，不一定是 `ListView`。
- 通常配合 `ListTile` 来实现导航项，便于维护。
- 可结合 `Navigator.push` 等跳转页面。

------

📦 9. 常见扩展玩法

- 加入动画或渐变背景
- 响应登录状态变化动态渲染内容
- 使用 `Bloc` / `Provider` 等状态管理控制内容展示
- 抽屉中显示版本号、退出登录等功能项

------







## 补充

### 1、数据监听ValueNotifier

`ValueNotifier` 是 Flutter 中一个非常有用的类，它实现了 `ValueListenable` 接口，用于通知监听者某个值的变化。与传统的 `setState` 方法不同，`ValueNotifier` 让你能够在数据变化时只更新部分 UI，而不需要重新构建整个组件树。

1. **什么是 `ValueNotifier`？**

`ValueNotifier` 是 Flutter 中提供的一种可观察的值的类。它保存一个值并且允许监听者（通常是小部件）在值变化时得到通知。`ValueNotifier` 可以与 `ValueListenableBuilder` 一起使用，以便在值变化时自动更新 UI。

`ValueNotifier` 可以用于许多场景，特别是在数据变化频繁，但不需要重新渲染整个界面的情况下。

2. **基本构造函数和用法**

创建一个 `ValueNotifier`

你可以通过给定一个初始值来创建一个 `ValueNotifier`：

```dart
ValueNotifier<int> counter = ValueNotifier<int>(0);  // 初始值为 0
```

这里，`ValueNotifier<int>` 表示它持有一个 `int` 类型的值。你可以随时更改它的值。

修改值

你可以通过访问 `ValueNotifier` 的 `value` 属性来修改它的值：

```dart
counter.value = 5;  // 设置值为 5
```

或者通过调用 `notifyListeners()` 手动通知所有监听者。

3. #### **使用 `ValueListenableBuilder` 来监听 `ValueNotifier`**

`ValueNotifier` 实现了 `ValueListenable` 接口，因此你可以使用 `ValueListenableBuilder` 来监听 `ValueNotifier` 的变化，并根据值变化更新 UI。

```dart
ValueListenableBuilder<int>(
  valueListenable: counter,  // 监听 counter 的值
  builder: (context, value, child) {
    return Text('Counter value: $value');  // 当 counter 的值发生变化时，更新 UI
  },
)
```

每次 `counter.value` 改变时，`ValueListenableBuilder` 会触发 `builder` 回调函数，更新 UI。

4. **常见使用场景**

示例 1: 简单的计数器

```dart
class CounterApp extends StatefulWidget {
  @override
  _CounterAppState createState() => _CounterAppState();
}

class _CounterAppState extends State<CounterApp> {
  final ValueNotifier<int> _counter = ValueNotifier<int>(0);

  void _incrementCounter() {
    _counter.value++;  // 增加计数器的值
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter App')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            // 使用 ValueListenableBuilder 来监听 _counter 的变化
            ValueListenableBuilder<int>(
              valueListenable: _counter,
              builder: (context, value, child) {
                return Text(
                  'Counter: $value',  // 显示当前计数
                  style: TextStyle(fontSize: 30),
                );
              },
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _incrementCounter,
              child: Text('Increment'),
            ),
          ],
        ),
      ),
    );
  }
}
```

在这个示例中：

- `ValueNotifier<int>(0)` 创建了一个初始值为 0 的计数器。
- `ValueListenableBuilder<int>` 监听 `_counter`，当 `_counter` 的值变化时，`builder` 会重新构建 UI。
- 按下按钮时，调用 `_incrementCounter()` 增加 `counter` 的值，`ValueListenableBuilder` 会自动刷新 UI。

示例 2: 监听进度条

```dart
class ProgressApp extends StatelessWidget {
  final ValueNotifier<double> _progressNotifier = ValueNotifier<double>(0.0);

  void _incrementProgress() {
    if (_progressNotifier.value < 1.0) {
      _progressNotifier.value += 0.1;
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Progress Example")),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            ValueListenableBuilder<double>(
              valueListenable: _progressNotifier,
              builder: (context, progress, child) {
                return Column(
                  children: [
                    LinearProgressIndicator(value: progress),  // 显示进度条
                    SizedBox(height: 20),
                    Text("${(progress * 100).toStringAsFixed(0)}%"),  // 显示进度百分比
                  ],
                );
              },
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _incrementProgress,  // 增加进度
              child: Text("Increment Progress"),
            ),
          ],
        ),
      ),
    );
  }
}
```

在这个例子中，我们用 `ValueNotifier<double>` 来表示进度。每次点击按钮时，`_progressNotifier.value` 增加 0.1，并通过 `ValueListenableBuilder` 更新 UI。

5. **`ValueNotifier` 的优点**

- **高效更新**：`ValueNotifier` 只会通知监听它的组件部分更新，不会导致整个组件树重建，因此非常适合频繁变动的值，如进度条、计数器等。
- **便捷性**：与传统的 `setState` 不同，`ValueNotifier` 让你能专注于数据的更新和监听，而不必手动管理状态。
- **UI和数据解耦**：使用 `ValueNotifier` 可以将业务逻辑与 UI 逻辑解耦，数据变化时自动刷新相关 UI。

6. **使用注意事项**

- **性能**：在性能要求较高的应用中，频繁的值变化可能会导致性能问题。尽量避免在 `builder` 中执行过于复杂的计算操作。
- **状态管理**：`ValueNotifier` 是简单的状态管理工具，适合用于简单的场景。如果你的应用涉及更复杂的状态管理，可能需要考虑使用更强大的状态管理工具，如 `Provider`、`Riverpod` 或 `Bloc`。

7. **总结**

`ValueNotifier` 是一个非常强大的工具，可以用于在数据变化时自动更新 UI，它简化了 UI 更新的流程，避免了传统的 `setState` 造成的性能浪费。你可以通过 `ValueNotifier` 来轻松地处理各种数据变化场景，尤其是在需要动态显示数据的应用中，如计数器、进度条等。

### 2、文本编辑器

`TextEditingController` 是 Flutter 中用于管理文本输入框内容的一个类。它不仅可以控制输入框中的文本内容，还能监听文本的变化，提供获取和修改文本的方法。常见的使用场景包括表单输入、搜索框、文本编辑器等。

1. **基本概念**

`TextEditingController` 用于控制和操作 `TextField` 或 `TextFormField` 的内容。它提供了以下功能：

- 获取文本框中的文本
- 设置文本框中的文本
- 监听文本变化
- 清空文本框

2. **构造方法**

```dart
TextEditingController();
```

`TextEditingController` 有一个构造方法，可以不传参数（初始化为空），也可以传入一个初始文本：

```dart
TextEditingController(text: 'Initial Text');
```

3. **基本用法**

在 `TextField` 中使用 `TextEditingController` 来绑定和控制文本内容。

示例 1: 简单的文本输入框

```dart
class MyTextFieldApp extends StatefulWidget {
  @override
  _MyTextFieldAppState createState() => _MyTextFieldAppState();
}

class _MyTextFieldAppState extends State<MyTextFieldApp> {
  // 创建 TextEditingController 实例
  final TextEditingController _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("TextEditingController Example")),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          children: [
            // 使用 TextEditingController 绑定 TextField
            TextField(
              controller: _controller,
              decoration: InputDecoration(hintText: "Enter something"),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // 获取文本框中的内容
                print('Text entered: ${_controller.text}');
              },
              child: Text('Print Text'),
            ),
          ],
        ),
      ),
    );
  }
}
```

在这个例子中，`_controller` 被绑定到 `TextField`，每当你输入内容时，它会存储在 `_controller.text` 中。点击按钮时，打印出当前文本框中的内容。

示例 2: 设置初始文本和清空文本框

```dart
class MyTextFieldApp extends StatefulWidget {
  @override
  _MyTextFieldAppState createState() => _MyTextFieldAppState();
}

class _MyTextFieldAppState extends State<MyTextFieldApp> {
  // 创建 TextEditingController 实例，并设置初始文本
  final TextEditingController _controller = TextEditingController(text: "Hello");

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("TextEditingController Example")),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: InputDecoration(hintText: "Enter something"),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // 清空文本框
                _controller.clear();
              },
              child: Text('Clear Text'),
            ),
          ],
        ),
      ),
    );
  }
}
```

在这个例子中，`TextEditingController` 被初始化为 `"Hello"`，并且通过点击按钮可以清空文本框中的内容。

4. **监听文本变化**

你可以使用 `TextEditingController` 的 `addListener` 方法来监听文本变化。每次用户输入文本时，`addListener` 会触发回调函数。

```dart
class MyTextFieldApp extends StatefulWidget {
  @override
  _MyTextFieldAppState createState() => _MyTextFieldAppState();
}

class _MyTextFieldAppState extends State<MyTextFieldApp> {
  final TextEditingController _controller = TextEditingController();

  @override
  void initState() {
    super.initState();
    // 添加监听器
    _controller.addListener(() {
      print('Current text: ${_controller.text}');
    });
  }

  @override
  void dispose() {
    _controller.dispose();  // 释放 TextEditingController
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("TextEditingController Listener Example")),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: InputDecoration(hintText: "Enter something"),
            ),
          ],
        ),
      ),
    );
  }
}
```

在这个例子中，每次文本框内容变化时，都会触发监听器并打印出当前文本。记得在 `dispose()` 方法中释放 `TextEditingController`，以避免内存泄漏。

5. **`TextField` 的其他常用操作**

除了获取和设置文本外，`TextEditingController` 还提供了以下常用操作：

- **`clear()`**: 清空文本框内容。

  ```dart
  _controller.clear();  // 清空文本框
  ```

- **`selection`**: 获取或设置文本框中的文本选择范围。你可以用它来控制光标位置或选择一部分文本。

  ```dart
  // 获取选中文本
  print(_controller.selection);
  
  // 设置光标位置
  _controller.selection = TextSelection.fromPosition(TextPosition(offset: 5));
  ```

- **`text`**: 获取或设置文本框的内容。

  ```dart
  String currentText = _controller.text;  // 获取文本
  _controller.text = 'New Text';          // 设置文本
  ```

6. **`TextEditingController` 在表单中的使用**

在表单中，`TextEditingController` 经常和 `TextFormField` 一起使用，以便管理表单的文本输入。

```dart
class MyFormApp extends StatefulWidget {
  @override
  _MyFormAppState createState() => _MyFormAppState();
}

class _MyFormAppState extends State<MyFormApp> {
  final _controller = TextEditingController();
  final _formKey = GlobalKey<FormState>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Form Example')),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _controller,
                decoration: InputDecoration(hintText: 'Enter something'),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Please enter some text';
                  }
                  return null;
                },
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () {
                  if (_formKey.currentState?.validate() ?? false) {
                    // 如果表单验证通过，获取文本框的内容
                    print('Form text: ${_controller.text}');
                  }
                },
                child: Text('Submit'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

在这个例子中，我们使用了 `TextFormField` 来创建一个表单输入框，并通过 `TextEditingController` 控制和验证输入的内容。

7. **注意事项**

- **内存管理**: 在 `StatefulWidget` 中使用 `TextEditingController` 时，记得在 `dispose()` 方法中调用 `_controller.dispose()` 来释放控制器，避免内存泄漏。
- **UI更新**: `TextEditingController` 本身并不会触发 UI 更新。如果需要根据文本变化动态更新 UI，可以结合 `setState` 或其他状态管理方法来实现。

8. **总结**

`TextEditingController` 是 Flutter 中用于管理和控制 `TextField` 和 `TextFormField` 文本内容的重要工具。它允许你获取、修改、清空文本框内容，并可以监听文本的变化。通过结合 `TextEditingController` 和 `TextFormField`，你可以轻松地实现复杂的表单和文本输入逻辑。

### 3、GETX

在 Flutter 中，**GetX** 是一个流行的轻量级状态管理工具，同时提供了路由管理和依赖注入功能。它的特点是简单、高效，能够帮助开发者快速构建高性能应用。

------

**GetX 的核心功能**

1. **状态管理**：响应式的状态管理方式，让 UI 自动监听和更新数据变化。
2. **路由管理**：支持命名路由和无上下文的页面导航。
3. **依赖注入**：便捷地管理依赖，避免复杂的上下文传递。

------

**如何集成 GetX**

1. 在 `pubspec.yaml` 中添加依赖：

   ```yaml
   dependencies:
     get: ^4.6.5
   ```

2. 导入 GetX：

   ```dart
   import 'package:get/get.dart';
   ```

------

**核心模块讲解**

1. **状态管理**

**响应式变量**

- 使用 `Rx` 类型创建响应式变量。
- 当变量值发生变化时，UI 会自动更新。

**示例：响应式计数器**

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

class CounterController extends GetxController {
  var count = 0.obs; // 声明一个响应式变量

  void increment() {
    count++; // 更新变量值
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final CounterController controller = Get.put(CounterController());

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('GetX Example')),
        body: Center(
          child: Obx(() => Text(
                'Count: ${controller.count}',
                style: TextStyle(fontSize: 24),
              )),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: controller.increment,
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

- 关键点

  ：

  - `obs` 将普通变量转为响应式变量。
  - `Obx` 用于监听响应式变量的变化并更新 UI。
  - 使用 `Get.put` 注入控制器，方便在全局访问。

------

**简单变量管理（非响应式）**

- 如果不需要响应式，可以直接使用普通变量配合 `update()` 方法。

**示例：普通变量管理**

```dart
class CounterController extends GetxController {
  int count = 0;

  void increment() {
    count++;
    update(); // 手动通知 UI 更新
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetBuilder<CounterController>(
      init: CounterController(),
      builder: (controller) {
        return Scaffold(
          body: Center(
            child: Text('Count: ${controller.count}'),
          ),
          floatingActionButton: FloatingActionButton(
            onPressed: controller.increment,
            child: Icon(Icons.add),
          ),
        );
      },
    );
  }
}
```

------

2. **路由管理**

**无上下文导航**

使用 GetX，您可以在任何地方导航，无需上下文。

**示例：导航到新页面**

```dart
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home Page')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Get.to(DetailPage()); // 跳转到 DetailPage
          },
          child: Text('Go to Detail Page'),
        ),
      ),
    );
  }
}

class DetailPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Detail Page')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Get.back(); // 返回上一页
          },
          child: Text('Go Back'),
        ),
      ),
    );
  }
}
```

------

**命名路由**

**示例：配置命名路由**

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      initialRoute: '/',
      getPages: [
        GetPage(name: '/', page: () => HomePage()),
        GetPage(name: '/details', page: () => DetailPage()),
      ],
    );
  }
}
```

- 跳转到命名路由

  ：

  ```dart
  Get.toNamed('/details');
  ```

- 返回上一页

  ：

  ```dart
  Get.back();
  ```

------

3. **依赖注入**

**通过 `Get.put` 注入**

- 在应用中全局注册控制器或依赖：

  ```dart
  final controller = Get.put(MyController());
  ```

**通过 `Get.lazyPut` 懒加载**

- 当依赖首次使用时再创建实例：

  ```dart
  Get.lazyPut(() => MyController());
  ```

**通过 `Get.find` 获取实例**

- 任何地方都可以访问已注册的依赖：

  ```dart
  final controller = Get.find<MyController>();
  ```

**示例：依赖注入**

```dart
class MyController extends GetxController {
  var name = 'Flutter'.obs;
}

void main() {
  Get.put(MyController()); // 注册依赖
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final controller = Get.find<MyController>();
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: Obx(() => Text('Hello, ${controller.name}')),
        ),
      ),
    );
  }
}
```

------

4. **Snackbar 和 Dialog**

- **Snackbar**：

  ```dart
  Get.snackbar('Title', 'This is a message');
  ```

- **Dialog**：

  ```dart
  Get.defaultDialog(
    title: 'Dialog Title',
    content: Text('This is a dialog'),
  );
  ```

- **底部弹窗**：

  ```dart
  Get.bottomSheet(
    Container(
      color: Colors.white,
      child: Wrap(
        children: [
          ListTile(
            leading: Icon(Icons.accessibility),
            title: Text('Option 1'),
            onTap: () => Get.back(),
          ),
        ],
      ),
    ),
  );
  ```

------

**总结**

GetX 是一个功能全面、简单易用的工具，适用于小型到中型的 Flutter 项目。其核心功能包括：

- 响应式状态管理
- 无上下文路由导航
- 依赖注入与管理

**优点**：

- 简单易学
- 无需依赖上下文
- 灵活高效

**适用场景**：

- 需要快速开发高性能应用。
- 对于项目规模不大但对性能和开发效率有较高要求的场景。

通过 GetX，您可以大幅提升开发效率，快速构建复杂的应用程序！



很好，这里我们来深入地、系统性地讲清楚：

------

### 4、🚀 Flutter 静态组件和非静态组件详解

在 Flutter 中，**“静态组件” 和 “非静态组件”** 并不是官方术语，但它们通常是指：

| 术语       | Flutter 正确叫法                |
| ---------- | ------------------------------- |
| 静态组件   | `StatelessWidget`（无状态组件） |
| 非静态组件 | `StatefulWidget`（有状态组件）  |

------

#### 🧠 为什么这样设计？

Flutter 的设计核心是 **声明式 UI + 不可变组件 + 状态管理清晰**。

- `Widget` 是 **不可变** 的 UI 描述（只描述结构）。
- 如果组件**不需要存储状态**，就用 `StatelessWidget`（轻量、性能好）。
- 如果组件**需要存储状态**（比如用户交互、动画等），就用 `StatefulWidget`。
- 状态由独立的 `State` 类来管理，使状态与描述分离，**保持职责单一且生命周期可控**。

------

#### 🧱 静态组件（StatelessWidget）

✅ 特点

- 不需要保存任何状态
- 所有配置通过构造函数传入
- UI 不会随着时间或交互发生变化
- 构建速度快，内存占用小

🔁 生命周期只有一个：

```dart
@override
Widget build(BuildContext context)
```

🌰 示例

```dart
class MyStaticWidget extends StatelessWidget {
  final String title;
  MyStaticWidget({required this.title});

  @override
  Widget build(BuildContext context) {
    return Text(title);
  }
}
```

------

#### 🔄 非静态组件（StatefulWidget）

✅ 特点

- 需要持久化状态，比如动画控制器、输入框、计数器等
- 可以通过 `setState` 触发 UI 更新
- 使用了两个类：
  - `StatefulWidget`：组件配置（不可变）
  - `State`：状态持有者（可变，生命周期完整）

#### ⚙️ 生命周期详解

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  // 1. 创建状态对象时调用
  @override
  void initState() {
    super.initState();
    print('initState');
  }

  // 2. 第一次依赖变化时调用（如 InheritedWidget）
  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    print('didChangeDependencies');
  }

  // 3. 每次 build
  @override
  Widget build(BuildContext context) {
    return Text('Hello');
  }

  // 4. 父组件重新构建时（传参发生变化）
  @override
  void didUpdateWidget(covariant MyWidget oldWidget) {
    super.didUpdateWidget(oldWidget);
    print('didUpdateWidget');
  }

  // 5. 组件临时从树上移除（但可能会重新挂载）
  @override
  void deactivate() {
    super.deactivate();
    print('deactivate');
  }

  // 6. 永久移除组件（释放资源）
  @override
  void dispose() {
    super.dispose();
    print('dispose');
  }
}
```

📌 生命周期执行顺序（首次挂载）：

```
createState ➝ initState ➝ didChangeDependencies ➝ build
```

📌 生命周期执行顺序（组件更新）：

```
didUpdateWidget ➝ build
```

📌 生命周期执行顺序（移除组件）：

```
deactivate ➝ dispose
```

------

#### 🧠 为什么 StatefulWidget 设计成两个类？

这可能是你最关心的问题，我们详细拆解下。

| 设计点                          | 原因                                      |
| ------------------------------- | ----------------------------------------- |
| Widget 是不可变的               | 便于热重载、调试和性能优化                |
| Widget 每次 setState 都会被重建 | 但我们要保留状态，所以状态必须单独存储    |
| State 存在于 Element 树中       | 不会随着 Widget 重建而消失                |
| 分离职责                        | Widget 负责 UI 配置，State 负责状态和逻辑 |

这是一种经典的“描述 ➕ 控制”分离的设计思路，保证结构清晰，状态稳定。

------

#### 🪄 实例对比：计数器

StatelessWidget 版本（错误地尝试保存状态）：

```dart
class CounterWrong extends StatelessWidget {
  int counter = 0;

  @override
  Widget build(BuildContext context) {
    return Text('$counter'); // 永远是 0
  }
}
```

每次 build 都是新对象，counter 永远是 0。

StatefulWidget 版本（正确）：

```dart
class CounterRight extends StatefulWidget {
  @override
  _CounterRightState createState() => _CounterRightState();
}

class _CounterRightState extends State<CounterRight> {
  int counter = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('$counter'),
        ElevatedButton(
          onPressed: () => setState(() {
            counter++;
          }),
          child: Text('Add'),
        ),
      ],
    );
  }
}
```

------

#### 🔚 总结对比

| 维度           | StatelessWidget  | StatefulWidget             |
| -------------- | ---------------- | -------------------------- |
| 是否可保存状态 | ❌ 不可           | ✅ 可                       |
| 用途           | 固定展示，性能好 | 动态交互，管理状态         |
| 生命周期       | 只有 `build`     | 多个完整生命周期方法       |
| 状态管理       | 无需             | 使用 `State` 与 `setState` |
| 性能           | 更优             | 稍高开销（但很合理）       |

------

