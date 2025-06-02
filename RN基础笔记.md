# RN快速上手

## **React Native 是什么？**

React Native 是基于 React 的框架，用于构建原生移动应用（iOS 和 Android）。它允许开发者使用 JavaScript 和 React 的语法来编写代码，但最终生成原生 UI 组件，而不是 WebView 中的 HTML/CSS。React Native 的特点包括：

- **跨平台**：一套代码运行在 iOS 和 Android 上。
- **原生性能**：直接使用原生组件（如 <View>、<Text>），性能接近原生应用。
- **热重载**：代码修改后立即看到效果，提升开发效率。

在你的代码中，ThemedView 是一个 React Native 组件，使用了 <View>（React Native 的核心组件，类似 HTML 的 <div>）。

------

**Expo 是什么？**

Expo 是一个基于 React Native 的开发工具和框架，旨在简化 React Native 应用的开发、构建和部署。它提供了一套工具和服务，包括：

- **Expo CLI**：用于创建、运行和调试项目的命令行工具。

- **Expo SDK**：一组预构建的库（如相机、地图、推送通知等），无需编写原生代码即可使用设备功能。

- **Expo Go**：一个移动应用，允许在开发时通过扫描二维码快速预览应用。

- **托管服务**：简化应用的构建和发布流程。

  ------

  

***创建*RN:**

用React-Native-Community脚手架创建

```bash
npm install -g @react-native-community/cli
npx @react-native-community/cli init MYAPP
```

用Expo创建（***目录路由***）

```bash
npm install -g expo-cli
npx create-expo-app my-app
```

**Expo vs. 纯 React Native**

如果你在考虑是使用 Expo 还是纯 React Native 来开发，这里是一些对比：

| 特性               | Expo                               | 纯 React Native                     |
| ------------------ | ---------------------------------- | ----------------------------------- |
| **入门难度**       | 简单，无需配置原生环境             | 复杂，需要配置 Xcode/Android Studio |
| **开发速度**       | 快速（热重载、Expo Go 预览）       | 较慢（需要编译原生代码）            |
| **功能支持**       | 提供大量预构建 API（如相机、地图） | 需手动集成原生模块                  |
| **自定义原生代码** | 有限（需“弹出”到 bare workflow）   | 完全支持                            |
| **构建和发布**     | 托管服务简化流程                   | 需手动配置构建流程                  |





## 1、常用核心组件



### 📝 `Text` 组件

`Text` 用于**显示一段文本内容**。（***RN中所有的文本内容必须要用TEXT组件包裹***）

✅ 基本用法：

```jsx
import { Text } from 'react-native';

<Text>Hello, React Native!</Text>
```

✨ 常见属性：

| 属性            | 作用                                         |
| --------------- | -------------------------------------------- |
| `style`         | 自定义文字样式（颜色、字体大小、行距等）     |
| `numberOfLines` | 限制显示行数，超出部分会省略号               |
| `ellipsizeMode` | 当超出时如何显示（tail, head, middle, clip） |
| `selectable`    | 是否可选择文字（默认 false）                 |
| `onPress`       | 点击文字事件处理                             |

🌟 示例（限制一行显示）：

```jsx
<Text numberOfLines={1} ellipsizeMode="tail" style={{ fontSize: 16 }}>
  这是一段很长很长的文字，会被省略……
</Text>
```

------

### ⌨️ `TextInput` 组件

`TextInput` 用于**接收用户输入**，类似于 HTML 的 `<input />`。

✅ 基本用法：

```jsx
import { TextInput } from 'react-native';
import { useState } from 'react';

const MyComponent = () => {
  const [text, setText] = useState('');

  return (
    <TextInput
      value={text}
      onChangeText={setText}
      placeholder="请输入内容"
      style={{ borderWidth: 1, padding: 8 }}
    />
  );
};
```

✨ 常见属性：

| 属性              | 作用                                               |
| ----------------- | -------------------------------------------------- |
| `value`           | 输入框当前值（受控组件）                           |
| `onChangeText`    | 输入文本变化时的回调                               |
| `placeholder`     | 占位符                                             |
| `secureTextEntry` | 密码模式（隐藏输入）                               |
| `keyboardType`    | 设置键盘类型（default, numeric, email-address 等） |
| `multiline`       | 是否多行输入                                       |
| `maxLength`       | 最大输入长度                                       |
| `editable`        | 是否可编辑                                         |
| `autoFocus`       | 是否自动聚焦                                       |

🌟 示例（密码输入框）：

```jsx
<TextInput
  secureTextEntry
  placeholder="请输入密码"
  style={{ borderWidth: 1, padding: 8 }}
/>
```

------

🆚 对比总结：

| 功能     | `Text`          | `TextInput`            |
| -------- | --------------- | ---------------------- |
| 显示文本 | ✅               | ❌                      |
| 输入文本 | ❌               | ✅                      |
| 支持样式 | ✅               | ✅                      |
| 可点击   | ✅（加 onPress） | ✅                      |
| 状态管理 | ❌               | ✅（需结合 `useState`） |

------

当然可以！React Native（RN）的 `Image` 组件是用来**展示图片**的，非常核心和常用，类似于网页里的 `<img>` 标签。

------

### 🖼️ Image基本用法：

```jsx
import { Image } from 'react-native';

<Image
  source={{ uri: 'https://example.com/my-image.jpg' }}
  style={{ width: 100, height: 100 }}
/>
```

RN 中的 `Image` 需要配合 `style` 设置尺寸，否则**图片不会显示**！

------

🗂️ `source` 属性

- 加载**网络图片**：

```jsx
source={{ uri: 'https://example.com/image.jpg' }}
```

- 加载**本地图片**（项目文件中的图片）：

```jsx
source={require('./assets/logo.png')}
```

注意：`require` 只能用于本地静态资源，不能动态拼路径。

------

🎯 常见属性一览：

| 属性            | 类型     | 说明                           |
| --------------- | -------- | ------------------------------ |
| `source`        | object   | 图片来源（`uri` 或 `require`） |
| `style`         | object   | 图片样式（必须设置宽高）       |
| `resizeMode`    | string   | 图片拉伸方式，详见下方         |
| `onLoad`        | function | 图片加载成功时调用             |
| `onError`       | function | 图片加载失败时调用             |
| `defaultSource` | require  | 图片加载前的占位图（仅限 iOS） |
| `blurRadius`    | number   | 图片模糊程度                   |

------

🎨 `resizeMode` 拉伸方式：

用于控制图片如何适配容器：

| 模式      | 效果                               |
| --------- | ---------------------------------- |
| `cover`   | 保持比例填满，超出部分裁剪（默认） |
| `contain` | 保持比例缩放完整显示               |
| `stretch` | 拉伸填满，不保持比例               |
| `center`  | 原图大小居中显示                   |
| `repeat`  | 重复平铺（iOS 支持好）             |

**示例**：

```jsx
<Image
  source={{ uri: 'https://example.com/image.jpg' }}
  style={{ width: 200, height: 200 }}
  resizeMode="contain"
/>
```

------

🔄 网络图失败占位图逻辑（推荐做法）：

```jsx
const [error, setError] = useState(false);

<Image
  source={
    error
      ? require('./assets/placeholder.png')
      : { uri: 'https://example.com/image.jpg' }
  }
  style={{ width: 100, height: 100 }}
  onError={() => setError(true)}
/>
```

------

🌟 常见场景

1. 显示头像、背景图、banner 图
2. 与 `FlatList` 或 `ScrollView` 组合显示图片列表
3. 加上点击事件用作按钮背景：

```jsx
<TouchableOpacity onPress={...}>
  <Image source={...} style={...} />
</TouchableOpacity>
```



### 🖼️ `ImageBackground` 是什么？

它是一个可以**作为容器使用的图片组件**，你可以在它里面嵌套文字、按钮、图标等内容。

> 就像 HTML 里的：
>
> ```jsx
> <div style="background-image: url(...)"> ...内容... </div>
> ```

------

✅ 基本用法：

```jsx
import { ImageBackground, Text } from 'react-native';

<ImageBackground
  source={{ uri: 'https://example.com/bg.jpg' }}
  style={{ width: '100%', height: 200, justifyContent: 'center', alignItems: 'center' }}
>
  <Text style={{ color: 'white', fontSize: 20 }}>我是背景图上的文字</Text>
</ImageBackground>
```

------

✨ 常用属性：

| 属性         | 说明                              |
| ------------ | --------------------------------- |
| `source`     | 图片地址（支持 uri 或 require）   |
| `style`      | 外层容器样式（必须设宽高）        |
| `imageStyle` | 设置图片本身的样式（比如圆角）    |
| `resizeMode` | 图片缩放模式（cover、contain 等） |
| `children`   | 你要显示在图片上的内容            |

------

🎯 示例：卡片带背景图 + 圆角

```jsx
<ImageBackground
  source={require('./assets/card-bg.jpg')}
  style={{
    width: 300,
    height: 150,
    justifyContent: 'flex-end',
    padding: 16,
  }}
  imageStyle={{ borderRadius: 12 }}
>
  <Text style={{ color: 'white', fontWeight: 'bold' }}>卡片标题</Text>
</ImageBackground>
```

------

⚠️ 注意点：

- `ImageBackground` 的 `style` 是**容器的样式**，包括宽高、内边距等；
- `imageStyle` 是**图片本身的样式**，比如想加圆角或模糊，就加在这；
- 里面可以嵌套多个组件，比如按钮、图标、布局组件等，完全当容器用。

------

🧠 使用场景：

- 登录页/欢迎页的背景图
- Banner 卡片、活动广告位
- 视频封面图 + 播放按钮
- 用户信息卡 + 背景

------



### 🔘 TouchableOpacity 

📌 简介

`TouchableOpacity` 是 React Native 中用于处理点击事件的组件之一。它会在用户点击时调整子元素的不透明度，提供一个视觉反馈效果。

------

🧱 基本用法

```tsx
import React from 'react';
import { TouchableOpacity, Text, StyleSheet } from 'react-native';

const MyButton = () => {
  return (
    <TouchableOpacity style={styles.button} onPress={() => alert('点击了！')}>
      <Text style={styles.text}>点击我</Text>
    </TouchableOpacity>
  );
};

const styles = StyleSheet.create({
  button: {
    backgroundColor: '#1976D2',
    padding: 10,
    borderRadius: 8,
  },
  text: {
    color: '#fff',
    textAlign: 'center',
  },
});
```

------

⚙️ 常用属性

| 属性名          | 说明                                         | 类型         |
| --------------- | -------------------------------------------- | ------------ |
| `onPress`       | 点击时触发的函数                             | `() => void` |
| `activeOpacity` | 被按下时的不透明度，范围为 0~1（默认是 0.2） | `number`     |
| `disabled`      | 是否禁用点击响应                             | `boolean`    |
| `style`         | 组件样式                                     | `object`     |

------

🎨 示例：设置透明度

```tsx
<TouchableOpacity onPress={handleClick} activeOpacity={0.6}>
  <Text>轻触我</Text>
</TouchableOpacity>
```

------

⚠️ 注意事项

- `TouchableOpacity` 适用于简单的按钮或列表项点击。
- 如果需要更复杂的手势反馈（比如缩放、滑动），可考虑使用 `Pressable` 或 `TouchableHighlight`。
- 多层嵌套 `TouchableOpacity` 时，注意点击区域的穿透与事件冒泡问题。

------

需要我再帮你讲解 `Pressable` 或整理成 PDF 吗？







### 🧭 ScrollView 组件

```jsx
import { ScrollView, Text, View } from 'react-native';

<ScrollView style={{ flex: 1 }}>
  <Text>我是可以滚动的内容</Text>
  {/* 你可以放很多很多内容 */}
</ScrollView>
```

ScrollView 的内容超出屏幕时会自动滚动，适合内容**不多时**使用。

------

🧱 常见属性

| 属性                             | 说明                                   |
| -------------------------------- | -------------------------------------- |
| `horizontal`                     | 是否横向滚动（默认是竖直方向）         |
| `showsVerticalScrollIndicator`   | 是否显示纵向滚动条                     |
| `showsHorizontalScrollIndicator` | 是否显示横向滚动条                     |
| `contentContainerStyle`          | 内容容器的样式（不是 ScrollView 本身） |
| `refreshControl`                 | 配置下拉刷新组件                       |
| `onScroll`                       | 监听滚动事件（可用于加载更多）         |
| `scrollEnabled`                  | 控制是否允许滚动                       |
| `keyboardShouldPersistTaps`      | 配合 TextInput，点击空白是否隐藏键盘   |

------

📦 内容撑满的写法（常配合 `contentContainerStyle`）

```jsx
<ScrollView
  contentContainerStyle={{ padding: 20 }}
>
  <Text>内容...</Text>
</ScrollView>
```

------

🔄 下拉刷新示例（结合 `RefreshControl`）

```jsx
import { ScrollView, RefreshControl } from 'react-native';
import { useState } from 'react';

const MyScroll = () => {
  const [refreshing, setRefreshing] = useState(false);

  const onRefresh = () => {
    setRefreshing(true);
    setTimeout(() => setRefreshing(false), 2000); // 模拟刷新
  };

  return (
    <ScrollView
      refreshControl={
        <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
      }
    >
      <Text>可下拉刷新</Text>
    </ScrollView>
  );
};
```

------

⚠️ 使用注意

| 场景                     | 推荐组件                                     |
| ------------------------ | -------------------------------------------- |
| 内容较少，可以一次性渲染 | ✅ `ScrollView`                               |
| 内容很多（如长列表）     | ❌ → **用 `FlatList`** 性能更好（虚拟化渲染） |
| 页面中嵌套多个滚动区域   | 注意不要嵌套多个 ScrollView，会产生冲突      |

------

🌟 横向滚动

```jsx
<ScrollView horizontal>
  <Text>1</Text>
  <Text>2</Text>
  <Text>3</Text>
</ScrollView>
```

常用于轮播图、标签栏等。

------



### 📝 React Native 列表组件

------

1. **FlatList**

- **用途**：用于渲染较长的一维滚动列表（如聊天记录、文章列表）。
- **特性**：
  - 高性能虚拟渲染
  - 支持分页加载（`onEndReached`）
  - 支持下拉刷新（`onRefresh`）
  - 支持自定义 `ItemSeparatorComponent`、`ListHeaderComponent` 等

```tsx
<FlatList
  data={data}
  renderItem={({ item }) => <Text>{item.name}</Text>}
  keyExtractor={(item) => item.id.toString()}
  onEndReached={loadMore}
  refreshing={isRefreshing}
  onRefresh={refreshData}
/>
```

------

2. **SectionList**

- #### **用途**：用于渲染带分组的列表，例如按日期或类别分组的数据。
- **特性**：
  - 每组有一个 `section` header
  - 支持所有 `FlatList` 的功能

```tsx
<SectionList
  sections={sectionsData}
  keyExtractor={(item, index) => item + index}
  renderItem={({ item }) => <Text>{item}</Text>}
  renderSectionHeader={({ section }) => <Text>{section.title}</Text>}
/>
```

------

3. **ScrollView**

- **用途**：渲染较少的子元素（内容量不大），用于静态或嵌套列表。
- **特性**：
  - 不支持虚拟化，性能不如 FlatList
  - 可以容纳任意嵌套结构
  - 支持横向滚动、分页等特性

```tsx
<ScrollView>
  {data.map(item => (
    <Text key={item.id}>{item.name}</Text>
  ))}
</ScrollView>
```

------

4. **VirtualizedList**

- ### **用途**：底层组件，FlatList 和 SectionList 都是基于它构建的。
- **特性**：
  - 适合有特殊数据结构需求的开发者使用
  - 提供更灵活的虚拟渲染控制

```tsx
<VirtualizedList
  data={data}
  initialNumToRender={10}
  renderItem={({ item }) => <Text>{item.name}</Text>}
  keyExtractor={item => item.id}
/>
```

------

5. **FlashList**（推荐第三方库）

- **库**：[Shopify/FlashList](https://github.com/Shopify/flash-list)
- **用途**：高性能替代 FlatList，适合超长列表或性能要求高的场景。
- **优势**：
  - 比 FlatList 更快
  - 减少白屏和卡顿现象
  - 内置预估高度等优化策略

```tsx
import { FlashList } from "@shopify/flash-list";

<FlashList
  data={data}
  renderItem={({ item }) => <Text>{item.name}</Text>}
  estimatedItemSize={50}
/>
```

------

🔍 选择建议



| 类型              | 场景推荐              | 优势                       |
| ----------------- | --------------------- | -------------------------- |
| `FlatList`        | 中大型列表（80%场景） | 性能优、API丰富            |
| `SectionList`     | 分组数据展示          | 自带分组header支持         |
| `ScrollView`      | 少量静态内容（<50项） | 简单易用，不推荐用于长列表 |
| `VirtualizedList` | 高级定制              | 更细粒度控制               |
| `FlashList`       | 超长列表/性能要求高   | Shopify出品，性能极佳      |

------



好的，明白了，你想要的是：

👉 **React Native 原生自带的 Toast（提示消息）怎么用？**

------

### 🍞 原生 Toast 总结

在 React Native 里，有个**官方自带**的模块叫：

```tsx
import { ToastAndroid } from 'react-native';
```

它是**Android专用**的！

iOS 是没有官方 Toast 的，需要自己封装（后面我也告诉你怎么处理）。

------

🛠️ 在 Android 上使用 `ToastAndroid`

最简单用法：

```tsx
import { ToastAndroid } from 'react-native';

// 显示一个短时间的Toast
ToastAndroid.show('这是提示内容', ToastAndroid.SHORT);
```

参数解释

- 第一个参数：提示的文本
- 第二个参数：
  - `ToastAndroid.SHORT` （短时间）
  - `ToastAndroid.LONG` （长时间）

------

让 Toast 出现在不同位置（底部、中间、顶部）

可以使用 `ToastAndroid.showWithGravity`：

```tsx
ToastAndroid.showWithGravity(
  '我是居中的提示～',
  ToastAndroid.SHORT,
  ToastAndroid.CENTER
);
```

**位置选项：**

- `ToastAndroid.TOP`
- `ToastAndroid.CENTER`
- `ToastAndroid.BOTTOM`

------

进一步自定义位置（绝对偏移）

使用 `showWithGravityAndOffset`：

```tsx
ToastAndroid.showWithGravityAndOffset(
  '我是自定义偏移的Toast～',
  ToastAndroid.LONG,
  ToastAndroid.BOTTOM,
  0, // X轴偏移量
  100 // Y轴偏移量（比如往上浮动一点）
);
```

------

❗ 注意

- `ToastAndroid` **只能在 Android 设备上生效**。
- iOS 系统里官方没有 Toast，需要自己引第三方库（比如 [`react-native-toast-message`](https://github.com/calintamas/react-native-toast-message)）。

如果你直接在 iOS 上调用 `ToastAndroid`，会报错！

------

🍎 iOS 怎么办？

如果要兼容 **Android + iOS**，通常做法是：

- 写一个封装 `showToast()` 方法
- Android 用 `ToastAndroid`
- iOS 用 Alert、SnackBar、或者装个跨端 Toast 库，比如：

推荐的库：

- [`react-native-toast-message`](https://github.com/calintamas/react-native-toast-message) （很流行，支持多种样式）
- [`react-native-simple-toast`](https://github.com/vonovak/react-native-simple-toast) （简单版）

------

📢 小结公式

| 平台    | 用法                 |
| ------- | -------------------- |
| Android | `ToastAndroid` ✅     |
| iOS     | 需要额外封装或引库 ❗ |

------

要不要我给你写一个**自动判断平台的小 Toast 封装函数**？
 比如 `showToast('xxx')`，自动 Android 原生 + iOS 弹窗？要的话告诉我，我可以顺便帮你做超漂亮的封装！🚀
 要不要？🌟



### 🌙 StatusBar

在 React Native 中，你可以通过内置的 `StatusBar` 组件来自定义状态栏的样式、背景色和内容颜色（如文字和图标的颜色）。以下是常见的用法示例和说明：

------

✅ 基本用法

```tsx
import React from 'react';
import { StatusBar, View } from 'react-native';

export default function App() {
  return (
    <View style={{ flex: 1 }}>
      <StatusBar
        backgroundColor="#1976D2" // Android 状态栏背景色
        barStyle="light-content"  // 状态栏内容颜色 (light-content / dark-content)
        translucent={false}       // 是否透明
      />
      {/* 其他内容 */}
    </View>
  );
}
```

------

📱 参数说明

| 属性              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| `barStyle`        | 控制状态栏文本/图标颜色（`light-content` 或 `dark-content`） |
| `backgroundColor` | 设置背景颜色（仅 Android 有效）                              |
| `translucent`     | 是否透明背景（仅 Android）                                   |
| `hidden`          | 是否隐藏状态栏（iOS + Android）                              |
| `animated`        | 状态变化是否有动画过渡效果                                   |

------

🌙 根据主题动态设置

你可以结合 `useColorScheme()` 或你自定义的主题系统动态设置状态栏样式：

```tsx
import { StatusBar, useColorScheme } from 'react-native';

const isDark = useColorScheme() === 'dark';

<StatusBar
  barStyle={isDark ? 'light-content' : 'dark-content'}
  backgroundColor={isDark ? '#121212' : '#FAFAFA'}
/>
```

------

⚠️ iOS 注意事项

- iOS 无法通过 `backgroundColor` 修改状态栏背景色，只能通过改变容器背景来“模拟”状态栏颜色。
- `StatusBar` 默认在 `SafeAreaView` 内部才能避免遮挡。

------



## 2、导航

React Native（RN）中的导航一般通过第三方库来实现，最主流的就是：

🌟 `React Navigation` —— React Native 官方推荐导航库

网址：https://reactnavigation.org

这是目前最常用、最强大、社区最活跃的导航库。

------

📦 安装（基础栈导航）

```bash
npm install @react-navigation/native
```

再安装依赖项：

```bash
npx expo install react-native-screens react-native-safe-area-context react-native-gesture-handler react-native-reanimated react-native-vector-icons
```

对于 bare React Native 项目，还需要安装 `react-native-screens` 和 `react-native-safe-area-context`：

```bash
npm install react-native-screens react-native-safe-area-context
```

然后安装你要用的导航器，比如：

📌 Stack Navigator（堆栈导航，最常用）

```bash
npm install @react-navigation/native-stack
```

------

📚 常见导航类型

| 类型             | 作用                               |
| ---------------- | ---------------------------------- |
| Stack Navigator  | 页面堆栈结构（常见于登录、详情页） |
| Bottom Tabs      | 底部导航栏（如微信、微博）         |
| Drawer Navigator | 抽屉导航（从侧边滑出菜单）         |
| Top Tabs         | 顶部 Tab 栏（常见于头条、知乎）    |

### 🧱 1. Stack Navigator（堆栈导航）

✅ 概念详解

Stack（栈）导航器使用栈数据结构：后进先出（LIFO）。每次跳转一个页面，相当于“压入栈”；按返回键或者调用 `goBack()`，就“弹出栈顶页面”。

就像浏览器的返回按钮一样，非常适合页面间前进/后退的交互流程。

------

🔧 安装依赖

```bash
npm install @react-navigation/native-stack
```

------

📄 使用方法

```tsx
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

import HomeScreen from './screens/Home';
import DetailScreen from './screens/Detail';

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Detail" component={DetailScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

------

📌 常用 API

- `navigation.navigate('Page')`：跳转到某页面(navigation.navigate('Details', { itemId: 42 });)
- `navigation.goBack()`：返回上一页
- `route.params`：获取页面传参
- `headerShown: false`：隐藏顶部标题栏

------

💬 典型场景

- 登录/注册流程
- 首页 → 详情页
- 设置页跳转子项设置

------

### 🧭 2. Bottom Tabs Navigator（底部标签导航）

✅ 概念详解

Bottom Tab 是移动 App 最常见的导航方式之一，在屏幕底部放置几个主导航项（类似微信：消息 / 通讯录 / 我）。

------

🔧 安装依赖

```bash
npm install @react-navigation/bottom-tabs react-native-vector-icons
```

------

📄 使用方法

```tsx
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

const Tab = createBottomTabNavigator();

function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator screenOptions={{ headerShown: false }}>
        <Tab.Screen name="Home" component={HomeScreen} />
        <Tab.Screen name="Profile" component={ProfileScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

------

📌 常用 API

- `tabBarIcon`：自定义 tab 图标（需搭配 `react-native-vector-icons`）
- `tabBarOptions`：配置 tab 样式，如颜色、高度等
- `tabBarBadge`：展示角标（如未读数量）

```tsx
<Tab.Screen
  name="Home"
  component={HomeScreen}
  options={{
    tabBarIcon: ({ color, size }) => (
      <Ionicons name="home-outline" size={size} color={color} />
    ),
    tabBarBadge: 3,
  }}
/>
```

------

💬 典型场景

- 微信、微博类主界面
- “首页 / 消息 / 我的” 类结构

------

### 🧳 3. Drawer Navigator（抽屉导航）

✅ 概念详解

Drawer 就是“抽屉式侧边栏”，通常从左边滑出一个菜单，展示多个功能页面入口。

------

🔧 安装依赖

```bash
npm install @react-navigation/drawer
```

------

📄 使用方法

```tsx
import { createDrawerNavigator } from '@react-navigation/drawer';

const Drawer = createDrawerNavigator();

function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator>
        <Drawer.Screen name="Dashboard" component={DashboardScreen} />
        <Drawer.Screen name="Settings" component={SettingsScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

------

📌 常用 API

- `drawerContent`：自定义抽屉内容（头像、退出按钮等）
- `drawerType`：设置抽屉样式（front/back/slide/permanent）
- `drawerPosition`：左侧或右侧抽屉

```tsx
<Drawer.Navigator
  drawerContent={(props) => <CustomDrawerContent {...props} />}
  drawerPosition="left"
/>
```

------

💬 典型场景

- 设置菜单
- 邮箱导航（如 Gmail 左侧抽屉）
- 不常用的页面收纳起来

------

### 🧭 4. Material Top Tabs（顶部标签页）

✅ 概念详解

Material Design 风格的顶部标签导航，支持左右滑动切换，适合用于分类浏览页面，比如头条、知乎的新闻流。

------

🔧 安装依赖

```bash
npm install @react-navigation/material-top-tabs react-native-tab-view
```

------

📄 使用方法

```tsx
import { createMaterialTopTabNavigator } from '@react-navigation/material-top-tabs';

const TopTab = createMaterialTopTabNavigator();

function App() {
  return (
    <NavigationContainer>
      <TopTab.Navigator>
        <TopTab.Screen name="All" component={AllScreen} />
        <TopTab.Screen name="News" component={NewsScreen} />
        <TopTab.Screen name="Tech" component={TechScreen} />
      </TopTab.Navigator>
    </NavigationContainer>
  );
}
```

------

📌 常用 API

- `tabBarOptions`：控制标签样式
- `swipeEnabled: false`：禁止左右滑动切换
- `lazy: true`：懒加载每个 tab 页

------

💬 典型场景

- 分类内容切换（新闻、图文、评论）
- 商品页面多个 tab（商品、评价、详情）

------

🎯 多导航嵌套组合示例

最常见结构是：

```tex
Bottom Tabs
 ├── Stack: Home
 ├── Stack: Profile
 └── Drawer: Settings
```

你可以将 `BottomTabs` 作为主导航，每个 Tab 内嵌一个 Stack 或 Drawer，形成强大的导航组合。

------

🚨 注意事项

1. 所有导航必须包裹在 `<NavigationContainer>` 中。

2. Android 上别忘了启用手势库：

   ```tsx
   import 'react-native-gesture-handler';
   ```

3. 使用 `react-native-screens` 可提升性能。

4. 若导航无效，多半是组件未被正确注册到对应 Navigator 中。



### 🔁5、跳转

------

🔁 **1. `navigate(name, params?)`**

跳转到某个页面（可以是 tab、stack 中的任何页面）：

```js
navigation.navigate('Home', { userId: 123 });
```

------

⬅️ **2. `goBack()`**

返回上一个页面：

```js
navigation.goBack();
```

------

🧭 **3. `push(name, params?)`**

像 `navigate` 一样跳转，但会**压入栈**，即使目标页已经存在，也会重新创建：

```js
navigation.push('Details', { id: 5 });
```

------

❌ **4. `pop(count?)`**

从栈中弹出页面（默认是弹出一个）：

```js
navigation.pop();      // 返回上一级
navigation.pop(2);     // 连续返回两级
```

------

🧹 **5. `popToTop()`**

返回栈顶页面：

```js
navigation.popToTop();
```

------

🧬 **6. `replace(name, params?)`**

替换当前页面为另一个页面（不会留下历史记录）：

```js
navigation.replace('Login');
```

------

🔄 **7. `reset(state)`**

重置整个导航状态（例如清空所有页面并跳转到首页）：

```js
navigation.reset({
  index: 0,
  routes: [{ name: 'Home' }],
});
```

------

📍 **8. `setParams(params)`**

更新当前页面的参数（不会重新渲染页面组件）：

```js
navigation.setParams({ title: 'New Title' });
```

------

✅ 示例：组合使用

```js
navigation.navigate('Tabs', {
  screen: 'Profile',
  params: { userId: 1 },
});
```

------





## 3、本地存储

### 🔐 1. async-storage

✅ 是什么？

`AsyncStorage` 是一个**轻量级、异步的键值对存储系统**，类似于浏览器的 `localStorage`，适合用来缓存登录信息、用户设置、小型数据。

------

🔧 安装

```bash
npm install @react-native-async-storage/async-storage
npx pod-install
```

------

📦 常用 API

📝 保存数据

```tsx
await AsyncStorage.setItem('userToken', 'abc123');
```

📖 读取数据

```tsx
const token = await AsyncStorage.getItem('userToken');
```

❌ 删除某个键

```tsx
await AsyncStorage.removeItem('userToken');
```

🧹 清空所有数据（慎用！）

```tsx
await AsyncStorage.clear();
```

✅ 批量操作

```tsx
// 批量设置
await AsyncStorage.multiSet([
  ['user', 'tom'],
  ['age', '23']
]);

// 批量读取
const result = await AsyncStorage.multiGet(['user', 'age']);
console.log(result); // [['user', 'tom'], ['age', '23']]
```

------

📌 注意事项

- 所有 API 都是 **异步** 的，需要 `await`。
- 存储的是字符串，如需存对象，请使用 `JSON.stringify()` 和 `JSON.parse()`。

```tsx
await AsyncStorage.setItem('user', JSON.stringify({ name: 'Tom' }));
const user = JSON.parse(await AsyncStorage.getItem('user'));
```

------

💬 使用场景

- 登录 token 缓存
- 引导页是否已读
- 用户偏好设置
- 小型缓存数据（例如搜索历史）

### 🔒 2. keychain

✅ 是什么？

`Keychain` 是一种更**安全的本地数据存储方式**，可将用户敏感信息（如 token、密码）存储到系统级的 **iOS Keychain / Android Encrypted SharedPreferences** 中。

------

🔧 安装

```bash
npm install react-native-keychain
npx pod-install
```

> iOS 还需开启 Keychain 共享功能（在 Xcode Capabilities 中）

------

📦 常用 API

📝 保存账号密码

```tsx
import * as Keychain from 'react-native-keychain';

await Keychain.setGenericPassword('myUsername', 'myPassword');
```

------

📖 读取账号密码

```tsx
const credentials = await Keychain.getGenericPassword();
if (credentials) {
  console.log(`User: ${credentials.username}, Pass: ${credentials.password}`);
} else {
  console.log('No credentials stored');
}
```

------

❌ 删除存储信息

```tsx
await Keychain.resetGenericPassword();
```

------

🔑 存储 token 之类的单个值（仅存密码）

```tsx
await Keychain.setGenericPassword('token', 'abc123');
const data = await Keychain.getGenericPassword();
const token = data?.password;
```

------

🛡️ 高级选项（可加密 / 限制访问）

```tsx
await Keychain.setGenericPassword('username', 'password', {
  accessControl: Keychain.ACCESS_CONTROL.BIOMETRY_ANY, // 支持指纹/Face ID
  accessible: Keychain.ACCESSIBLE.WHEN_UNLOCKED_THIS_DEVICE_ONLY,
  authenticationPrompt: {
    title: '请验证指纹/Face ID'
  },
});
```

------

💬 使用场景

- 存储用户名/密码
- 存储登录 token（比 AsyncStorage 更安全）
- 开启生物识别登录（Face ID、指纹）
- 金融类、企业类 App 推荐使用

------

#### 🔍 AsyncStorage vs Keychain 对比

| 特性         | AsyncStorage           | Keychain                                                  |
| ------------ | ---------------------- | --------------------------------------------------------- |
| 数据类型     | 字符串（可转对象）     | 用户名 + 密码形式（或单独密码）                           |
| 是否加密     | ❌ 否                   | ✅ 是（使用系统级加密）                                    |
| 存储位置     | 应用内部存储（非加密） | 系统级安全存储（iOS Keychain / Android EncryptedStorage） |
| 是否可被窃取 | 相对较高风险           | 安全性更高                                                |
| 常用场景     | 缓存、偏好设置         | 登录凭证、token、安全信息                                 |

------

#### 📦 推荐用法组合

- 登录场景中：
  - token 用 `Keychain` 存储
  - 是否已登录、用户设置用 `AsyncStorage` 存储

------



### 🔐 Keychain高级选项

```tsx
await Keychain.setGenericPassword(username, password, options);
```

`options` 支持多个高级属性，下面我将它们按分类讲解👇

------

🛡️ 1. `accessControl`（访问控制）

指定存储数据的访问方式，例如是否需要 **生物识别（指纹、Face ID）或设备密码**。

可选值：

| 值                                    | 描述                                     |
| ------------------------------------- | ---------------------------------------- |
| `ACCESS_CONTROL.USER_PRESENCE`        | 只要用户验证过一次（如解锁屏幕）即可访问 |
| `ACCESS_CONTROL.BIOMETRY_ANY`         | 允许任意形式的生物识别（Face ID 或指纹） |
| `ACCESS_CONTROL.BIOMETRY_CURRENT_SET` | 当前设备注册的生物识别                   |
| `ACCESS_CONTROL.DEVICE_PASSCODE`      | 需要设备密码验证                         |
| `ACCESS_CONTROL.APPLICATION_PASSWORD` | 应用自定义密码（很少用）                 |

✅ 示例：强制 Face ID / 指纹验证才能访问

```tsx
await Keychain.setGenericPassword('user', 'secure123', {
  accessControl: Keychain.ACCESS_CONTROL.BIOMETRY_ANY,
});
```

------

🔑 2. `accessible`（数据访问条件）

控制何时可以访问 Keychain 中的数据，比如设备是否解锁、是否为当前设备。

常见值：

| 值                                          | 含义                                           |
| ------------------------------------------- | ---------------------------------------------- |
| `ACCESSIBLE.WHEN_UNLOCKED`                  | 设备解锁时可访问                               |
| `ACCESSIBLE.WHEN_UNLOCKED_THIS_DEVICE_ONLY` | 仅当前设备解锁时可访问，不支持 iCloud 备份恢复 |
| `ACCESSIBLE.ALWAYS`                         | 永远可访问（⚠️ 不推荐）                         |
| `ACCESSIBLE.AFTER_FIRST_UNLOCK`             | 第一次解锁后即使锁屏也可访问                   |

✅ 示例：设备解锁后，且仅当前设备能访问

```tsx
await Keychain.setGenericPassword('user', 'pass', {
  accessible: Keychain.ACCESSIBLE.WHEN_UNLOCKED_THIS_DEVICE_ONLY
});
```

------

🔏 3. `authenticationPrompt`（认证弹窗）

用于 iOS，当访问需要验证时自定义弹窗提示内容。

```tsx
await Keychain.getGenericPassword({
  authenticationPrompt: {
    title: '请验证以解锁',
    subtitle: '使用 Face ID / 指纹',
    description: '访问敏感信息需要验证',
    cancel: '取消'
  }
});
```

------

📱 4. `service`（自定义存储命名空间）

每个 `service` 相当于一个独立的“Keychain 区块”，可以按模块或账号区分存储。

```tsx
await Keychain.setGenericPassword('user', 'pass', {
  service: 'com.myapp.userToken'
});
```

------

🧠 5. `securityLevel`（Android 专属）

控制加密等级：

| 值                               | 含义                              |
| -------------------------------- | --------------------------------- |
| `SECURITY_LEVEL.ANY`             | 任意加密方案                      |
| `SECURITY_LEVEL.SECURE_SOFTWARE` | 软件加密                          |
| `SECURITY_LEVEL.SECURE_HARDWARE` | 硬件安全模块（如 TPM / Keystore） |

```tsx
await Keychain.setGenericPassword('u', 'p', {
  securityLevel: Keychain.SECURITY_LEVEL.SECURE_HARDWARE
});
```

------

💡 6. 组合示例：开启生物认证 + 限制当前设备 + 自定义命名

```tsx
await Keychain.setGenericPassword('tom', 'superSecret123', {
  accessControl: Keychain.ACCESS_CONTROL.BIOMETRY_CURRENT_SET,
  accessible: Keychain.ACCESSIBLE.WHEN_UNLOCKED_THIS_DEVICE_ONLY,
  service: 'com.myapp.login',
});
```

然后读取时：

```tsx
const result = await Keychain.getGenericPassword({
  authenticationPrompt: {
    title: '请通过指纹或Face ID验证'
  },
  service: 'com.myapp.login'
});
```

------

✅ 总结：常用组合推荐

| 场景                       | 推荐配置                                               |
| -------------------------- | ------------------------------------------------------ |
| 普通敏感数据（无 Face ID） | `accessible: WHEN_UNLOCKED_THIS_DEVICE_ONLY`           |
| 需要 Face ID / 指纹验证    | `accessControl: BIOMETRY_ANY` + `authenticationPrompt` |
| 不可被云端恢复             | `accessible: WHEN_UNLOCKED_THIS_DEVICE_ONLY`           |
| 支持多模块存储             | 使用不同的 `service` 名称                              |

------

### 🧠  MMKV 是什么？

**MMKV** 是腾讯开源的一个高性能 Key-Value 本地持久化组件，原本用于微信中替代 NSUserDefaults / SharedPreferences，特性是：

- 内部使用 mmap（内存映射）+ protobuf 编码。
- 读写效率极高，适合频繁读写小数据。
- 支持加密，线程安全。

`react-native-mmkv` 就是对这个 MMKV 的 React Native 封装。

------

🔧 2. API 详细讲解

📌 创建实例

```tsx
import { MMKV } from 'react-native-mmkv';

const storage = new MMKV({
  id: 'my-app', // 可选，默认是 'mmkv.default'
  path: 'custom/path', // 可选，自定义存储路径
  encryptionKey: 'super-secret-key', // 可选，启用加密
});
```

------

📌 存储数据

```tsx
storage.set('isLogin', true);
storage.set('token', 'abc123');
storage.set('age', 25);
storage.set('profile', JSON.stringify({ name: 'Tom', age: 20 }));
```

> ⚠️ 不能直接存对象或数组，需要手动 `JSON.stringify()`。

------

📌 读取数据

```tsx
const isLogin = storage.getBoolean('isLogin'); // true
const token = storage.getString('token'); // 'abc123'
const age = storage.getNumber('age'); // 25

const profile = JSON.parse(storage.getString('profile') || '{}');
```

------

📌 删除 / 清除

```tsx
storage.delete('token');
storage.clearAll(); // 清空所有键值
```

------

📌 获取所有 Key、判断是否存在

```tsx
const allKeys = storage.getAllKeys();
const hasToken = storage.contains('token'); // true / false
```

------

⚡ 3. 性能对比（vs AsyncStorage）

| 操作         | AsyncStorage | MMKV                    |
| ------------ | ------------ | ----------------------- |
| 写入一个键值 | 慢（异步）   | 快（同步）              |
| 读取键值     | 慢           | 极快                    |
| 支持数据类型 | string       | string、number、boolean |
| 多实例支持   | ❌            | ✅                       |
| 加密支持     | ❌            | ✅                       |
| 平台支持     | RN 全平台    | RN 全平台               |

**MMKV 优势场景**：

- 高频读取（如：token、语言设置、用户ID）
- 冷启动时读取配置（同步读取更快）
- 小体积本地缓存
- 状态持久化（配合 Zustand、Redux）

------

📦 4. 项目封装建议

建议封装一个 storage 工具类或模块：

```tsx
// storage.ts
import { MMKV } from 'react-native-mmkv';

const storage = new MMKV();

export const setItem = (key: string, value: any) => {
  if (typeof value === 'object') {
    storage.set(key, JSON.stringify(value));
  } else {
    storage.set(key, value);
  }
};

export const getItem = (key: string) => {
  const value = storage.getString(key);
  try {
    return JSON.parse(value ?? '');
  } catch {
    return value;
  }
};

export const removeItem = (key: string) => {
  storage.delete(key);
};

export const clearStorage = () => {
  storage.clearAll();
};
```

------

🧪 5. 状态管理 + MMKV 持久化（如 Zustand）

```tsx
import { create } from 'zustand';
import { MMKV } from 'react-native-mmkv';

const storage = new MMKV();

export const useAuthStore = create((set) => ({
  token: storage.getString('token') || '',
  setToken: (token: string) => {
    storage.set('token', token);
    set({ token });
  },
  logout: () => {
    storage.delete('token');
    set({ token: '' });
  },
}));
```

这样状态和存储同步，刷新也不会丢失。

------

🧰 6. 实战建议

| 场景                      | 建议                              |
| ------------------------- | --------------------------------- |
| 存 token、用户ID、登录态  | ✅ MMKV                            |
| 本地缓存用户偏好设置      | ✅ MMKV                            |
| 存储大对象 / 多层嵌套数据 | ❌ 慎用，考虑 SQLite、WatermelonDB |
| 存储图片、Base64、二进制  | ✅ 支持 Buffer                     |
| 和状态库集成做持久化      | ✅ Zustand、Jotai 都很适合         |

------

如果你告诉我你现在要开发什么功能（比如登录、偏好设置、缓存数据等），我可以直接帮你设计一个完整的存储模块或封装方案。要不要？





## 4、其他组件

###  	4.1  🧩QR

`qrcode.react` 是一个用来在 React 项目中生成二维码的库，基于 `qrcode` 和 `React` 封装，使用简单，功能实用。

------

🧩 安装方法

```bash
npm install qrcode.react
# 或者
yarn add qrcode.react
```

------

🔧 基本用法

```tsx
import { QRCode } from 'qrcode.react';

function MyComponent() {
  return (
    <QRCode value="https://example.com" />
  );
}
```

------

🔍 常用 Props



| 属性            | 类型                    | 说明                       |
| --------------- | ----------------------- | -------------------------- |
| `value`         | `string`                | **二维码内容**，必须填写   |
| `size`          | `number`                | 尺寸（宽高），默认 128     |
| `fgColor`       | `string`                | 前景色，默认 `#000000`     |
| `bgColor`       | `string`                | 背景色，默认 `#ffffff`     |
| `level`         | `'L' | 'M' | 'Q' | 'H'` | 容错级别，默认 `'L'`（低） |
| `includeMargin` | `boolean`               | 是否包含边距，默认 `false` |
| `renderAs`      | `'canvas' | 'svg'`      | 渲染方式，默认 `canvas`    |

------

🖼 示例：带颜色和 svg 渲染

```tsx
<QRCode
  value="https://yourapp.com"
  size={256}
  bgColor="#F0F0F0"
  fgColor="#1A73E8"
  level="H"
  includeMargin={true}
  renderAs="svg"
/>
```

------

📤 获取二维码数据（如 base64）

```tsx
import { useRef, useEffect } from 'react';
import { QRCode } from 'qrcode.react';

function QRCodeWithExport() {
  const qrRef = useRef(null);

  useEffect(() => {
    const canvas = qrRef.current?.querySelector('canvas');
    if (canvas) {
      const dataURL = canvas.toDataURL();
      console.log('Base64 QR:', dataURL);
      // 你可以将 dataURL 用于下载、展示等
    }
  }, []);

  return (
    <div ref={qrRef}>
      <QRCode value="https://example.com" />
    </div>
  );
}
```

------

🧠 总结

- `qrcode.react` 是一个轻量但功能齐全的二维码生成工具
- 可自定义样式、容错等级、渲染类型
- 适合需要快速集成二维码的 React 项目

------



`qrcode.react` **不能直接在 React Native（RN）中使用**，因为它依赖于 DOM 和 HTML 的渲染能力（比如 `<canvas>` 和 `<svg>`），而这些在 React Native 中并不支持。

✅ 在 React Native 中生成二维码的正确做法：

你可以使用 **专为 React Native 设计的二维码组件库**。最常用的是：

------

1. [`react-native-qrcode-svg`](https://github.com/awesomejerry/react-native-qrcode-svg)

📦 安装：

```bash
npm install react-native-qrcode-svg
```

> 如果你还没安装 `react-native-svg`，需要一起装：

```bash
npm install react-native-svg
```

> 并根据平台进行链接（如果你不是用 Expo）：

```bash
npx pod-install
```

------

🧪 基本用法：

```tsx
import QRCode from 'react-native-qrcode-svg';
import React from 'react';
import { View } from 'react-native';

export default function MyQRCode() {
  return (
    <View>
      <QRCode
        value="https://example.com"
        size={200}
        color="black"
        backgroundColor="white"
      />
    </View>
  );
}
```

------

🖼 支持嵌入 logo：

```tsx
<QRCode
  value="https://example.com"
  logo={{ uri: 'https://example.com/logo.png' }}
  logoSize={30}
/>
```

------

2. 如果你使用 Expo：

`react-native-qrcode-svg` 也兼容 Expo，不需要额外链接原生模块，只需：

```bash
npx expo install react-native-svg react-native-qrcode-svg
```

------

🔚 总结



| 库                        | 支持平台     | 是否支持 RN | 支持 logo |
| ------------------------- | ------------ | ----------- | --------- |
| `qrcode.react`            | React（Web） | ❌ 不支持    | ✔         |
| `react-native-qrcode-svg` | React Native | ✅ 支持      | ✔         |

------



### 4.2  ⚙️Modal

✅ 最简单方式：使用 `ActivityIndicator` + `Modal`

你已经有 `Modal` 的结构了，可以配合 `ActivityIndicator` 加一个全屏 Loading：

------

✅ 步骤一：引入 Loading 所需组件

```tsx
import { ActivityIndicator } from 'react-native';
```

------

✅ 步骤二：添加一个 `loading` 状态

```tsx
const [loading, setLoading] = useState(false);
```

------

✅ 步骤三：请求前后更新 loading 状态

```tsx
const getUserInfoF = async () => {
  setLoading(true); // 开始 loading
  try {
    let data = {
      userEmail: 'Jack-JK.Ye@aia.com',
      Password: '123456',
    };
    let res = await getUserInfo(data, '/workflows/...');
    console.log('获取用户信息', res);
    setData(res);
    res && setVisible(false);
  } catch (error) {
    Alert.alert('请求失败', error.message);
  } finally {
    setLoading(false); // 结束 loading
  }
};
```

------

✅ 步骤四：添加 Loading Modal 组件

放在 `return` 的最下面：

```tsx
<Modal visible={loading} transparent={true} animationType="none">
  <View style={styles.loadingOverlay}>
    <ActivityIndicator size="large" color="#d31145" />
    <Text style={{ marginTop: 10, color: '#fff' }}>加载中...</Text>
  </View>
</Modal>
```

------

✅ 步骤五：补充样式

在 `StyleSheet.create` 里添加：

```tsx
loadingOverlay: {
  flex: 1,
  justifyContent: 'center',
  alignItems: 'center',
  backgroundColor: 'rgba(0, 0, 0, 0.5)', // 半透明遮罩
},
```

------

✅ 完成后效果：

- 用户点击按钮后页面会显示一个居中的 loading 动画；
- 请求完成后自动隐藏；
- 背景是半透明遮罩，无法操作页面内容。

------

### 4.3  🔔下拉刷新

✅ 基本用法（搭配 ScrollView）

你可以在你当前页面的 `ScrollView` 上添加 `refreshControl`：

✅ 步骤一：引入组件

```tsx
import { RefreshControl } from 'react-native';
```

------

✅ 步骤二：添加两个状态

```tsx
const [refreshing, setRefreshing] = useState(false);
```

------

✅ 步骤三：创建刷新函数

```tsx
const onRefresh = async () => {
  setRefreshing(true);
  // 模拟异步加载
  await getUserInfoF(); // 调用你已有的请求函数
  setRefreshing(false);
};
```

------

✅ 步骤四：给 ScrollView 添加 `refreshControl`

找到你原来的 `ScrollView`，修改如下：

```tsx
<ScrollView
  contentContainerStyle={styles.scrollContainer}
  refreshControl={
    <RefreshControl
      refreshing={refreshing}
      onRefresh={onRefresh}
      colors={['#d31145']} // Android 的加载颜色
      tintColor="#d31145"   // iOS 加载颜色
    />
  }
>
```

------

✅ 最终效果：

- 下拉会触发 `onRefresh` 方法；
- 会显示加载动画；
- `refreshing` 设置为 `false` 后自动结束加载。

------

✅ 其他可选参数：



| 参数                      | 说明                             |
| ------------------------- | -------------------------------- |
| `refreshing`              | 是否在加载中（必填）             |
| `onRefresh`               | 下拉时触发的函数（必填）         |
| `colors`                  | Android 下的加载动画颜色（数组） |
| `tintColor`               | iOS 下加载动画的颜色             |
| `title`                   | iOS 的提示文本                   |
| `progressBackgroundColor` | Android 的背景色                 |

------



### 4.4  🔲ICON组件



### 4.5 📷调用摄像头

✅ 方式一：`react-native-image-picker`（你原来使用的）

⭐ 特点：

- 适合快速打开系统相机或相册。
- 支持拍照、录像、选择媒体文件。
- 使用系统 UI，操作简单。

📦 安装：

```bash
npm install react-native-image-picker
```

📋 权限配置（Android）：

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

📖 示例代码：

```tsx
import {launchCamera} from 'react-native-image-picker';

const openCamera = () => {
  const options = { mediaType: 'photo', cameraType: 'back', saveToPhotos: true };
  launchCamera(options, (response) => {
    if (response.didCancel) console.log('用户取消了拍摄');
    else if (response.errorCode) console.error('打开失败:', response.errorMessage);
    else console.log('照片信息:', response.assets);
  });
};
```

✅ 优点：

- 快速集成，无需自定义 UI。
- 支持拍照、录像。

❌ 缺点：

- 无法自定义 UI。
- 无法实时预览相机画面。
- 不适合做扫码、AR 等实时处理场景。

------

✅ 方式二：`react-native-vision-camera`（推荐用于高级功能）

⭐ 特点：

- 可自定义 UI 的摄像头库。
- 支持实时视频流、扫码、AR、人脸识别等。
- 性能高，适合复杂场景。

📦 安装：

```bash
npm install react-native-vision-camera
npx pod-install
```

📋 权限配置（Android）：

```xml
<uses-permission android:name="android.permission.CAMERA" />
```

📖 示例代码：

```tsx
import {Camera, useCameraDevices} from 'react-native-vision-camera';

const CameraScreen = () => {
  const devices = useCameraDevices();
  const device = devices.back;

  return (
    <Camera
      style={StyleSheet.absoluteFill}
      device={device}
      isActive={true}
    />
  );
};
```

✅ 优点：

- 自定义摄像头界面（比如加按钮、扫描框）。
- 性能优异，适合实时扫码或人脸识别。
- 支持第三方插件，如扫码库 `vision-camera-code-scanner`。

❌ 缺点：

- 配置稍复杂（权限、组件化）。
- 初期学习成本较高。

------

🔚 总结建议



| 场景                         | 推荐方式                       |
| ---------------------------- | ------------------------------ |
| 拍照、录像（简单用途）       | ✅ `react-native-image-picker`  |
| 扫码、AR、人脸识别等高级功能 | ✅ `react-native-vision-camera` |

------



### 4.6📜 常用权限总结

1. **摄像头权限**

- **描述**：允许应用访问设备的摄像头，进行拍照、录像、视频通话等操作。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.CAMERA" />
  ```

- **iOS 权限**：在 `Info.plist` 中添加：

  ```xml
  <key>NSCameraUsageDescription</key>
  <string>我们需要使用摄像头进行拍照</string>
  ```

------

2. **存储权限**

- **描述**：允许应用读写设备的存储空间，用于保存或读取文件。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  ```

  > **注意**：自 Android 11 起，`WRITE_EXTERNAL_STORAGE` 权限已被限制，推荐使用 `Scoped Storage`。

- **iOS 权限**：iOS 默认不需要显式请求存储权限，只需要通过文件选择器访问。

------

3. **位置权限**

- **描述**：允许应用获取设备的位置信息，适用于地图、定位等功能。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
  ```

- **iOS 权限**：在 `Info.plist` 中添加：

  ```xml
  <key>NSLocationWhenInUseUsageDescription</key>
  <string>我们需要使用位置来获取你的地理信息</string>
  <key>NSLocationAlwaysUsageDescription</key>
  <string>我们需要持续获取位置信息</string>
  ```

------

4. **麦克风权限**

- **描述**：允许应用访问设备的麦克风，用于语音录制、语音识别等功能。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  ```

- **iOS 权限**：在 `Info.plist` 中添加：

  ```xml
  <key>NSMicrophoneUsageDescription</key>
  <string>我们需要使用麦克风来录制音频</string>
  ```

------

5. **相册/文件读取权限**

- **描述**：允许应用访问设备的相册或文件管理，读取图片、视频等文件。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  ```

- **iOS 权限**：在 `Info.plist` 中添加：

  ```xml
  <key>NSPhotoLibraryUsageDescription</key>
  <string>我们需要访问相册来选择图片或视频</string>
  ```

------

6. **通知权限**

- **描述**：允许应用发送本地通知或推送通知。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.ACCESS_NOTIFICATION_POLICY" />
  ```

- **iOS 权限**：在 `Info.plist` 中添加：

  ```xml
  <key>UIBackgroundModes</key>
  <array>
    <string>fetch</string>
    <string>remote-notification</string>
  </array>
  ```

------

7. **蓝牙权限**

- **描述**：允许应用使用设备的蓝牙功能，例如扫描设备、连接设备。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.BLUETOOTH" />
  <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
  <uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
  ```

- **iOS 权限**：在 `Info.plist` 中添加：

  ```xml
  <key>NSBluetoothPeripheralUsageDescription</key>
  <string>我们需要使用蓝牙进行设备配对</string>
  ```

------

8. **传感器权限**

- **描述**：允许应用访问设备的传感器，例如加速计、陀螺仪等。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  ```

- **iOS 权限**：通常不需要特别权限，但需要根据使用的传感器来配置。

------

9. **电话权限**

- **描述**：允许应用拨打电话、查看电话状态。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.CALL_PHONE" />
  ```

- **iOS 权限**：没有专门的电话权限，但需要实现拨打电话的功能。

------

10. **短信权限**

- **描述**：允许应用读取或发送短信。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.SEND_SMS" />
  <uses-permission android:name="android.permission.READ_SMS" />
  ```

- **iOS 权限**：没有直接的短信权限，但可以通过 `MFMessageComposeViewController` 来发送短信。

------

11. **后台任务权限**

- **描述**：允许应用在后台运行时执行特定任务，如拉取数据。

- **Android 权限**：

  ```xml
  <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
  ```

- **iOS 权限**：在 `Info.plist` 中添加：

  ```xml
  <key>UIBackgroundModes</key>
  <array>
    <string>fetch</string>
    <string>remote-notification</string>
  </array>
  ```

------

🔚 总结：

- **Android** 和 **iOS** 权限配置有所不同，需要根据平台特性分别配置。
- 特定功能的权限（如摄像头、麦克风、位置、存储等）需要在 `AndroidManifest.xml` 和 `Info.plist` 中配置。
- 自 Android 6.0 (API 23) 起，Android 引入了 **动态权限申请**，需要在代码中请求用户授权。

------



### 4.7 📦 React Native 环境变量

✅ 安装

使用 `npm` 或 `yarn` 安装：

```bash
npm install react-native-config
# 或
yarn add react-native-config
```

------

✅ 创建 `.env` 文件

在项目根目录创建 `.env` 文件，并添加环境变量：

```bash
API_URL=https://api.example.com
APP_NAME=MyApp
```

支持多个环境文件：

- `.env`（默认）
- `.env.development`
- `.env.production`
- `.env.staging`

------

✅ 在代码中使用变量

```tsx
import Config from 'react-native-config';

console.log(Config.API_URL); // 输出: https://api.example.com
```

------

✅ 多环境支持

iOS 配置（Xcode）：

1. 打开 Xcode -> 选择你的 Target
2. 点击 `Build Settings`
3. 搜索 `Build Arguments` 或 `Preprocessor Macros`
4. 添加变量（如）：`ENVFILE=.env.production`

或使用 CLI 指定环境：

```bash
ENVFILE=.env.staging react-native run-ios
```

------

Android 配置：

确保在 `android/app/build.gradle` 中已添加：

```xml
apply from: project(':react-native-config').projectDir.getPath() + "/dotenv.gradle"
```

然后使用 CLI 运行：

```bash
ENVFILE=.env.staging react-native run-android
```

------

⚠️ 注意事项

- 每次修改 `.env` 后需要重新构建项目（不能只热重载）。
- 环境变量在构建时写入，**不能运行时动态修改**。
- 不要在 `.env` 中放敏感信息（如密码），仍可能被反编译查看。

------



### 4.8  🔔Notification （通知）

🔔 一、`react-native-push-notification` 是什么？

这是一个用于管理本地通知（Local Notification）和远程通知（Push Notification）的库。它可以处理：

- 定时通知
- 本地通知
- 推送通知（需配合 FCM）

------

 

1️⃣ 安装依赖

```bash
npm install react-native-push-notification
```

> 如果你使用的是 RN >= 0.60，会自动 link，无需手动 link。

------

2️⃣ Android 配置（重要 ⚠️）

a. 添加 Firebase 支持（用于远程推送）

- 添加 `google-services.json` 到 `android/app/`
- 修改 `android/build.gradle`：

```bash
classpath 'com.google.gms:google-services:4.3.10'
```

- 修改 `android/app/build.gradle`：

```bash
apply plugin: 'com.google.gms.google-services'
```

b. 修改 `AndroidManifest.xml`

```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
<uses-permission android:name="android.permission.VIBRATE"/>
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/> <!-- Android 13+ -->

<application>
  <receiver android:name="com.dieam.reactnativepushnotification.modules.RNPushNotificationPublisher" android:exported="true"/>
  <receiver android:name="com.dieam.reactnativepushnotification.modules.RNPushNotificationBootEventReceiver" android:exported="true">
    <intent-filter>
      <action android:name="android.intent.action.BOOT_COMPLETED"/>
    </intent-filter>
  </receiver>
</application>
```

------

3️⃣ iOS 配置

- 确保启用了 `Push Notifications` 和 `Background Modes` > `Remote notifications`
- 修改 `AppDelegate.m` 来注册通知

```xml
#import <UserNotifications/UserNotifications.h>
#import <RNCPushNotificationIOS.h>

// 在 didFinishLaunchingWithOptions 添加
UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
center.delegate = self;
```

------

🧪 三、初始化通知配置

你需要在 App 启动时初始化配置通知行为：

```tsx
import PushNotification from 'react-native-push-notification';

PushNotification.configure({
  onRegister: function (token) {
    console.log('TOKEN:', token); // FCM 或 APNs 的 token
  },

  onNotification: function (notification) {
    console.log('NOTIFICATION:', notification);

    // 处理用户点击通知
    notification.finish(PushNotificationIOS.FetchResult.NoData);
  },

  permissions: {
    alert: true,
    badge: true,
    sound: true,
  },

  popInitialNotification: true,
  requestPermissions: true,
});
```

------

🔔 四、常用 API 示例

🎯 显示本地通知

```tsx
PushNotification.localNotification({
  channelId: "default-channel-id", // Android 必须
  title: "本地通知标题",
  message: "这是通知内容",
});
```

⏰ 定时通知

```tsx
PushNotification.localNotificationSchedule({
  channelId: "default-channel-id",
  message: "这是定时通知",
  date: new Date(Date.now() + 5 * 1000), // 5 秒后
});
```

✅ 创建 Android 通知频道

```tsx
PushNotification.createChannel(
  {
    channelId: "default-channel-id",
    channelName: "默认通道",
    importance: 4,
  },
  (created) => console.log(`createChannel returned '${created}'`)
);
```

------

📲 五、远程推送配合 FCM 使用（简述）

- 配置 Firebase 和 FCM，获取服务端推送的 FCM Token（通过 `onRegister` 获取）
- 后端向这个 Token 发送消息
- App 会收到通知，`onNotification` 被触发
- 如果前台收到消息但没有自动展示通知，可以手动调用 `localNotification` 展示

------

✅ 总结对比



| 功能     | 是否支持     | 说明                               |
| -------- | ------------ | ---------------------------------- |
| 本地通知 | ✅            | 使用 `.localNotification`          |
| 定时通知 | ✅            | 使用 `.localNotificationSchedule`  |
| 远程推送 | ✅            | 需配合 FCM，使用 `.configure` 监听 |
| iOS 支持 | ✅            | 需配置 `AppDelegate.m`             |
| 通知频道 | ✅（Android） | 必须创建才能显示通知               |

------

🎯 二、`@react-native-firebase/messaging` 是什么？

这是 React Native 官方推荐的 Firebase 插件之一，专用于处理 **Firebase Cloud Messaging (FCM)** 的功能，包括：

- 获取设备的 **FCM Token**
- 接收 **远程推送通知**
- 处理 **前台、后台、杀死状态下** 的推送消息
- 处理 **数据消息**（后台执行自定义逻辑）

------

🧰 二、安装与配置

1️⃣ 安装依赖

```bash
npm install @react-native-firebase/app
npm install @react-native-firebase/messaging
```

------

2️⃣ Firebase 控制台配置

- 在 Firebase 控制台 创建项目
- 添加 Android/iOS 应用
- 下载并放置配置文件：
  - Android：`google-services.json` → `android/app/`
  - iOS：`GoogleService-Info.plist` → `ios/`

------

3️⃣ Android 配置

`android/build.gradle`

```bash
buildscript {
  dependencies {
    classpath 'com.google.gms:google-services:4.3.10'
  }
}
```

`android/app/build.gradle`

```xml
apply plugin: 'com.google.gms.google-services'
```

Android 权限（`AndroidManifest.xml`）

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/> <!-- Android 13+ -->
```

------

4️⃣ iOS 配置

- 启用通知功能（`Push Notifications` 和 `Background Modes`）
- 修改 `AppDelegate.m` 处理通知授权
- 安装 CocoaPods

```
cd ios
pod install
```

------

🧩 三、常用 API 和使用场景

1️⃣ 请求权限 & 获取 FCM Token

```tsx
import messaging from '@react-native-firebase/messaging';

// 请求权限（iOS）或检查权限（Android 13+）
const requestPermission = async () => {
  const authStatus = await messaging().requestPermission();
  const enabled =
    authStatus === messaging.AuthorizationStatus.AUTHORIZED ||
    authStatus === messaging.AuthorizationStatus.PROVISIONAL;

  if (enabled) {
    console.log('Authorization status:', authStatus);
  }
};

// 获取 FCM Token
const getFcmToken = async () => {
  const token = await messaging().getToken();
  console.log('FCM Token:', token);
  return token;
};
```

------

2️⃣ 监听消息

前台监听消息（App 打开状态）

```tsx
messaging().onMessage(async remoteMessage => {
  console.log('📩 Foreground message:', remoteMessage);
  // 你可以手动显示一个通知（结合 Notifee 或其他库）
});
```

后台监听消息

```tsx
messaging().setBackgroundMessageHandler(async remoteMessage => {
  console.log('📩 Background message:', remoteMessage);
});
```

App 被杀死时被通知唤醒

```tsx
// 获取点击通知启动 app 的消息
messaging()
  .getInitialNotification()
  .then(remoteMessage => {
    if (remoteMessage) {
      console.log('App opened by notification:', remoteMessage);
    }
  });
```

------

3️⃣ 删除 Token（登出时可用）

```tsx
await messaging().deleteToken();
```

------

🚀 四、完整示例整合

```tsx
import { useEffect } from 'react';
import messaging from '@react-native-firebase/messaging';

export const useFCM = () => {
  useEffect(() => {
    const init = async () => {
      await messaging().requestPermission();
      const token = await messaging().getToken();
      console.log('FCM Token:', token);

      // Foreground
      const unsubscribe = messaging().onMessage(async remoteMessage => {
        console.log('Message in foreground:', remoteMessage);
      });

      // Background
      messaging().setBackgroundMessageHandler(async remoteMessage => {
        console.log('Message in background:', remoteMessage);
      });

      return unsubscribe;
    };

    init();
  }, []);
};
```

------

🔥 五、消息类型说明



| 类型                     | 说明                                               |
| ------------------------ | -------------------------------------------------- |
| **Notification Message** | 有 title 和 body，系统处理 UI 展示                 |
| **Data Message**         | 纯数据，开发者自定义处理（适合前台展示、静默通知） |

------

✅ 六、和其他库（如 Notifee）配合

- `@react-native-firebase/messaging` 主要处理接收推送、获取 token

- **Notifee** 用于前台自定义通知展示，例如：

  ```tsx
  import notifee from '@notifee/react-native';
  
  notifee.displayNotification({
    title: remoteMessage.notification?.title,
    body: remoteMessage.notification?.body,
    android: {
      channelId: 'default',
    },
  });
  ```

------

🧠 七、总结



| 功能                                 | 支持 |
| ------------------------------------ | ---- |
| 获取设备 Token                       | ✅    |
| 接收远程推送通知（前台/后台/杀死）   | ✅    |
| 自定义前台通知展示（需结合 Notifee） | ✅    |
| 设置后台处理函数                     | ✅    |
| 支持 Android & iOS                   | ✅    |

------

如果你想，我可以接下来帮你写一个完整的封装模块 `useFirebaseMessaging` 或者写一个带 UI 的通知测试页面，你更想要哪一种？



🚨**Notifee** 

是一个功能强大的 React Native 库，用于处理本地通知的展示和管理。它可以创建、更新、删除、调度通知，并提供丰富的自定义选项来实现本地通知的多样化需求。相比于 React Native 默认的通知库（如 `PushNotificationIOS`），Notifee 提供了更为强大和灵活的通知功能，特别是在 Android 平台上，Notifee 支持更多的高级功能，比如通知渠道、通知组、以及多媒体通知。

主要特点

- **多平台支持**：支持 iOS 和 Android。
- **通知渠道（Android）**：提供通知频道的创建和管理，使得应用可以控制不同类型通知的行为（如声音、震动等）。
- **定时通知**：可以调度通知，设定通知的触发时间。
- **本地通知的复杂展示**：支持大文本、图片、按钮等丰富展示效果。
- **用户交互**：支持点击通知打开应用并传递数据、以及自定义操作按钮。

------

📦 一、安装与配置

1️⃣ 安装依赖

```bash
npm install @notifee/react-native
```

2️⃣ 配置

iOS 配置

- 在 `ios/Podfile` 中确保有如下依赖：

```bash
pod 'notifee/react-native', :path => '../node_modules/@notifee/react-native'
```

- 在 `AppDelegate.m` 中添加以下代码来处理通知权限：

```bash
#import <UserNotifications/UserNotifications.h>
#import <Notifee/Notifee.h>

// 在 didFinishLaunchingWithOptions 方法内添加
[NotifeeModule register];
```

- 然后执行 `pod install` 以完成配置。

Android 配置

- 在 `AndroidManifest.xml` 中添加所需的权限：

```xml
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/> <!-- Android 13+ -->
<uses-permission android:name="android.permission.VIBRATE"/>
```

- 在 `MainApplication.java` 中初始化 Notifee：

```java
import io.invertase.notifee.NotifeePackage;

@Override
protected List<ReactPackage> getPackages() {
  return Arrays.<ReactPackage>asList(
      new MainReactPackage(),
      new NotifeePackage() // 添加 Notifee 包
  );
}
```

------

🧩 二、常用 API

1️⃣ 请求权限

在显示通知之前，你需要请求通知权限（iOS）。

```tsx
import notifee from '@notifee/react-native';

const requestPermission = async () => {
  const settings = await notifee.requestPermission();
  console.log('Permission settings:', settings);
  return settings;
};
```

2️⃣ 创建通知频道（Android）

在 Android 上，你必须创建一个通知频道（Notification Channel），以便管理通知的行为（声音、振动、优先级等）。每个通知必须指定一个频道。

```tsx
import notifee from '@notifee/react-native';

const createChannel = async () => {
  const channelId = await notifee.createChannel({
    id: 'default',
    name: 'Default Channel',
    importance: 4,  // 高优先级
    sound: 'default',
    vibration: true,
  });
  console.log('Created channel with ID:', channelId);
};
```

3️⃣ 显示通知

使用 `displayNotification` 来显示通知。你可以在通知中添加标题、内容、图标等。

```tsx
const displayNotification = async () => {
  await notifee.displayNotification({
    title: 'Hello, world!',
    body: 'This is a sample notification.',
    android: {
      channelId: 'default',
      smallIcon: 'ic_launcher',
      color: '#00FF00', // 可选，设置颜色
    },
  });
};
```

4️⃣ 定时通知（调度通知）

你可以设置定时通知，通知将在特定的时间点触发。

```tsx
const scheduleNotification = async () => {
  await notifee.createTriggerNotification(
    {
      title: 'Scheduled Notification',
      body: 'This notification will be triggered at a specific time.',
      android: {
        channelId: 'default',
        smallIcon: 'ic_launcher',
      },
    },
    {
      type: notifee.TriggerType.TIMESTAMP,  // 按时间戳触发
      timestamp: Date.now() + 60000, // 1 分钟后
    }
  );
};
```

5️⃣ 处理通知点击事件

你可以监听通知点击事件，以便用户点击通知后打开特定的页面。

```tsx
notifee.onForegroundEvent(({ type, detail }) => {
  if (type === notifee.EventType.PRESS) {
    console.log('Notification pressed:', detail.notification);
    // 你可以根据通知的内容进行跳转或其他操作
  }
});
```

6️⃣ 更新通知

Notifee 还允许你更新已经显示的通知。例如，更新通知内容或状态。

```tsx
const updateNotification = async (notificationId) => {
  await notifee.displayNotification({
    id: notificationId,
    title: 'Updated Notification Title',
    body: 'Updated content goes here...',
    android: {
      channelId: 'default',
      smallIcon: 'ic_launcher',
    },
  });
};
```

------

📱 三、平台适配

iOS

- 在 iOS 上，Notifee 会自动处理用户的通知权限请求，并使用 `UNNotificationRequest` 来管理通知。
- iOS 需要处理 `AppDelegate.m`，确保通知的正确初始化。

Android

- **Android 8.0+** 需要通知频道（Notification Channel）支持。
- 在 Android 上，Notifee 提供了更灵活的通知行为设置，包括优先级、声音、振动等。

------

🧠 四、总结



| 功能                | 支持 | 说明                                          |
| ------------------- | ---- | --------------------------------------------- |
| 请求权限            | ✅    | 通过 `requestPermission` 请求权限             |
| 本地通知展示        | ✅    | 使用 `displayNotification` 展示               |
| 定时通知            | ✅    | 使用 `createTriggerNotification` 设置定时通知 |
| 更新通知            | ✅    | 可以通过 ID 更新通知内容                      |
| 通知渠道（Android） | ✅    | 必须创建频道来控制通知的行为                  |
| 处理点击事件        | ✅    | 监听 `onForegroundEvent` 处理点击事件         |

------

🌟 五、示例代码

结合上面讲解的功能，以下是一个简单的例子：

```tsx
import React, { useEffect } from 'react';
import { Button } from 'react-native';
import notifee from '@notifee/react-native';

const App = () => {
  useEffect(() => {
    const init = async () => {
      await notifee.requestPermission();
      await notifee.createChannel({
        id: 'default',
        name: 'Default Channel',
        importance: 4,
      });
    };
    init();
  }, []);

  const showNotification = async () => {
    await notifee.displayNotification({
      title: 'Hello!',
      body: 'This is a sample notification.',
      android: {
        channelId: 'default',
        smallIcon: 'ic_launcher',
      },
    });
  };

  const scheduleNotification = async () => {
    await notifee.createTriggerNotification(
      {
        title: 'Scheduled Notification',
        body: 'This will show after 10 seconds.',
        android: {
          channelId: 'default',
          smallIcon: 'ic_launcher',
        },
      },
      {
        type: notifee.TriggerType.TIMESTAMP,
        timestamp: Date.now() + 10000, // 10 秒后
      }
    );
  };

  return (
    <>
      <Button title="Show Notification" onPress={showNotification} />
      <Button title="Schedule Notification" onPress={scheduleNotification} />
    </>
  );
};

export default App;
```

这样，你就可以实现一个简单的本地通知展示和调度。



### 4.9  📚 Selector

📚 React Native - Selector 选择器组件总结

🎯 1. 官方推荐的基础组件：`Picker`

- 来自独立库 `@react-native-picker/picker`
- 支持 iOS 和 Android 的原生选择器效果。

⚙️ 安装

```bash
npm install @react-native-picker/picker
```

💻 示例代码

```tsx
import { Picker } from '@react-native-picker/picker';
import { useState } from 'react';

function MySelector() {
  const [selectedValue, setSelectedValue] = useState('java');

  return (
    <Picker
      selectedValue={selectedValue}
      onValueChange={(itemValue, itemIndex) => setSelectedValue(itemValue)}
    >
      <Picker.Item label="Java" value="java" />
      <Picker.Item label="JavaScript" value="javascript" />
      <Picker.Item label="Python" value="python" />
    </Picker>
  );
}
```

------

🎨 2. 自定义 Modal 弹窗实现选择器

- 使用 `Modal + TouchableOpacity + FlatList` 组合自定义。
- 可以实现更炫酷的弹窗选择器样式。
- 适合需要自定义 UI 的场景（比如底部弹出、单选、多选等）。

------

🚀 3. 第三方选择器库推荐



| 📦 库名                                                       | ✨ 特点                         |
| ------------------------------------------------------------ | ------------------------------ |
| [`react-native-modal-selector`](https://github.com/peacechen/react-native-modal-selector) | 简单好用，支持 Modal 弹窗      |
| [`react-native-picker-select`](https://github.com/lawnstarter/react-native-picker-select) | 样式自定义强，支持 Placeholder |
| [`react-native-dropdown-picker`](https://github.com/hossein-zare/react-native-dropdown-picker) | 类似下拉菜单体验，功能丰富     |

📦 `react-native-picker-select` 示例

```tsx
npm install react-native-picker-select
import RNPickerSelect from 'react-native-picker-select';

function MySelector() {
  return (
    <RNPickerSelect
      onValueChange={(value) => console.log(value)}
      items={[
        { label: 'Football', value: 'football' },
        { label: 'Baseball', value: 'baseball' },
        { label: 'Hockey', value: 'hockey' },
      ]}
    />
  );
}
```

------

📝 小总结



| 方法                          | 适合场景                      |
| ----------------------------- | ----------------------------- |
| `@react-native-picker/picker` | 原生体验，快速简单            |
| 自定义 Modal                  | 需要高度定制 UI，符合设计规范 |
| 第三方库                      | 快速开发、丰富功能、样式自由  |

------

要不要我再帮你一版更 ✨**完整带目录的Markdown笔记版**？比如加 `[TOC]` 自动目录，适合直接用在 Obsidian、Notion 这些工具里～
 要的话跟我说！🚀



### 4.10 🖼️ ImageViewer

------

📚 常见方案



| 方案                                                         | 特点                                   |
| ------------------------------------------------------------ | -------------------------------------- |
| [`react-native-image-zoom-viewer`](https://github.com/ascoders/react-native-image-viewer) | 功能全，支持缩放、滑动切换、长按保存。 |
| [`react-native-image-viewing`](https://github.com/jobtoday/react-native-image-viewing) | 更轻量，简单查看大图，不需要太复杂。   |
| [`react-native-fast-image`](https://github.com/DylanVann/react-native-fast-image) + 自己封装Viewer | 性能极致，适合大规模高性能加载。       |

------

🛠️ 使用 `react-native-image-zoom-viewer`

安装

```bash
npm install react-native-image-zoom-viewer react-native-image-viewing
```

或

```bash
yarn add react-native-image-zoom-viewer react-native-image-viewing
```

基础用法示例

```tsx
import React from 'react';
import { Modal } from 'react-native';
import ImageViewer from 'react-native-image-zoom-viewer';

export default function MyImageViewer({ visible, onClose, images }) {
  return (
    <Modal visible={visible} transparent={true} onRequestClose={onClose}>
      <ImageViewer
        imageUrls={images}  // [{ url: 'https://example.com/image1.jpg' }]
        enableSwipeDown
        onSwipeDown={onClose}
        onCancel={onClose}
        saveToLocalByLongPress={false}
      />
    </Modal>
  );
}
```

调用示例：

```tsx
<MyImageViewer 
  visible={isViewerVisible}
  onClose={() => setViewerVisible(false)}
  images={[{ url: 'https://your-image-url.jpg' }]}
/>
```

------

⚡ 使用 `react-native-image-viewing`（更轻量）

示例

```tsx
import ImageViewing from 'react-native-image-viewing';

<ImageViewing
  images={[{ uri: 'https://example.com/image1.jpg' }]}
  imageIndex={0}
  visible={isVisible}
  onRequestClose={() => setVisible(false)}
/>
```

------

⚡ 小Tips

- `imageUrls` 要求是一个数组格式，每个元素形如 `{ url: 'xxx' }`。
- `react-native-image-zoom-viewer` 支持手势缩放、滑动关闭、长按保存。
- `react-native-image-viewing` 适合简单预览，不支持复杂手势控制。
- 自定义需求（如底部小圆点、标题栏）可以用 `react-native-swiper` 等组件配合封装。

------

📢 总结

✅ 要功能全面 → **`react-native-image-zoom-viewer`**
 ✅ 要轻量简单 → **`react-native-image-viewing`**
 ✅ 要高性能 → **`fast-image`** 自己做大图浏览

------



### 4.11 🥳react-native-toast-message`

------

📦 安装

```bash
npm install react-native-toast-message
```

或者

```bash
yarn add react-native-toast-message
```

------

🔌 基础使用步骤

1. 在根组件注册 Toast 组件

在你的 `App.tsx` 或 `App.js` 里，挂上 `Toast`：

```tsx
import Toast from 'react-native-toast-message';

export default function App() {
  return (
    <>
      {/* 你的导航或页面组件 */}
      
      <Toast /> {/* 👈 Toast 组件放到最后 */}
    </>
  );
}
```

> 📢 注意：`<Toast />` 必须加到应用树里，否则不会显示！

------

2. 在代码中调用 `Toast.show`

示例：

```tsx
import Toast from 'react-native-toast-message';

Toast.show({
  type: 'success',    // 'success' | 'error' | 'info'
  text1: 'Hello 👋',
  text2: '这是一个提示信息',
});
```

------

🎨 内置的三种 Toast 类型

| 类型      | 效果               |
| --------- | ------------------ |
| `success` | 绿色背景，成功提示 |
| `error`   | 红色背景，错误提示 |
| `info`    | 蓝色背景，普通信息 |

------

🛠️ 更多配置选项

```tsx
Toast.show({
  type: 'success',
  text1: '标题', 
  text2: '子标题，可以写详细点',
  position: 'top', // 'top' | 'bottom'
  visibilityTime: 3000, // 显示多久（毫秒）
  autoHide: true, // 是否自动消失
  topOffset: 30, // 顶部偏移量
  bottomOffset: 40, // 底部偏移量
  onPress: () => {
    console.log('用户点了Toast！');
  }
});
```

------

📦 小封装一下（比如统一使用）

你可以自己封一个 `toast.ts` 工具文件：

```tsx
import Toast from 'react-native-toast-message';

export function showSuccessToast(message: string, subMessage?: string) {
  Toast.show({
    type: 'success',
    text1: message,
    text2: subMessage,
    position: 'top',
  });
}

export function showErrorToast(message: string, subMessage?: string) {
  Toast.show({
    type: 'error',
    text1: message,
    text2: subMessage,
    position: 'top',
  });
}
```

用的时候就很爽了：

```tsx
import { showSuccessToast, showErrorToast } from './toast';

showSuccessToast('提交成功', '恭喜你完成了提交！');
showErrorToast('提交失败', '请检查网络连接');
```

------

🚀 高阶玩法：自定义 Toast 样式

如果你觉得默认的太普通，可以完全自定义！

```tsx
<Toast config={{
  customToast: ({ text1, props }) => (
    <View style={{ height: 60, backgroundColor: 'pink', justifyContent: 'center', alignItems: 'center' }}>
      <Text>{text1}</Text>
    </View>
  )
}} />
```

然后调用：

```tsx
Toast.show({
  type: 'customToast', // 👈 注意是你注册的名字
  text1: '这是自定义Toast!',
});
```

你甚至可以自己画图标、加按钮、任意布局，想怎么玩都行 ✨

------

📢 小总结

| 特性                                      | 说明 |
| ----------------------------------------- | ---- |
| Android / iOS通用                         | ✅    |
| 支持类型：success / error / info / 自定义 | ✅    |
| 支持位置：top / bottom                    | ✅    |
| 支持自定义UI                              | ✅    |
| 支持点击事件、时长控制                    | ✅    |

------



### 4.12🗺️ React Native 地图开发笔记

📍 使用场景

- 实时定位展示
- 地图打点（Marker）
- 路线绘制（Polyline）
- 事件交互（点击、拖动）
- 路径导航或显示 POI 信息

------

#### 🌍 Google Maps

🔧 安装依赖

```bash
npm install react-native-maps
```

🧩 基础配置（iOS/Android）

- iOS：在 `AppDelegate.m` 中添加 Google API Key
- Android：在 `AndroidManifest.xml` 中添加权限与 API key

📦 常用功能

✅ 1. 定位当前位置

```tsx
import Geolocation from '@react-native-community/geolocation';

Geolocation.getCurrentPosition(
  (info) => console.log(info.coords),
  (err) => console.warn(err),
  { enableHighAccuracy: true }
);
```

📍 2. 添加标记点 Marker

```tsx
<Marker
  coordinate={{ latitude: 37.78825, longitude: -122.4324 }}
  title="位置"
  description="这是当前位置"
/>
```

✏️ 3. 绘制路径 Polyline

```tsx
<Polyline
  coordinates={[
    { latitude: 37.78, longitude: -122.43 },
    { latitude: 37.79, longitude: -122.44 },
  ]}
  strokeColor="#FF0000"
  strokeWidth={4}
/>
```

🧭 4. 地图事件监听

```tsx
<MapView onRegionChangeComplete={(region) => console.log(region)} />
```

------

#### 🌍🇨🇳 高德地图

🔧 安装依赖

```bash
npm install @amap/amap-react-native
```

⚙️ iOS 配置步骤

1. 使用 CocoaPods 安装原生依赖。
2. 在 `Info.plist` 添加：

```xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>App需要您的地理位置</string>
```

1. 配置后台定位、权限、API Key。

📦 常用功能

✅ 1. 获取当前定位

```tsx
import AMapLocation from '@amap/amap-react-native-location';

AMapLocation.startUpdatingLocation();
AMapLocation.addLocationListener((location) => {
  console.log(location);
});
```

📍 2. 添加 Marker

```tsx
<MapView.Marker
  coordinate={{ latitude: 39.9042, longitude: 116.4074 }}
  title="当前位置"
/>
```

✏️ 3. 绘制 Polyline 路线

```tsx
<MapView.Polyline
  coordinates={[
    { latitude: 39.90, longitude: 116.40 },
    { latitude: 39.91, longitude: 116.41 },
  ]}
  color="blue"
  width={4}
/>
```

🧭 4. 监听地图点击事件

```tsx
<MapView onPress={(e) => console.log(e.nativeEvent.coordinate)} />
```

------

📊 功能对比表

| 功能           | Google Maps ✅                 | 高德地图 ✅       |
| -------------- | ----------------------------- | ---------------- |
| 定位功能       | 支持 React Native Geolocation | 原生高德定位 SDK |
| Marker 打点    | ✅ 支持                        | ✅ 支持           |
| Polyline 路径  | ✅ 支持                        | ✅ 支持           |
| 地图事件监听   | ✅ 支持                        | ✅ 支持           |
| 地图样式自定义 | ✅ 丰富样式支持                | ❌ 限制较多       |
| 适用区域       | 全球通用                      | 国内推荐         |

------

🧪 实战建议

- 🌐 Google Maps 更适合国际化项目，有良好文档与灵活的样式支持。
- 🇨🇳 高德地图适合国内业务（如外卖、快递、打车）开发，定位更精准、服务本地化。

------





## 5、问题

### 5.1 依赖冲突

```bash
D:\reactNative\code\TssTemplate>npm ls react-native-svg 
TssTemplate@0.0.1 D:\reactNative\code\TssTemplate
├─┬ @pingtou/rn-vant@1.0.0
│ ├─┬ @pingtou/rn-vant-icons@1.0.0
│ │ └── react-native-svg@15.11.2 deduped
│ └── react-native-svg@12.5.1
├─┬ react-native-qrcode-svg@6.3.15
│ └── react-native-svg@15.11.2 deduped
└── react-native-svg@15.11.2
```



推荐使用方法：在package.json中加上

```js
  "resolutions": {
    "react-native-svg": "^15.11.2"
  }
```



但是还是一样的问题，建议用Yarn进行安装依赖。



### 5.2 高德地图返回问题

安卓端，在页面里使用react-native-amap3d地图，正常显示，但是在返回时会闪退，包括导航返回和按键返回。
**解决方案**
application 加上[android](https://so.csdn.net/so/search?q=android&spm=1001.2101.3001.7020):allowNativeHeapPointerTagging=“false”

<img src="C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20250507141554386.png" alt="image-20250507141554386" style="zoom:50%;" />





## 6、组件库

RN-VANT: https://rn-vant.vercel.app/

ANTD-RN: https://rn.mobile.ant.design/index-cn