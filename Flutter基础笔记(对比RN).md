# Flutter 快速上手

## **Flutter 是什么？**

Flutter 是 Google 开发的开源 UI 框架，用于构建高性能、跨平台的原生应用，支持 iOS、Android、Web 和桌面。它使用 Dart 语言，通过 Skia 渲染引擎直接绘制 UI，核心特点包括：

- **跨平台**：一套代码运行在 iOS、Android、Web 和桌面平台。
- **高性能**：编译为原生机器码，性能接近原生应用。
- **热重载**：代码修改后立即刷新 UI，提升开发效率。

Flutter 的组件体系基于 **Widget**，所有 UI 元素（包括布局、文本、图片等）都是 Widget。Flutter 不依赖原生组件，而是通过 Dart 代码直接渲染。

> RN 中的 `ThemedView` 对应 Flutter 的 `Container` 或 `Material` Widget，用于构建基础布局。

---

**Flutter vs. Expo**

Flutter 没有直接类似 RN 的 Expo 托管工具，但它提供了强大的脚手架和插件生态。以下是 Flutter 和 Expo 的对比：

| 特性               | Flutter                            | Expo (RN)                          |
|--------------------|------------------------------------|------------------------------------|
| **入门难度**       | 中等，需要安装 Flutter SDK 和 IDE  | 简单，无需配置原生环境             |
| **开发速度**       | 快速（热重载支持）                 | 快速（热重载、Expo Go 预览）       |
| **功能支持**       | 提供大量官方 Widget 和插件         | 提供大量预构建 API（如相机、地图） |
| **自定义原生代码** | 完全支持（通过 Platform Channels） | 有限（需“弹出”到 bare workflow）   |
| **构建和发布**     | 需手动配置构建流程                 | 托管服务简化流程                   |

---

### **创建 Flutter 项目**

Flutter 使用官方 CLI 工具创建项目：

```bash
flutter create my_app
cd my_app
flutter run
```

> Flutter 不需要类似 Expo 的工具，直接通过 `flutter run` 运行应用，支持热重载。需要在本地安装 Flutter SDK 和 Dart，并配置好 Android Studio 或 Xcode 环境。

---

## 1、常用核心组件

Flutter 的核心组件是 **Widget**，分为无状态（`StatelessWidget`）和有状态（`StatefulWidget`）。以下是 RN 笔记中核心组件的 Flutter 对应实现。

---

### 📝 `Text` 组件

Flutter 中的 `Text` Widget 用于显示文本内容。

✅ 基本用法：

```dart
import 'package:flutter/material.dart';

Text('Hello, Flutter!')
```

✨ 常见属性：

| 属性            | 作用                                         |
|-----------------|----------------------------------------------|
| `style`         | 自定义文字样式（颜色、字体大小等）           |
| `maxLines`      | 限制显示行数，超出部分省略                  |
| `overflow`      | 超出时的处理方式（ellipsis, clip 等）        |
| `textAlign`     | 文本对齐方式（left, center, right 等）       |
| `onTap`         | 点击文字事件（需用 GestureDetector 包裹）    |

🌟 示例（限制一行显示）：

```dart
Text(
  '这是一段很长很长的文字，会被省略……',
  maxLines: 1,
  overflow: TextOverflow.ellipsis,
  style: TextStyle(fontSize: 16),
)
```

> Flutter 不像 RN 要求所有文本必须用 `Text` 包裹，但 `Text` 是显示文本的唯一 Widget。

---

### ⌨️ `TextField` 组件

Flutter 的 `TextField` Widget 用于接收用户输入，类似于 RN 的 `TextInput`。

✅ 基本用法：

```dart
import 'package:flutter/material.dart';

class MyComponent extends StatefulWidget {
  @override
  _MyComponentState createState() => _MyComponentState();
}

class _MyComponentState extends State<MyComponent> {
  final TextEditingController _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return TextField(
      controller: _controller,
      decoration: InputDecoration(
        hintText: '请输入内容',
        border: OutlineInputBorder(),
        contentPadding: EdgeInsets.all(8),
      ),
      onChanged: (value) {
        setState(() {});
      },
    );
  }
}
```

✨ 常见属性：

| 属性              | 作用                                               |
|-------------------|----------------------------------------------------|
| `controller`      | 控制输入框的值                                     |
| `onChanged`       | 输入内容变化时的回调                               |
| `decoration`      | 样式装饰（包含 hintText、border 等）               |
| `obscureText`     | 密码模式（隐藏输入）                               |
| `keyboardType`    | 设置键盘类型（text, number, emailAddress 等）      |
| `maxLines`        | 设置行数（多行输入时用）                           |
| `maxLength`       | 最大输入长度                                       |
| `enabled`         | 是否可编辑                                         |
| `autofocus`       | 是否自动聚焦                                       |

🌟 示例（密码输入框）：

```dart
TextField(
  obscureText: true,
  decoration: InputDecoration(
    hintText: '请输入密码',
    border: OutlineInputBorder(),
    contentPadding: EdgeInsets.all(8),
  ),
)
```

---

🆚 对比总结：

| 功能     | `Text`          | `TextField`            |
|----------|-----------------|------------------------|
| 显示文本 | ✅               | ❌                      |
| 输入文本 | ❌               | ✅                      |
| 支持样式 | ✅               | ✅                      |
| 可点击   | ✅（加 GestureDetector） | ✅                      |
| 状态管理 | ❌               | ✅（需结合 `TextEditingController`） |

---

### 🖼️ `Image` 组件

Flutter 的 `Image` Widget 用于展示图片。

✅ 基本用法：

```dart
Image.network(
  'https://example.com/my-image.jpg',
  width: 100,
  height: 100,
)
```

> Flutter 的 `Image` 必须设置宽高，否则可能不显示。

🗂️ 图片来源：

- 加载**网络图片**：

```dart
Image.network('https://example.com/image.jpg')
```

- 加载**本地图片**（需在 `pubspec.yaml` 中声明）：

```yaml
# pubspec.yaml
flutter:
  assets:
    - assets/logo.png
```

```dart
Image.asset('assets/logo.png')
```

🎯 常见属性：

| 属性            | 说明                           |
|-----------------|-------------------------------|
| `width`         | 图片宽度                      |
| `height`        | 图片高度                      |
| `fit`           | 图片适配方式（详见下方）       |
| `color`         | 图片着色                      |
| `errorBuilder`  | 加载失败时的占位 Widget       |
| `loadingBuilder`| 加载中的占位 Widget           |

🎨 `fit` 适配方式（对应 RN 的 `resizeMode`）：

| 模式          | 效果                               |
|---------------|------------------------------------|
| `BoxFit.cover` | 保持比例填满，超出部分裁剪（默认） |
| `BoxFit.contain` | 保持比例缩放完整显示             |
| `BoxFit.fill`  | 拉伸填满，不保持比例             |
| `BoxFit.fitWidth` | 宽度适配，保持比例              |

**示例**：

```dart
Image.network(
  'https://example.com/image.jpg',
  width: 200,
  height: 200,
  fit: BoxFit.contain,
)
```

🔄 网络图失败占位逻辑：

```dart
Image.network(
  'https://example.com/image.jpg',
  width: 100,
  height: 100,
  errorBuilder: (context, error, stackTrace) {
    return Image.asset('assets/placeholder.png');
  },
  loadingBuilder: (context, child, loadingProgress) {
    if (loadingProgress == null) return child;
    return CircularProgressIndicator();
  },
)
```

🌟 常见场景：

1. 显示头像、背景图、banner 图。
2. 与 `ListView` 组合显示图片列表。
3. 加上点击事件用作按钮背景：

```dart
GestureDetector(
  onTap: () {
    // 点击事件
  },
  child: Image.network('https://example.com/image.jpg'),
)
```

---

### 🖼️ 图片作为背景（类似 RN 的 `ImageBackground`）

Flutter 使用 `Stack` 和 `Image` 组合，或 `Container` 的 `decoration` 实现类似 RN `ImageBackground` 的效果。

✅ 基本用法：

```dart
Stack(
  children: [
    Image.network(
      'https://example.com/bg.jpg',
      width: double.infinity,
      height: 200,
      fit: BoxFit.cover,
    ),
    Center(
      child: Text(
        '我是背景图上的文字',
        style: TextStyle(color: Colors.white, fontSize: 20),
      ),
    ),
  ],
)
```

✨ 常用属性：

Flutter 没有直接的 `ImageBackground` 组件，但可以通过 `Container` 的 `decoration` 设置背景图片：

| 属性            | 说明                              |
|-----------------|-----------------------------------|
| `decoration`    | 设置背景图片、圆角等样式          |
| `child`         | 背景图上的内容                    |

🎯 示例：卡片带背景图 + 圆角：

```dart
Container(
  width: 300,
  height: 150,
  decoration: BoxDecoration(
    borderRadius: BorderRadius.circular(12),
    image: DecorationImage(
      image: NetworkImage('https://example.com/card-bg.jpg'),
      fit: BoxFit.cover,
    ),
  ),
  child: Align(
    alignment: Alignment.bottomLeft,
    child: Padding(
      padding: EdgeInsets.all(16),
      child: Text(
        '卡片标题',
        style: TextStyle(color: Colors.white, fontWeight: FontWeight.bold),
      ),
    ),
  ),
)
```

⚠️ 注意点：
- Flutter 没有直接的 `imageStyle`，但可以通过 `DecorationImage` 设置图片样式。
- 背景图上的内容通过 `child` 嵌套。

🧠 使用场景：
- 登录页/欢迎页的背景图。
- Banner 卡片、活动广告位。
- 视频封面图 + 播放按钮。

---

### 🧭 `SingleChildScrollView` 组件

Flutter 的 `SingleChildScrollView` 对应 RN 的 `ScrollView`，用于可滚动内容。

✅ 基本用法：

```dart
import 'package:flutter/material.dart';

SingleChildScrollView(
  child: Column(
    children: [
      Text('我是可以滚动的内容'),
      // 更多内容...
    ],
  ),
)
```

🧱 常见属性：

| 属性                  | 说明                                   |
|-----------------------|----------------------------------------|
| `scrollDirection`     | 滚动方向（Axis.vertical 或 Axis.horizontal） |
| `reverse`             | 是否反向滚动                           |
| `physics`             | 滚动物理效果（如 BouncingScrollPhysics） |
| `controller`          | 滚动控制器（可用于监听或控制滚动）     |

📦 内容撑满的写法：

```dart
SingleChildScrollView(
  padding: EdgeInsets.all(20),
  child: Column(
    children: [
      Text('内容...'),
    ],
  ),
)
```

🔄 下拉刷新（使用 `RefreshIndicator`）：

```dart
class MyScroll extends StatefulWidget {
  @override
  _MyScrollState createState() => _MyScrollState();
}

class _MyScrollState extends State<MyScroll> {
  bool _isRefreshing = false;

  Future<void> _onRefresh() async {
    setState(() {
      _isRefreshing = true;
    });
    await Future.delayed(Duration(seconds: 2)); // 模拟刷新
    setState(() {
      _isRefreshing = false;
    });
  }

  @override
  Widget build(BuildContext context) {
    return RefreshIndicator(
      onRefresh: _onRefresh,
      child: SingleChildScrollView(
        physics: AlwaysScrollableScrollPhysics(),
        child: Column(
          children: [
            Text('可下拉刷新'),
          ],
        ),
      ),
    );
  }
}
```

⚠️ 使用注意：

| 场景                     | 推荐组件                                     |
|--------------------------|----------------------------------------------|
| 内容较少                 | ✅ `SingleChildScrollView`                    |
| 内容很多（如长列表）     | ❌ → 用 `ListView.builder`（性能更好）         |
| 页面中嵌套多个滚动区域   | 小心嵌套冲突，使用 `NestedScrollView` 解决   |

🌟 横向滚动：

```dart
SingleChildScrollView(
  scrollDirection: Axis.horizontal,
  child: Row(
    children: [
      Text('1'),
      Text('2'),
      Text('3'),
    ],
  ),
)
```

---

### 📝 Flutter 列表组件

Flutter 提供了多种列表组件，类似于 RN 的 `FlatList`、`SectionList` 等。

#### 1. **`ListView`**

- **用途**：用于渲染一维滚动列表（如聊天记录、文章列表）。
- **特性**：
  - 提供 `ListView.builder` 实现虚拟化渲染，性能优。
  - 支持分页加载。
  - 支持下拉刷新。

```dart
ListView.builder(
  itemCount: data.length,
  itemBuilder: (context, index) {
    return Text(data[index].name);
  },
)
```

#### 2. **`ListView.separated`**

- **用途**：用于渲染带分隔符的列表。
- **特性**：
  - 自动为列表项添加分隔符。

```dart
ListView.separated(
  itemCount: data.length,
  itemBuilder: (context, index) {
    return Text(data[index].name);
  },
  separatorBuilder: (context, index) {
    return Divider();
  },
)
```

#### 3. **`SingleChildScrollView`**

- **用途**：渲染少量静态内容。
- **特性**：
  - 不支持虚拟化，适合少量内容。
  - 支持任意嵌套结构。

```dart
SingleChildScrollView(
  child: Column(
    children: data.map((item) => Text(item.name)).toList(),
  ),
)
```

#### 4. **分组列表（类似 RN 的 `SectionList`）**

Flutter 没有直接的 `SectionList`，但可以通过 `ListView` 自定义实现分组：

```dart
class GroupedList extends StatelessWidget {
  final List<Map<String, dynamic>> sections = [
    {'title': 'Group 1', 'data': ['Item 1', 'Item 2']},
    {'title': 'Group 2', 'data': ['Item 3', 'Item 4']},
  ];

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: sections.length,
      itemBuilder: (context, index) {
        final section = sections[index];
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Padding(
              padding: EdgeInsets.all(8.0),
              child: Text(section['title'], style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
            ),
            ...section['data'].map<Widget>((item) => ListTile(title: Text(item))).toList(),
          ],
        );
      },
    );
  }
}
```

#### 5. **`sliver_list`（高级用法）**

- **用途**：用于复杂滚动效果（如嵌套滚动）。
- **特性**：
  - 配合 `CustomScrollView` 使用，提供更细粒度的控制。

```dart
CustomScrollView(
  slivers: [
    SliverList(
      delegate: SliverChildBuilderDelegate(
        (context, index) => Text(data[index].name),
        childCount: data.length,
      ),
    ),
  ],
)
```

#### 🔍 选择建议

| 类型              | 场景推荐              | 优势                       |
|-------------------|-----------------------|----------------------------|
| `ListView.builder`| 中大型列表（80%场景） | 性能优，虚拟化渲染         |
| `ListView.separated` | 需要分隔符的列表     | 内置分隔符支持             |
| `SingleChildScrollView` | 少量静态内容（<50项） | 简单易用，不适合长列表     |
| `CustomScrollView` | 复杂滚动效果         | 更细粒度控制               |

---

## 2、导航

Flutter 的导航由 `Navigator` 管理，内置支持堆栈导航。Flutter 也有类似 RN `React Navigation` 的第三方库（如 `go_router`），但我们先聚焦官方方式。

---

### 🧱 1. 堆栈导航（Stack Navigator）

Flutter 使用 `Navigator` 实现页面堆栈导航。

✅ 使用方法：

```dart
// main.dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (context) => HomeScreen(),
        '/detail': (context) => DetailScreen(),
      },
    );
  }
}

// home_screen.dart
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pushNamed(context, '/detail', arguments: {'itemId': 42});
          },
          child: Text('Go to Detail'),
        ),
      ),
    );
  }
}

// detail_screen.dart
class DetailScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final args = ModalRoute.of(context)!.settings.arguments as Map;
    return Scaffold(
      appBar: AppBar(title: Text('Detail')),
      body: Center(
        child: Text('Item ID: ${args['itemId']}'),
      ),
    );
  }
}
```

📌 常用 API：

- `Navigator.pushNamed(context, '/route')`：跳转到某页面。
- `Navigator.pop(context)`：返回上一页。
- `ModalRoute.of(context)!.settings.arguments`：获取页面传参。
- `AppBar`：默认提供顶部标题栏，可通过 `Scaffold` 的 `appBar` 设置。

💬 典型场景：
- 登录/注册流程。
- 首页 → 详情页。

---

### 🧭 2. 底部标签导航（Bottom Tabs Navigator）

Flutter 使用 `BottomNavigationBar` 实现底部导航。

✅ 使用方法：

```dart
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  int _currentIndex = 0;

  final List<Widget> _pages = [
    HomeScreen(),
    ProfileScreen(),
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: _pages[_currentIndex],
        bottomNavigationBar: BottomNavigationBar(
          currentIndex: _currentIndex,
          onTap: (index) {
            setState(() {
              _currentIndex = index;
            });
          },
          items: [
            BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
            BottomNavigationBarItem(icon: Icon(Icons.person), label: 'Profile'),
          ],
        ),
      ),
    );
  }
}
```

📌 常用 API：

- `items`：配置底部导航项。
- `currentIndex`：当前选中项。
- `onTap`：切换页面时的回调。

💬 典型场景：
- “首页 / 消息 / 我的” 类结构。

---

### 🧳 3. 抽屉导航（Drawer Navigator）

Flutter 使用 `Drawer` 实现抽屉导航。

✅ 使用方法：

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Dashboard')),
        drawer: Drawer(
          child: ListView(
            children: [
              DrawerHeader(child: Text('Menu')),
              ListTile(
                title: Text('Settings'),
                onTap: () {
                  Navigator.pushNamed(context, '/settings');
                },
              ),
            ],
          ),
        ),
        body: Center(child: Text('Dashboard')),
      ),
    );
  }
}
```

📌 常用 API：

- `child`：抽屉内容。
- `DrawerHeader`：抽屉头部。

💬 典型场景：
- 设置菜单。
- 不常用的页面收纳。

---

### 🧭 4. 顶部标签页（Material Top Tabs）

Flutter 使用 `TabBar` 和 `TabBarView` 实现顶部标签导航。

✅ 使用方法：

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: DefaultTabController(
        length: 3,
        child: Scaffold(
          appBar: AppBar(
            bottom: TabBar(
              tabs: [
                Tab(text: 'All'),
                Tab(text: 'News'),
                Tab(text: 'Tech'),
              ],
            ),
          ),
          body: TabBarView(
            children: [
              Center(child: Text('All')),
              Center(child: Text('News')),
              Center(child: Text('Tech')),
            ],
          ),
        ),
      ),
    );
  }
}
```

📌 常用 API：

- `length`：Tab 数量。
- `tabs`：Tab 标签。
- `children`：Tab 对应的页面。

💬 典型场景：
- 分类内容切换（新闻、图文、评论）。

---

### 🎯 多导航嵌套组合

Flutter 支持嵌套导航，比如底部导航结合堆栈导航：

```dart
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pushNamed(context, '/detail');
          },
          child: Text('Go to Detail'),
        ),
      ),
    );
  }
}
```

---

### 🚨 注意事项

1. 所有导航必须在 `MaterialApp` 或 `CupertinoApp` 中配置。
2. Flutter 的导航不需要额外的手势库支持。
3. 使用 `Navigator 2.0` 或第三方库（如 `go_router`）可以实现更复杂的导航逻辑。

---

## 3、本地存储

Flutter 提供了多种本地存储方式，类似于 RN 的 `AsyncStorage` 和 `Keychain`。

---

### 🔐 1. shared_preferences（类似 RN 的 AsyncStorage）

✅ 是什么？

`shared_preferences` 是一个轻量级键值对存储库，类似于 RN 的 `AsyncStorage`。

🔧 安装：

```bash
flutter pub add shared_preferences
```

📦 常用 API：

📝 保存数据：

```dart
import 'package:shared_preferences/shared_preferences.dart';

Future<void> saveData() async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.setString('userToken', 'abc123');
}
```

📖 读取数据：

```dart
Future<String?> getData() async {
  final prefs = await SharedPreferences.getInstance();
  return prefs.getString('userToken');
}
```

❌ 删除数据：

```dart
Future<void> removeData() async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.remove('userToken');
}
```

🧹 清空数据：

```dart
Future<void> clearData() async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.clear();
}
```

✅ 批量操作：

```dart
Future<void> multiSet() async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.setString('user', 'tom');
  await prefs.setString('age', '23');
}

Future<Map<String, String>> multiGet() async {
  final prefs = await SharedPreferences.getInstance();
  final user = prefs.getString('user') ?? '';
  final age = prefs.getString('age') ?? '';
  return {'user': user, 'age': age};
}
```

📌 注意事项：
- 异步操作，使用 `await`。
- 支持存储基本类型（`String`, `int`, `double`, `bool`），对象需序列化为 `String`。

💬 使用场景：
- 登录 token 缓存。
- 引导页是否已读。
- 用户偏好设置。

---

### 🔒 2. flutter_secure_storage（类似 RN 的 Keychain）

✅ 是什么？

`flutter_secure_storage` 提供安全的存储方式，基于 iOS Keychain 和 Android EncryptedSharedPreferences。

🔧 安装：

```bash
flutter pub add flutter_secure_storage
```

📦 常用 API：

📝 保存数据：

```dart
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

final storage = FlutterSecureStorage();

Future<void> saveCredentials() async {
  await storage.write(key: 'userToken', value: 'abc123');
}
```

📖 读取数据：

```dart
Future<String?> getCredentials() async {
  return await storage.read(key: 'userToken');
}
```

❌ 删除数据：

```dart
Future<void> deleteCredentials() async {
  await storage.delete(key: 'userToken');
}
```

🛡️ 高级选项（加密存储）：

```dart
await storage.write(
  key: 'userToken',
  value: 'abc123',
  aOptions: AndroidOptions(encryptedSharedPreferences: true),
);
```

💬 使用场景：
- 存储敏感数据（如 token、密码）。
- 开启生物识别登录（需要额外插件支持，如 `local_auth`）。

#### 🔍 shared_preferences vs flutter_secure_storage 对比

| 特性         | shared_preferences     | flutter_secure_storage                       |
|--------------|------------------------|----------------------------------------------|
| 数据类型     | 基本类型（需序列化对象） | 字符串                                      |
| 是否加密     | ❌ 否                   | ✅ 是（系统级加密）                          |
| 存储位置     | 应用内部存储（非加密） | 系统级安全存储                              |
| 常用场景     | 缓存、偏好设置         | 登录凭证、token、安全信息                   |

#### 📦 推荐用法组合

- 登录场景中：
  - token 用 `flutter_secure_storage` 存储。
  - 是否已登录、用户设置用 `shared_preferences` 存储。

---

### 🧠 Hive（类似 RN 的 MMKV）

✅ 是什么？

`Hive` 是 Flutter 中一个高性能的键值存储库，类似于 RN 的 `MMKV`，支持快速读写。

🔧 安装：

```bash
flutter pub add hive hive_flutter
```

📦 使用方法：

```dart
import 'package:hive/hive.dart';
import 'package:hive_flutter/hive_flutter.dart';

void main() async {
  await Hive.initFlutter();
  var box = await Hive.openBox('myBox');
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: ElevatedButton(
            onPressed: () async {
              var box = Hive.box('myBox');
              await box.put('token', 'abc123');
              print(box.get('token')); // abc123
            },
            child: Text('Save Token'),
          ),
        ),
      ),
    );
  }
}
```

📌 常用 API：

- `put(key, value)`：存储数据。
- `get(key)`：读取数据。
- `delete(key)`：删除数据。
- `clear()`：清空所有数据。

⚡ 性能对比（vs shared_preferences）：

| 操作         | shared_preferences | Hive                    |
|--------------|--------------------|-------------------------|
| 写入一个键值 | 慢（异步）         | 快（同步）              |
| 读取键值     | 慢                 | 极快                    |
| 支持数据类型 | 基本类型           | 任意类型（需注册适配器） |
| 加密支持     | ❌                 | ✅（需配置）             |

💬 使用场景：
- 高频读取（如 token、用户ID）。
- 小体积本地缓存。

---

## 4、其他组件

### 🧩 4.1 QR 码

Flutter 使用 `qr_flutter` 生成二维码。

🔧 安装：

```bash
flutter pub add qr_flutter
```

✅ 基本用法：

```dart
import 'package:qr_flutter/qr_flutter.dart';

QrImageView(
  data: 'https://example.com',
  version: QrVersions.auto,
  size: 200.0,
)
```

📌 常用属性：

| 属性            | 说明                       |
|-----------------|----------------------------|
| `data`          | 二维码内容                 |
| `size`          | 尺寸                       |
| `foregroundColor` | 前景色                   |
| `backgroundColor` | 背景色                   |
| `errorCorrectionLevel` | 容错级别（低到高） |

🖼 支持嵌入 logo：

```dart
QrImageView(
  data: 'https://example.com',
  size: 200,
  embeddedImage: AssetImage('assets/logo.png'),
  embeddedImageStyle: QrEmbeddedImageStyle(size: Size(30, 30)),
)
```

---

### ⚙️ 4.2 Modal

Flutter 使用 `showDialog` 或 `Overlay` 实现模态框。

✅ Loading 示例：

```dart
Future<void> getUserInfo(BuildContext context) async {
  // 显示 Loading
  showDialog(
    context: context,
    barrierDismissible: false,
    builder: (context) => Center(
      child: Column(
        mainAxisSize: MainAxisSize.min,
        children: [
          CircularProgressIndicator(color: Color(0xFFD31145)),
          SizedBox(height: 10),
          Text('加载中...', style: TextStyle(color: Colors.white)),
        ],
      ),
    ),
    barrierColor: Colors.black54, // 半透明遮罩
  );

  try {
    await Future.delayed(Duration(seconds: 2)); // 模拟请求
  } finally {
    Navigator.pop(context); // 关闭 Loading
  }
}
```

---

### 🔔 4.3 下拉刷新

Flutter 使用 `RefreshIndicator` 实现下拉刷新。

✅ 基本用法：

```dart
RefreshIndicator(
  onRefresh: () async {
    await Future.delayed(Duration(seconds: 2));
  },
  color: Color(0xFFD31145),
  child: ListView(
    physics: AlwaysScrollableScrollPhysics(),
    children: [
      Text('可下拉刷新'),
    ],
  ),
)
```

📌 其他可选参数：

| 参数         | 说明                             |
|--------------|----------------------------------|
| `onRefresh`  | 下拉时触发的函数（必填）         |
| `color`      | 加载动画颜色                     |
| `backgroundColor` | 背景色                   |

---

### 📷 4.5 调用摄像头

Flutter 使用 `camera` 插件调用摄像头。

🔧 安装：

```bash
flutter pub add camera
```

✅ 示例（简单拍照）：

```dart
import 'package:camera/camera.dart';

class CameraScreen extends StatefulWidget {
  @override
  _CameraScreenState createState() => _CameraScreenState();
}

class _CameraScreenState extends State<CameraScreen> {
  CameraController? _controller;

  @override
  void initState() {
    super.initState();
    _initializeCamera();
  }

  Future<void> _initializeCamera() async {
    final cameras = await availableCameras();
    _controller = CameraController(cameras[0], ResolutionPreset.medium);
    await _controller!.initialize();
    setState(() {});
  }

  @override
  Widget build(BuildContext context) {
    if (_controller == null || !_controller!.value.isInitialized) {
      return Center(child: CircularProgressIndicator());
    }
    return CameraPreview(_controller!);
  }
}
```

✅ 高级用法（推荐 `image_picker` 插件）：

🔧 安装：

```bash
flutter pub add image_picker
```

```dart
import 'package:image_picker/image_picker.dart';

Future<void> openCamera() async {
  final picker = ImagePicker();
  final image = await picker.pickImage(source: ImageSource.camera);
  if (image != null) {
    print('照片路径: ${image.path}');
  }
}
```

🔚 总结建议：

| 场景                         | 推荐方式                       |
|------------------------------|--------------------------------|
| 拍照、录像（简单用途）       | ✅ `image_picker`              |
| 扫码、AR、人脸识别等高级功能 | ✅ `camera`                    |

---

### 📜 4.6 常用权限总结（Flutter）

Flutter 的权限管理通常通过 `permission_handler` 插件实现。

🔧 安装：

```bash
flutter pub add permission_handler
```

✅ 示例（请求摄像头权限）：

```dart
import 'package:permission_handler/permission_handler.dart';

Future<void> requestCameraPermission() async {
  var status = await Permission.camera.request();
  if (status.isGranted) {
    print('摄像头权限已授予');
  } else {
    print('摄像头权限被拒绝');
  }
}
```

📋 权限配置：

1. **摄像头权限**

- **Android**：

```xml
<uses-permission android:name="android.permission.CAMERA" />
```

- **iOS**：

```xml
<key>NSCameraUsageDescription</key>
<string>我们需要使用摄像头进行拍照</string>
```

2. **存储权限**

- **Android**：

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

- **iOS**：无需额外配置。

3. **位置权限**

- **Android**：

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

- **iOS**：

```xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>我们需要使用位置来获取你的地理信息</string>
```

4. **麦克风权限**

- **Android**：

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

- **iOS**：

```xml
<key>NSMicrophoneUsageDescription</key>
<string>我们需要使用麦克风来录制音频</string>
```

5. **相册/文件读取权限**

- **Android**：

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

- **iOS**：

```xml
<key>NSPhotoLibraryUsageDescription</key>
<string>我们需要访问相册来选择图片或视频</string>
```

6. **通知权限**

- **Android**：无需额外配置。
- **iOS**：

```xml
<key>UIBackgroundModes</key>
<array>
  <string>fetch</string>
  <string>remote-notification</string>
</array>
```

7. **蓝牙权限**

- **Android**：

```xml
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

- **iOS**：

```xml
<key>NSBluetoothPeripheralUsageDescription</key>
<string>我们需要使用蓝牙进行设备配对</string>
```

🔚 总结：
- Flutter 的权限需要在 `AndroidManifest.xml` 和 `Info.plist` 中配置。
- 使用 `permission_handler` 动态请求权限。

---

## 总结

Flutter 和 RN 在跨平台开发上有许多相似之处，但 Flutter 使用 Dart 和 Widget 体系，导航和存储方式更内置。通过上述笔记，你可以快速从 RN 迁移到 Flutter 开发。如果需要更详细的某个部分（例如导航封装、状态管理等），可以告诉我，我会进一步帮你设计！