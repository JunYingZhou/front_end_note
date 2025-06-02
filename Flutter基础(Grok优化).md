# 📘 Flutter 基础笔记（详细版）

## 📦 一、Dart 基础

### 🛠️ 1. 安装 Flutter SDK

Flutter 的安装需要配置环境，特别是在国内网络环境下，建议使用镜像以加速下载。

- **通过国内镜像安装**：
  - 访问 [清华大学 TUNA 协会镜像](https://flutter.cn/community/china#清华大学-tuna-协会)，获取 Flutter SDK。
  - 国内镜像可以有效避免网络问题，确保下载速度。
- **设置环境变量**：
  1. 下载 Flutter SDK 压缩包。
  2. 解压后，将 `flutter/bin` 目录路径添加到系统环境变量中（Windows 用户可编辑 PATH，macOS/Linux 用户可编辑 `.bashrc` 或 `.zshrc`）。
  3. 在终端运行以下命令以下载依赖：
     ```powershell
     flutter
     ```
- **验证安装**：
  - 检查版本号：
    ```powershell
    flutter --version
    ```
    这将显示 Flutter 的当前版本，例如 `Flutter 3.16.0`。
  - 运行 `flutter doctor` 检查环境：
    ```powershell
    flutter doctor
    ```
    该命令会检测是否存在问题（如缺少 Android SDK、Dart SDK 等），并提供修复建议。

### ⚙️ 2. 编译模式

Dart 支持两种编译模式：**JIT（即时编译）** 和 **AOT（提前编译）**，分别适用于开发和生产环境。

#### **JIT（Just-In-Time）编译**
- **特点**：
  - 在程序运行时将 Dart 代码动态编译为机器码。
  - 支持 **热重载（Hot Reload）**，开发者可快速预览代码修改效果。
  - 允许动态反射和运行时类型检查，灵活性高。
  - 由于运行时编译，启动时间稍长，性能不如 AOT。
- **使用场景**：
  - 开发阶段：通过 `flutter run` 命令运行应用，默认使用 JIT 模式。
  - 热重载功能让开发者可以快速调试和调整 UI。
- **适用平台**：
  - Flutter 应用的开发阶段，例如在模拟器或真机上运行调试。

#### **AOT（Ahead-Of-Time）编译**
- **特点**：
  - 在发布前将 Dart 代码编译为高效的机器码。
  - 启动时间快，运行时性能接近原生应用。
  - 为了优化性能，动态特性（如反射）会被限制。
  - 预编译的机器码会导致生成文件体积稍大。
- **使用场景**：
  - 生产环境：用于发布高性能的应用。
  - 提供更流畅的用户体验，适合最终用户使用。
- **适用平台**：
  - Flutter 应用的发布阶段，通过 `flutter build` 命令生成 APK 或 IPA 文件。

#### **对比总结**

| **特性**     | **JIT**                  | **AOT**                          |
|--------------|--------------------------|----------------------------------|
| **编译时间** | 运行时即时编译           | 预先编译                         |
| **性能**     | 启动时间慢，运行性能稍低 | 启动快，运行效率高               |
| **文件体积** | 较小（无预编译机器码）   | 较大（包含机器码）               |
| **调试支持** | 支持动态反射和热重载     | 不支持动态反射，适合优化后代码   |
| **适用场景** | 开发阶段                 | 生产阶段                         |

#### **Flutter 示例**
- **开发阶段（JIT 模式）**：
  ```powershell
  flutter run
  ```
  - 运行后，支持热重载，开发者可实时查看 UI 修改效果。
  - 适合快速迭代和调试。
- **生产阶段（AOT 模式）**：
  ```powershell
  flutter build apk
  flutter build ios
  ```
  - 生成 Android APK 或 iOS IPA 文件，适用于发布到应用商店。

#### **选择建议**
- **开发阶段**：使用 JIT 模式，利用热重载快速调试。
- **生产阶段**：使用 AOT 模式，确保性能和用户体验。
- Dart 的双模式设计让开发者在开发和部署之间灵活切换。

---

## 🏗️ 二、Flutter 基础

### 🆕 1. 创建 Flutter 项目

Flutter 项目可以通过 IDE 或命令行创建，以下以 Android Studio 为例。

- **步骤**：
  1. 在 Android Studio 中安装 Flutter 插件：
     - 打开 `File > Settings > Plugins`，搜索并安装 `Flutter`。
     - 安装后会自动安装 Dart 插件。
  2. 创建新项目：
     - 选择 `File > New > New Flutter Project`，按照向导完成项目创建。
  - **解决国内下载慢问题**：
    - 由于网络限制，Flutter 依赖下载可能较慢，建议配置国内镜像。
    - 参考 [Flutter 配置 Gradle 镜像](https://blog.csdn.net/qianxiamuxin/article/details/134322224)，修改 `android/build.gradle` 和 `flutter.gradle` 文件，使用国内镜像源（如阿里云镜像）。
- **项目目录结构**：
  - `lib/`：存放 Dart 代码，主要开发目录。
  - `android/`：Android 原生代码。
  - `ios/`：iOS 原生代码。
  - `pubspec.yaml`：项目配置文件，管理依赖和资源。

### 🧩 2. Flutter 小组件（Widget）

Flutter 的核心是 **Widget**，一切界面元素都由 Widget 构建。Widget 具有不可变性、树形结构和高度可组合的特点。

#### **Widget 的特点**
- **不可变性**：Widget 一旦创建，其属性不可更改。UI 更新通过重建 Widget 实现。
- **树形结构**：所有 Widget 组成 Widget 树，Flutter 通过树结构管理和渲染界面。
- **组合性**：通过嵌套多个简单 Widget，可以构建复杂的 UI。

#### **Widget 分类**
##### **a) 基础 Widget**
- **布局相关**：
  - `Container`：多用途容器，支持边距、填充、边框、背景色等。
  - `Row`：水平布局。
  - `Column`：垂直布局。
  - `Stack`：堆叠布局，子 Widget 可重叠。
  - `Expanded`、`Flexible`：控制子 Widget 的伸缩行为。
- **文本与图像**：
  - `Text`：显示普通文本。
  - `RichText`：显示富文本，支持多样式。
  - `Image`：显示图片，支持网络和本地资源。

##### **b) 输入 Widget**
- `TextField`：文本输入框。
- `Checkbox`：复选框。
- `Radio`：单选按钮。
- `Switch`：开关。
- `Slider`：滑块。
- **按钮系列**：
  - `ElevatedButton`：浮起效果按钮。
  - `TextButton`：扁平按钮。
  - `IconButton`：图标按钮。
  - `FloatingActionButton`：悬浮按钮。

##### **c) 布局 Widget**
- **容器类**：
  - `Padding`：设置内边距。
  - `Center`：居中显示子 Widget。
  - `Align`：自定义对齐方式。
  - `SizedBox`：固定尺寸容器。
- **列表类**：
  - `ListView`：可滚动列表。
  - `GridView`：网格布局。
  - `SingleChildScrollView`：单子 Widget 滚动视图。

##### **d) 可交互 Widget**
- `GestureDetector`：监听手势（点击、滑动、长按等）。
- `InkWell`：带涟漪效果的点击区域。
- `Draggable` 和 `DragTarget`：实现拖拽功能。

##### **e) 功能性 Widget**
- `Scaffold`：提供基本布局结构（AppBar、Drawer、FloatingActionButton 等）。
- `AppBar`：顶部导航栏。
- `BottomNavigationBar`：底部导航栏。
- `TabBar` 和 `TabBarView`：标签栏和页面切换。
- `Drawer`：侧边抽屉。
- `SnackBar`：临时消息提示。
- `Dialog` 和 `AlertDialog`：弹出对话框。

#### **Widget 生命周期**
Flutter Widget 分为两类：
- **有状态（StatefulWidget）**：
  - 拥有状态，可动态更新。
  - 需要实现 `createState` 方法，返回 `State` 对象。
  - 适合动态界面（计数器、表单等）。
- **无状态（StatelessWidget）**：
  - 无状态，构造后不变。
  - 适合静态界面（标题、图标等）。

#### **示例：简单界面**
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
        appBar: AppBar(title: Text('Flutter Widgets')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('Hello, Flutter!'),
              ElevatedButton(
                onPressed: () => print('Button Pressed'),
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

#### **使用技巧**
- **热重载**：通过 `flutter run` 启动应用，修改代码后按 `r` 触发热重载，实时查看效果。
- **Flutter Inspector**：在 IDE 中使用 Flutter Inspector 检查 Widget 树，调试布局。
- **组合优先**：优先通过组合简单 Widget 构建复杂 UI，而不是从头实现。

### 🎨 3. 样式与字体

#### **修改字体样式**
通过 `TextStyle` 自定义字体样式：
```dart
Text(
  '解谜之印',
  style: TextStyle(
    fontSize: 20.0,
    fontWeight: FontWeight.bold,
    letterSpacing: 2.0,
    color: Colors.white,
    fontFamily: 'RubikVinyl',
  ),
)
```
- `fontSize`：字体大小。
- `fontWeight`：字体粗细。
- `letterSpacing`：字符间距。
- `color`：字体颜色。
- `fontFamily`：字体家族。

#### **使用自定义字体**
1. 在项目根目录创建 `fonts` 文件夹，将字体文件（如 `RubikVinyl-Regular.ttf`）放入其中。
2. 在 `pubspec.yaml` 中配置字体：
   ```yaml
   flutter:
     fonts:
       - family: RubikVinyl
         fonts:
           - asset: fonts/RubikVinyl-Regular.ttf
   ```
3. 在 `TextStyle` 中通过 `fontFamily` 指定字体。

#### **字体资源**
- 可在 [Google Fonts](https://fonts.google.com) 下载免费字体，支持多种样式。

### 🖼️ 4. 图像与静态资源

Flutter 支持加载网络图片和本地图片，分别使用 `NetworkImage` 和 `AssetImage`。

#### **NetworkImage**
- **用途**：加载网络图片。
- **特点**：
  - 来源于 URL，支持动态加载。
  - 可能因网络问题导致加载延迟或失败。
  - 可通过 `loadingBuilder` 和 `errorBuilder` 处理加载和错误状态。
- **示例**：
  ```dart
  Image.network(
    'https://example.com/your-image.jpg',
    loadingBuilder: (context, child, loadingProgress) {
      if (loadingProgress == null) return child;
      return Center(
        child: CircularProgressIndicator(
          value: loadingProgress.expectedTotalBytes != null
              ? loadingProgress.cumulativeBytesLoaded / (loadingProgress.expectedTotalBytes ?? 1)
              : null,
        ),
      );
    },
    errorBuilder: (context, error, stackTrace) => Text('图片加载失败'),
  )
  ```

#### **AssetImage**
- **用途**：加载本地资源图片。
- **特点**：
  - 图片存储在项目目录，加载速度快。
  - 需要在 `pubspec.yaml` 中声明。
  - 不依赖网络，稳定性高。
- **配置步骤**：
  1. 在项目根目录创建 `assets/images` 文件夹，存放图片（如 `your-image.png`）。
  2. 在 `pubspec.yaml` 中声明：
     ```yaml
     flutter:
       assets:
         - assets/images/your-image.png
     ```
  3. 使用 `Image.asset` 加载：
     ```dart
     Image.asset('assets/images/your-image.png')
     ```

#### **对比总结**

| **特性**       | **NetworkImage**                     | **AssetImage**                  |
|----------------|--------------------------------------|---------------------------------|
| **来源**       | 网络 URL                            | 本地资源                        |
| **优点**       | 动态加载，适合远程图片              | 本地加载，速度快，无需网络依赖  |
| **缺点**       | 依赖网络，可能加载失败或速度慢      | 需要提前打包到应用中            |
| **使用场景**   | 头像、API 返回的图片                | 图标、背景图、固定资源          |
| **加载时效果** | 支持 `loadingBuilder` 和 `errorBuilder` | 无特殊效果                     |

### 🖱️ 5. 图标与按钮

#### **Icon**
- **用途**：显示矢量图标，符合 Material Design 风格。
- **特点**：
  - 通过 `Icons` 类访问 Flutter 内置图标（如 `Icons.favorite`）。
  - 支持自定义大小、颜色和样式。
- **示例**：
  ```dart
  Icon(
    Icons.favorite,
    color: Colors.red,
    size: 50.0,
    semanticLabel: 'Favorite Icon',
  )
  ```
  - `color`：设置图标颜色。
  - `size`：设置图标大小。
  - `semanticLabel`：为无障碍功能提供描述。

#### **Button**
Flutter 提供多种按钮类型，满足不同交互需求。

##### **ElevatedButton**
- 浮起效果按钮，适合主要操作。
  ```dart
  ElevatedButton(
    onPressed: () => print('按钮被点击！'),
    child: Text('Elevated Button'),
  )
  ```

##### **TextButton**
- 扁平按钮，适合次要操作。
  ```dart
  TextButton(
    onPressed: () => print('TextButton 被点击！'),
    child: Text('Text Button'),
  )
  ```

##### **IconButton**
- 图标按钮，适合操作栏或列表项。
  ```dart
  IconButton(
    icon: Icon(Icons.thumb_up),
    color: Colors.blue,
    onPressed: () => print('IconButton 被点击！'),
  )
  ```

##### **FloatingActionButton**
- 悬浮按钮，突出主要操作。
  ```dart
  FloatingActionButton(
    onPressed: () => print('FloatingActionButton 被点击！'),
    child: Icon(Icons.add),
  )
  ```

##### **图标与按钮组合**
- 使用 `ElevatedButton.icon` 组合图标和文本：
  ```dart
  ElevatedButton.icon(
    onPressed: () => print('带图标的按钮被点击！'),
    icon: Icon(Icons.send, color: Colors.white),
    label: Text('发送'),
  )
  ```

#### **对比总结**

| **特性**     | **Icon**                           | **Button**                                   |
|--------------|------------------------------------|----------------------------------------------|
| **用途**     | 显示静态或装饰性图标               | 提供用户交互功能                             |
| **常见实现** | `Icon`, `ImageIcon`                | `ElevatedButton`, `TextButton`, `IconButton` |
| **支持交互** | 不支持（需外部包裹按钮实现）       | 支持点击、长按等交互                         |

### 📏 6. Container 与 Padding

#### **Container**
- **用途**：通用布局容器，支持多种样式和布局属性。
- **常见属性**：
  - `width`、`height`：设置尺寸。
  - `padding`：内边距。
  - `margin`：外边距。
  - `decoration`：装饰（如背景色、边框、阴影）。
  - `alignment`：子 Widget 对齐方式。
- **示例**：
  ```dart
  Container(
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
    child: Text('我是一个 Container', style: TextStyle(color: Colors.white, fontSize: 16)),
  )
  ```

#### **Padding**
- **用途**：专门设置内边距。
- **常见属性**：
  - `padding`：使用 `EdgeInsets` 指定内边距。
- **示例**：
  ```dart
  Padding(
    padding: EdgeInsets.all(16),
    child: Container(
      color: Colors.blue,
      child: Text('我是一个带有 Padding 的 Container', style: TextStyle(color: Colors.white)),
    ),
  )
  ```

#### **对比总结**

| **特性**     | **Container**                            | **Padding**                        |
|--------------|------------------------------------------|------------------------------------|
| **功能**     | 多功能容器，支持尺寸、装饰等             | 仅用于设置内边距                   |
| **主要用途** | 布局、装饰、设置尺寸、对齐等             | 调整子 Widget 与父组件之间的间距   |
| **性能**     | 功能多，相对较重                         | 专注于内边距，性能更轻             |
| **常用场景** | 复杂布局和样式                           | 简单间距调整                       |

#### **性能建议**
- 如果仅需设置内边距，使用 `Padding` 更高效。
- `Container` 适合需要多种样式和布局属性的场景。

### ↔️ 7. Rows

#### **Row 组件**
- **用途**：水平排列子 Widget。
- **常见属性**：
  - `children`：子 Widget 列表。
  - `mainAxisAlignment`：主轴（水平）对齐方式。
  - `crossAxisAlignment`：交叉轴（垂直）对齐方式。
  - `mainAxisSize`：主轴空间占用（`max` 或 `min`）。
  - `textDirection`：文本方向（支持多语言布局）。
  - `verticalDirection`：垂直排列方向。

#### **对齐方式**
- **MainAxisAlignment**：
  - `start`：从左开始。
  - `center`：居中。
  - `end`：从右开始。
  - `spaceBetween`：子 Widget 间均匀分布，首尾无间距。
  - `spaceAround`：子 Widget 间均匀分布，首尾有间距。
  - `spaceEvenly`：子 Widget 间和首尾间距相等。
- **CrossAxisAlignment**：
  - `start`：顶部对齐。
  - `center`：垂直居中。
  - `end`：底部对齐。
  - `stretch`：拉伸填满交叉轴。

#### **基础示例**
```dart
Row(
  children: [
    Icon(Icons.star, size: 50, color: Colors.orange),
    Icon(Icons.star, size: 50, color: Colors.orange),
    Icon(Icons.star, size: 50, color: Colors.orange),
  ],
)
```

#### **主轴对齐示例**
```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    Icon(Icons.star, size: 50, color: Colors.orange),
    Icon(Icons.star, size: 50, color: Colors.orange),
    Icon(Icons.star, size: 50, color: Colors.orange),
  ],
)
```

#### **交叉轴对齐示例**
```dart
Row(
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    Icon(Icons.star, size: 50, color: Colors.orange),
    Container(width: 20),
    Icon(Icons.star, size: 100, color: Colors.orange),
    Container(width: 20),
    Icon(Icons.star, size: 75, color: Colors.orange),
  ],
)
```

#### **结合 Expanded**
```dart
Row(
  children: [
    Expanded(
      child: Container(
        color: Colors.red,
        height: 50,
        child: Center(child: Text('Box 1')),
      ),
    ),
    Expanded(
      child: Container(
        color: Colors.green,
        height: 50,
        child: Center(child: Text('Box 2')),
      ),
    ),
    Expanded(
      child: Container(
        color: Colors.blue,
        height: 50,
        child: Center(child: Text('Box 3')),
      ),
    ),
  ],
)
```

#### **总结**
- `Row` 适用于水平排列布局。
- 使用 `Expanded` 分配剩余空间，避免溢出。
- 通过 `MainAxisAlignment` 和 `CrossAxisAlignment` 灵活控制对齐。

### ↕️ 8. Column

#### **Column 组件**
- **用途**：垂直排列子 Widget。
- **常见属性**：
  - `mainAxisAlignment`：主轴（垂直）对齐方式。
  - `crossAxisAlignment`：交叉轴（水平）对齐方式。
  - `mainAxisSize`：主轴空间占用。
  - `children`：子 Widget 列表。

#### **对齐方式**
- **MainAxisAlignment**：
  - `start`：顶部对齐。
  - `center`：垂直居中。
  - `end`：底部对齐。
  - `spaceBetween`：子 Widget 间均匀分布。
  - `spaceAround`：子 Widget 间均匀分布，首尾有间距。
  - `spaceEvenly`：子 Widget 间和首尾间距相等。
- **CrossAxisAlignment**：
  - `start`：左侧对齐。
  - `center`：水平居中。
  - `end`：右侧对齐。
  - `stretch`：拉伸填满水平空间。

#### **基础示例**
```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    Text('Item 1'),
    Text('Item 2'),
    ElevatedButton(onPressed: () {}, child: Text('Button')),
  ],
)
```

#### **带间距的布局**
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

#### **总结**
- `Column` 适用于垂直排列布局。
- 使用 `MainAxisAlignment` 和 `CrossAxisAlignment` 控制对齐。
- 常用于表单、列表等垂直布局场景。

### 📏 9. Expanded

#### **Expanded 组件**
- **用途**：扩展子 Widget，填充父组件的可用空间。
- **特点**：
  - 仅适用于 `Row`、`Column` 或 `Flex` 布局。
  - 多个 `Expanded` 可通过 `flex` 属性按比例分配空间。

#### **基础用法**
```dart
Column(
  children: [
    Container(color: Colors.red, height: 100),
    Expanded(child: Container(color: Colors.green)),
    Container(color: Colors.blue, height: 100),
  ],
)
```
- 绿色容器会填充剩余垂直空间。

#### **比例分配**
```dart
Column(
  children: [
    Expanded(flex: 2, child: Container(color: Colors.red)),
    Expanded(flex: 1, child: Container(color: Colors.green)),
    Expanded(flex: 3, child: Container(color: Colors.blue)),
  ],
)
```
- 红色、绿色、蓝色容器按 2:1:3 比例分配空间。

#### **结合 Spacer**
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
- `Spacer` 用于插入空白区域，按比例分配。

#### **注意事项**
- `Expanded` 只能用于 Flex 布局。
- 嵌套时可结合 `SizedBox` 限制尺寸。

### 🔄 10. StatelessWidget

#### **特点**
- **不可变性**：构造后状态不可变。
- **高性能**：无需状态管理，渲染效率高。
- **依赖外部参数**：UI 由构造函数参数决定。

#### **生命周期**
- **build()**：唯一生命周期方法，定义 UI。
  ```dart
  @override
  Widget build(BuildContext context) {
    return Text('Hello StatelessWidget');
  }
  ```

#### **示例**
```dart
import 'package:flutter/material.dart';

class MyStatelessWidget extends StatelessWidget {
  final String title;

  const MyStatelessWidget({required this.title, super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text(title)),
      body: Center(
        child: Text('这是一个 StatelessWidget 示例', style: TextStyle(fontSize: 18)),
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

#### **构成解析**
- **final 属性**：属性不可变，使用 `final` 修饰。
- **build 方法**：描述 UI，每次重绘时调用。
- **参数更新**：通过构造函数传递参数，外部数据变化时重建。

#### **使用场景**
- 静态内容：标题、图标、固定文本等。
- 无需内部状态管理：内容随父组件参数变化。

### 🔄 11. StatefulWidget

#### **特点**
- **动态更新**：通过状态管理响应用户交互。
- **分离状态**：状态由 `State` 类管理，`StatefulWidget` 本身不可变。
- **重绘机制**：调用 `setState` 触发 UI 重建。

#### **创建方式**
```dart
import 'package:flutter/material.dart';

class MyStatefulWidget extends StatefulWidget {
  const MyStatefulWidget({super.key});

  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() => _counter++);
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Counter: $_counter'),
        ElevatedButton(
          onPressed: _incrementCounter,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

#### **生命周期**
- **initState**：初始化状态。
  ```dart
  @override
  void initState() {
    super.initState();
    print('State initialized');
  }
  ```
- **didChangeDependencies**：依赖项变化时调用。
- **build**：构建 UI。
- **setState**：更新状态。
- **didUpdateWidget**：父组件更新时调用。
- **deactivate**：状态暂时移除时调用。
- **dispose**：组件销毁时调用。
  ```dart
  @override
  void dispose() {
    super.dispose();
    print('State disposed');
  }
  ```

#### **使用场景**
- 动态内容：计数器、表单输入、动画等。
- 复杂交互：页面切换、动态列表。

#### **完整示例：计数器**
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: CounterPage());
  }
}

class CounterPage extends StatefulWidget {
  @override
  _CounterPageState createState() => _CounterPageState();
}

class _CounterPageState extends State<CounterPage> {
  int counter = 0;

  void incrementCounter() {
    setState(() => counter++);
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

#### **注意事项**
- 使用 `setState` 更新状态，避免频繁调用。
- `build` 方法保持简洁，复杂逻辑抽取到其他方法。
- 在 `dispose` 中释放资源，避免内存泄漏。

### 📜 12. ListView

#### **常用属性**
- **children**：静态列表内容。
  ```dart
  ListView(
    children: [
      ListTile(title: Text('Item 1')),
      ListTile(title: Text('Item 2')),
    ],
  )
  ```
- **builder**：动态构建列表。
  ```dart
  ListView.builder(
    itemCount: 10,
    itemBuilder: (context, index) => ListTile(title: Text('Item $index')),
  )
  ```
- **itemCount**：列表项数量。
- **scrollDirection**：滚动方向（`Axis.vertical` 或 `Axis.horizontal`）。
- **padding**：内边距。
- **shrinkWrap**：根据内容调整大小。
- **reverse**：反向排列。

#### **常用方法**
- **scrollTo**：使用 `ScrollController` 控制滚动。
  ```dart
  final controller = ScrollController();
  ListView.builder(
    controller: controller,
    itemCount: 10,
    itemBuilder: (context, index) => ListTile(title: Text('Item $index')),
  );
  controller.jumpTo(100.0);
  ```
- **animateTo**：平滑滚动。
  ```dart
  controller.animateTo(
    100.0,
    duration: Duration(seconds: 1),
    curve: Curves.ease,
  );
  ```

#### **ListTile 属性**
- `leading`：前置控件。
- `title`：主标题。
- `subtitle`：副标题。
- `trailing`：后置控件。
  ```dart
  ListTile(
    leading: Icon(Icons.check),
    title: Text('Item 1'),
    subtitle: Text('This is the subtitle'),
    trailing: Icon(Icons.arrow_forward),
  )
  ```

#### **子类**
- **ListView.builder**：懒加载列表。
- **ListView.separated**：带分隔符。
  ```dart
  ListView.separated(
    itemCount: 10,
    itemBuilder: (context, index) => ListTile(title: Text('Item $index')),
    separatorBuilder: (context, index) => Divider(),
  )
  ```
- **ListView.custom**：自定义列表。

#### **总结**
- `ListView` 适用于滚动列表场景。
- 使用 `builder` 优化性能，`separated` 添加分隔符。

### 🃏 13. Card

#### **特点**
- **圆角与阴影**：默认带圆角和轻微阴影。
- **背景色**：默认使用 Material 风格的 `surface` 颜色。
- **裁剪行为**：支持裁剪子 Widget。
- **自定义形状**：通过 `shape` 属性设置。

#### **属性**
- `color`：背景颜色。
- `elevation`：阴影深度。
- `margin`：外边距。
- `shape`：形状（如 `RoundedRectangleBorder`）。
- `clipBehavior`：裁剪行为。
- `child`：子 Widget。

#### **基础用法**
- **简单卡片**：
  ```dart
  Card(
    child: Padding(
      padding: EdgeInsets.all(16.0),
      child: Text('Hello, Flutter!'),
    ),
  )
  ```
- **自定义形状与阴影**：
  ```dart
  Card(
    elevation: 8.0,
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(15.0)),
    child: Padding(
      padding: EdgeInsets.all(16.0),
      child: Text('Custom shaped Card!'),
    ),
  )
  ```
- **设置背景颜色**：
  ```dart
  Card(
    color: Colors.blue[50],
    elevation: 4,
    child: Padding(
      padding: EdgeInsets.all(16.0),
      child: Text('Card with custom color!'),
    ),
  )
  ```

#### **进阶用法**
- **嵌套复杂组件**：
  ```dart
  Card(
    elevation: 6,
    margin: EdgeInsets.all(10),
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
    child: Column(
      mainAxisSize: MainAxisSize.min,
      children: [
        ListTile(
          leading: Icon(Icons.album, size: 50),
          title: Text('Card Title'),
          subtitle: Text('This is a subtitle'),
        ),
        ButtonBar(
          children: [
            TextButton(onPressed: () {}, child: Text('ACTION 1')),
            TextButton(onPressed: () {}, child: Text('ACTION 2')),
          ],
        ),
      ],
    ),
  )
  ```
- **裁剪内容**：
  ```dart
  Card(
    clipBehavior: Clip.antiAlias,
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(15)),
    child: Column(
      children: [
        Image.network('https://via.placeholder.com/150'),
        Padding(
          padding: EdgeInsets.all(16.0),
          child: Text('Card with clipped image!'),
        ),
      ],
    ),
  )
  ```
- **动态生成**：
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

#### **常见搭配**
- **ListView**：用于列表项展示。
- **GridView**：网格布局中展示卡片。
- **InkWell**：添加点击效果。
  ```dart
  Card(
    elevation: 4,
    child: InkWell(
      onTap: () => print('Card tapped!'),
      child: Padding(
        padding: EdgeInsets.all(16.0),
        child: Text('Tap me!'),
      ),
    ),
  )
  ```

#### **完整示例**
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
                onTap: () => print('${items[index]} tapped!'),
              ),
            );
          },
        ),
      ),
    );
  }
}
```

#### **总结**
- `Card` 适用于信息块展示，支持复杂内容。
- 通过 `shape` 和 `elevation` 自定义样式。

### 📚 14. Stack

#### **特点**
- **子组件堆叠**：子 Widget 按声明顺序从底到顶排列。
- **定位布局**：通过 `Positioned` 或 `Align` 控制位置。
- **灵活性**：支持复杂 UI 布局。

#### **属性**
- `alignment`：未定位子 Widget 的对齐方式。
- `fit`：子 Widget 填充方式。
- `clipBehavior`：裁剪行为。
- `children`：子 Widget 列表。

#### **基础用法**
- **简单堆叠**：
  ```dart
  Stack(
    children: [
      Container(width: 200, height: 200, color: Colors.blue),
      Container(width: 150, height: 150, color: Colors.red),
      Container(width: 100, height: 100, color: Colors.green),
    ],
  )
  ```
- **使用 Positioned**：
  ```dart
  Stack(
    children: [
      Container(width: 200, height: 200, color: Colors.blue),
      Positioned(
        top: 50,
        left: 50,
        child: Container(width: 100, height: 100, color: Colors.red),
      ),
      Positioned(
        bottom: 20,
        right: 20,
        child: Container(width: 50, height: 50, color: Colors.green),
      ),
    ],
  )
  ```
- **使用 alignment**：
  ```dart
  Stack(
    alignment: Alignment.center,
    children: [
      Container(width: 200, height: 200, color: Colors.blue),
      Container(width: 100, height: 100, color: Colors.red),
    ],
  )
  ```

#### **高级用法**
- **图文叠加**：
  ```dart
  Stack(
    alignment: Alignment.bottomCenter,
    children: [
      Image.network('https://via.placeholder.com/300', width: 300, height: 200, fit: BoxFit.cover),
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
- **动态徽章**：
  ```dart
  Stack(
    children: [
      Icon(Icons.shopping_cart, size: 100),
      Positioned(
        top: 5,
        right: 5,
        child: Container(
          padding: EdgeInsets.all(4),
          decoration: BoxDecoration(color: Colors.red, shape: BoxShape.circle),
          child: Text('3', style: TextStyle(color: Colors.white, fontSize: 12)),
        ),
      ),
    ],
  )
  ```
- **全屏布局**：
  ```dart
  Stack(
    fit: StackFit.expand,
    children: [
      Container(color: Colors.blue),
      Align(
        alignment: Alignment.topCenter,
        child: Text('Top Text', style: TextStyle(color: Colors.white, fontSize: 24)),
      ),
      Align(
        alignment: Alignment.bottomCenter,
        child: Text('Bottom Text', style: TextStyle(color: Colors.white, fontSize: 24)),
      ),
    ],
  )
  ```

#### **注意事项**
- 避免过多复杂子 Widget，影响性能。
- 使用 `clipBehavior` 裁剪超出部分。
- 父组件尺寸可能限制子 Widget 布局。

#### **总结**
- `Stack` 适用于需要重叠布局的场景。
- 通过 `Positioned` 和 `Align` 精确控制位置。

---

## 📋 补充

### 📡 1. 数据监听（ValueNotifier）

#### **简介**
- `ValueNotifier` 实现 `ValueListenable` 接口，用于监听值变化。
- 适合局部 UI 更新，避免 `setState` 导致全局重绘。

#### **用法**
- **创建**：
  ```dart
  ValueNotifier<int> counter = ValueNotifier<int>(0);
  ```
- **修改值**：
  ```dart
  counter.value = 5;
  ```
- **监听变化**：
  ```dart
  ValueListenableBuilder<int>(
    valueListenable: counter,
    builder: (context, value, child) => Text('Counter value: $value'),
  )
  ```

#### **示例：计数器**
```dart
class CounterApp extends StatefulWidget {
  @override
  _CounterAppState createState() => _CounterAppState();
}

class _CounterAppState extends State<CounterApp> {
  final ValueNotifier<int> _counter = ValueNotifier<int>(0);

  void _incrementCounter() => _counter.value++;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter App')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ValueListenableBuilder<int>(
              valueListenable: _counter,
              builder: (context, value, child) => Text('Counter: $value', style: TextStyle(fontSize: 30)),
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

#### **示例：进度条**
```dart
class ProgressApp extends StatelessWidget {
  final ValueNotifier<double> _progressNotifier = ValueNotifier<double>(0.0);

  void _incrementProgress() {
    if (_progressNotifier.value < 1.0) _progressNotifier.value += 0.1;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Progress Example')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ValueListenableBuilder<double>(
              valueListenable: _progressNotifier,
              builder: (context, progress, child) => Column(
                children: [
                  LinearProgressIndicator(value: progress),
                  SizedBox(height: 20),
                  Text('${(progress * 100).toStringAsFixed(0)}%'),
                ],
              ),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _incrementProgress,
              child: Text('Increment Progress'),
            ),
          ],
        ),
      ),
    );
  }
}
```

#### **优点**
- 高效更新：仅更新监听部分。
- 解耦：数据和 UI 分离。
- 简单易用：适合小型状态管理。

#### **注意事项**
- 避免在 `builder` 中执行复杂计算。
- 对于复杂状态管理，考虑使用 `Provider` 或 `Bloc`。

### ✍️ 2. 文本编辑器（TextEditingController）

#### **简介**
- `TextEditingController` 用于管理 `TextField` 或 `TextFormField` 的内容。
- 支持获取、设置、监听文本变化。

#### **用法**
- **创建**：
  ```dart
  final controller = TextEditingController(text: 'Initial Text');
  ```
- **绑定**：
  ```dart
  TextField(
    controller: controller,
    decoration: InputDecoration(hintText: 'Enter something'),
  )
  ```
- **监听变化**：
  ```dart
  controller.addListener(() => print('Current text: ${controller.text}'));
  ```

#### **示例：简单输入**
```dart
class MyTextFieldApp extends StatefulWidget {
  @override
  _MyTextFieldAppState createState() => _MyTextFieldAppState();
}

class _MyTextFieldAppState extends State<MyTextFieldApp> {
  final TextEditingController _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('TextEditingController Example')),
      body: Padding(
        padding: EdgeInsets.all(20.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: InputDecoration(hintText: 'Enter something'),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () => print('Text entered: ${_controller.text}'),
              child: Text('Print Text'),
            ),
          ],
        ),
      ),
    );
  }
}
```

#### **示例：表单**
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
        padding: EdgeInsets.all(20.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _controller,
                decoration: InputDecoration(hintText: 'Enter something'),
                validator: (value) => value?.isEmpty ?? true ? 'Please enter some text' : null,
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () {
                  if (_formKey.currentState?.validate() ?? false) {
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

#### **常用操作**
- **清空**：`controller.clear()`
- **设置光标**：
  ```dart
  controller.selection = TextSelection.fromPosition(TextPosition(offset: 5));
  ```

#### **注意事项**
- 在 `dispose` 中释放控制器：
  ```dart
  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
  ```
- 不直接触发 UI 更新，需结合 `setState` 或其他状态管理。

### 🛠️ 3. GetX

#### **简介**
- GetX 是一个轻量级状态管理、路由管理和依赖注入工具。
- 特点：简单高效，支持响应式状态管理。

#### **集成**
- 在 `pubspec.yaml` 中添加依赖：
  ```yaml
  dependencies:
    get: ^4.6.5
  ```
- 导入：
  ```dart
  import 'package:get/get.dart';
  ```

#### **状态管理**
- **响应式变量**：
  ```dart
  class CounterController extends GetxController {
    var count = 0.obs;

    void increment() => count++;
  }
  ```
- **监听变化**：
  ```dart
  Obx(() => Text('Count: ${controller.count}'))
  ```
- **示例**：
  ```dart
  import 'package:flutter/material.dart';
  import 'package:get/get.dart';

  class CounterController extends GetxController {
    var count = 0.obs;

    void increment() => count++;
  }

  void main() => runApp(MyApp());

  class MyApp extends StatelessWidget {
    final CounterController controller = Get.put(CounterController());

    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          appBar: AppBar(title: Text('GetX Example')),
          body: Center(
            child: Obx(() => Text('Count: ${controller.count}', style: TextStyle(fontSize: 24))),
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

#### **路由管理**
- **无上下文导航**：
  ```dart
  Get.to(DetailPage());
  Get.back();
  ```
- **命名路由**：
  ```dart
  GetMaterialApp(
    initialRoute: '/',
    getPages: [
      GetPage(name: '/', page: () => HomePage()),
      GetPage(name: '/details', page: () => DetailPage()),
    ],
  );
  Get.toNamed('/details');
  ```

#### **依赖注入**
- **注入**：`Get.put(MyController())`
- **懒加载**：`Get.lazyPut(() => MyController())`
- **获取**：`Get.find<MyController>()`

#### **弹窗**
- **Snackbar**：
  ```dart
  Get.snackbar('Title', 'This is a message');
  ```
- **Dialog**：
  ```dart
  Get.defaultDialog(title: 'Dialog Title', content: Text('This is a dialog'));
  ```

#### **总结**
- GetX 适用于中小型项目，简化状态、路由和依赖管理。
- 优点：无上下文导航、响应式状态管理、高效开发。

### ⚖️ 4. 两种组件的区别

#### **StatelessWidget（无状态组件）**
- **定义**：不依赖内部状态，UI 由外部参数决定。
- **特点**：
  - 不可变：构造后状态不变。
  - 高性能：无需状态管理。
  - 依赖外部：通过构造函数参数更新。
- **示例**：
  ```dart
  class GreetingWidget extends StatelessWidget {
    final String name;

    const GreetingWidget({required this.name, super.key});

    @override
    Widget build(BuildContext context) {
      return Text('Hello, $name!');
    }
  }
  ```

#### **StatefulWidget（有状态组件）**
- **定义**：可动态更新，状态由 `State` 类管理。
- **特点**：
  - 动态更新：通过 `setState` 重建 UI。
  - 分离状态：`State` 类管理状态逻辑。
  - 复杂交互：适合动态 UI。
- **示例**：
  ```dart
  class CounterWidget extends StatefulWidget {
    const CounterWidget({super.key});

    @override
    _CounterWidgetState createState() => _CounterWidgetState();
  }

  class _CounterWidgetState extends State<CounterWidget> {
    int _count = 0;

    void _increment() {
      setState(() => _count++);
    }

    @override
    Widget build(BuildContext context) {
      return Column(
        children: [
          Text('Count: $_count'),
          ElevatedButton(onPressed: _increment, child: Text('Add')),
        ],
      );
    }
  }
  ```

#### **为什么这样设计？**
- **性能优化**：
  - `StatelessWidget` 避免不必要重绘。
  - `StatefulWidget` 局部更新状态。
- **职责清晰**：
  - `StatelessWidget` 专注静态渲染。
  - `StatefulWidget` 管理动态交互。
- **响应式模型**：
  - Flutter 核心理念：UI 是状态的函数。
- **灵活性**：
  - 两种组件满足不同场景需求。
- **避免复杂性**：
  - 无需为静态 UI 引入状态管理。

#### **对比总结**

| **特性**       | **StatelessWidget**    | **StatefulWidget**    |
|----------------|------------------------|-----------------------|
| **状态管理**   | 无状态，依赖外部参数   | 有状态，内部管理      |
| **UI 更新**    | 参数变化时重建         | 调用 `setState` 重建  |
| **性能**       | 轻量，适合静态 UI      | 稍重，适合动态 UI     |
| **代码复杂度** | 简单，无需额外类       | 需要 `State` 类       |
| **使用场景**   | 静态文本、图标         | 计数器、表单、动画    |

#### **如何选择？**
- **无状态**：使用 `StatelessWidget`，如标题、图标。
- **有状态**：使用 `StatefulWidget`，如表单、计数器。
- **优化建议**：将大 `StatefulWidget` 拆分为多个小 `StatelessWidget`，减少状态管理范围。

---

## 📝 总结

- **Flutter 核心**：一切皆 Widget，UI 是状态的函数。
- **组件选择**：根据是否需要状态管理选择 `StatelessWidget` 或 `StatefulWidget`。
- **开发流程**：
  1. 安装 Flutter SDK 并配置环境。
  2. 创建项目，熟悉目录结构。
  3. 使用 Widget 构建 UI（如 `Row`、`Column`、`ListView`）。
  4. 管理状态（`ValueNotifier`、`GetX`）。
- **工具推荐**：
  - `GetX`：状态管理、路由管理。
  - `TextEditingController`：文本输入管理。
  - `ValueNotifier`：轻量数据监听。