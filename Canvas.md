# Canvas

## 1、🎨初识Canvas

在前端开发中，**Canvas** 是 HTML5 提供的一个用于绘图的元素，常用于渲染图形、动画、游戏、数据可视化等场景。它是一个 **位图绘图区域**，允许你使用 JavaScript 动态地绘制像素级的图形。

------

### 🎨 Canvas 的基本概念：

```html
<canvas id="myCanvas" width="300" height="150"></canvas>
```

- `canvas` 标签本身只是一个容器，没有内容。
- 绘图操作是通过 JavaScript 完成的。
- 需要使用 `getContext()` 获取绘图上下文。

------

### 📌 获取上下文并绘图示例：

```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d'); // 获取 2D 上下文

// 绘制一个红色矩形
ctx.fillStyle = 'red';
ctx.fillRect(50, 50, 100, 100);
```

------

### 🎯 Canvas 的两种上下文：

1. `2d`：二维绘图，用于画线条、矩形、圆、图片等。
2. `webgl` 或 `webgl2`：三维绘图，用于高性能图形渲染（比如游戏、3D 建模）。

------

### 🧠 Canvas 的特点：

- **像素级控制**，可以实现复杂图形。
- **不具备语义性**，不像 SVG 中的元素可以被单独选中或修改。
- **性能好**，适合绘制大量元素（如游戏、动画等）。
- 不支持事件绑定到绘制的图形上（需要手动处理点击等事件）。

------

### 🆚 Canvas 与 SVG 对比：

| 特性     | Canvas               | SVG                     |
| -------- | -------------------- | ----------------------- |
| 渲染方式 | 像素（位图）绘制     | 基于 DOM 的矢量图形     |
| 缩放效果 | 放大会失真           | 可无限缩放，清晰        |
| 性能     | 高，适合复杂大量元素 | 低，元素越多性能越差    |
| 交互支持 | 需手动实现           | 可通过 DOM 事件直接支持 |

------



## 2、🖌️ Canvas 的上下文对象（Context）详解

在 HTML5 Canvas 中，要想绘制内容，必须先通过 JavaScript 获取 Canvas 的“上下文对象”，即**绘图环境**，然后调用该对象的方法进行图形绘制。

------

### 📌 常见下文类型：

| 上下文类型       | 描述                                             | 获取方式                              |
| ---------------- | ------------------------------------------------ | ------------------------------------- |
| `2d`             | 二维上下文，支持基本图形绘制（如线、矩形、圆等） | `canvas.getContext('2d')`             |
| `webgl`          | 使用 WebGL 1.0 进行 3D 图形绘制                  | `canvas.getContext('webgl')`          |
| `webgl2`         | 使用 WebGL 2.0（更强大的 3D API）                | `canvas.getContext('webgl2')`         |
| `bitmaprenderer` | 允许直接渲染 `ImageBitmap` 到 Canvas             | `canvas.getContext('bitmaprenderer')` |
| `webgpu`         | WebGPU 新标准，浏览器支持仍在发展中（实验性质）  | `canvas.getContext('webgpu')`         |

------

### ✅ 下文用途示例：

#### 📌 `2d` 上下文示例：

```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');
ctx.fillStyle = 'green';
ctx.fillRect(10, 10, 100, 100);
```

#### 📌 `webgl` 上下文示例（基本初始化）：

```javascript
const canvas = document.getElementById('myCanvas');
const gl = canvas.getContext('webgl');
if (!gl) {
  console.error('WebGL not supported');
}
```

------

### 🌐 浏览器支持

| 浏览器          | `2d` 支持 | `webgl` 支持  | `webgl2` 支持 | `bitmaprenderer` 支持 | `webgpu` 支持（实验） |
| --------------- | --------- | ------------- | ------------- | --------------------- | --------------------- |
| Chrome          | ✅         | ✅             | ✅             | ✅                     | ✅（需手动开启）       |
| Firefox         | ✅         | ✅             | ✅             | ✅                     | ✅（开发版支持）       |
| Safari          | ✅         | ✅             | ✅             | ✅                     | 🚫（部分实验支持）     |
| Edge (Chromium) | ✅         | ✅             | ✅             | ✅                     | ✅                     |
| Opera           | ✅         | ✅             | ✅             | ✅                     | ✅（需设置）           |
| 移动端浏览器    | ✅         | ✅（多数支持） | ✅（较新设备） | ✅                     | 🚫                     |

------

### 🔍 小贴士：

- 大部分常见应用只用 `2d` 或 `webgl` 即可满足需求。
- `webgpu` 是 Web 图形的新一代标准，比 WebGL 更高性能，但仍不稳定，未来值得关注。
- 使用 `getContext` 时建议检查返回值是否为 `null`，以防浏览器不支持该上下文。

------

## 3、🎨 Canvas 的填充与路径绘制

在 `Canvas` 中，图形的绘制通常通过“路径”来完成。你可以使用 `beginPath()` 开始绘制路径，然后使用各种绘制方法（如 `moveTo()`、`lineTo()`）定义路径，最后使用 `fill()` 或 `stroke()` 渲染路径。

------

### 🧱 1. 基本路径流程

```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

ctx.beginPath();            // 开始一条新路径
ctx.moveTo(50, 50);         // 移动到起始点
ctx.lineTo(150, 50);        // 画一条线到新点
ctx.lineTo(100, 100);       // 再画一条线
ctx.closePath();            // 可选，闭合路径（首尾连接）

ctx.fillStyle = 'lightblue'; 
ctx.fill();                 // 填充路径
ctx.strokeStyle = 'blue';   
ctx.stroke();               // 描边路径
```

------

### 🖌️ 2. 填充与描边属性

| 属性          | 描述                              |
| ------------- | --------------------------------- |
| `fillStyle`   | 设置填充颜色、渐变、图案          |
| `strokeStyle` | 设置线条颜色                      |
| `lineWidth`   | 设置描边宽度                      |
| `lineJoin`    | 设置线连接方式（miter、round等）  |
| `lineCap`     | 设置线条末端样式（butt、round等） |

```javascript
ctx.fillStyle = 'red';
ctx.strokeStyle = 'black';
ctx.lineWidth = 2;
```

------

### 🌀 3. 绘制基本图形路径示例

#### ✅ 圆形（使用 `arc()`）：

```javascript
ctx.beginPath();
ctx.arc(100, 75, 50, 0, Math.PI * 2); // 圆心(100,75)，半径50
ctx.fill();  // 填充圆
```

------

#### ✅ 矩形（也可用路径方式）：

```javascript
ctx.beginPath();
ctx.rect(20, 20, 100, 50);  // 从(20,20)开始，宽100高50
ctx.fill();
```

> 当然，Canvas 提供了更简单的矩形方法（不需路径）：

```javascript
ctx.fillRect(20, 20, 100, 50);     // 立即绘制填充矩形
ctx.strokeRect(20, 20, 100, 50);   // 立即绘制描边矩形
ctx.clearRect(30, 30, 40, 20);     // 清除区域
```

------

### 🧩 4. 填充规则（非零 vs 奇偶）

对于自定义形状中是否需要“洞”，可以设置填充规则：

```javascript
ctx.fill('evenodd');   // 奇偶规则，适用于环形、镂空等
ctx.fill('nonzero');   // 默认规则
```

------

你提到“清楚”，如果是想问：

------

#### 5、❓如何清除 Canvas 的内容？

可以使用 Canvas 提供的 `clearRect()` 方法来清除画布中的内容。

✅ 基本语法：

```javascript
ctx.clearRect(x, y, width, height);
```

✅ 清除整个画布：

```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

// 清除整个画布
ctx.clearRect(0, 0, canvas.width, canvas.height);
```

------

💡 补充技巧：

1. 每帧清除：用于动画刷新

```javascript
function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  // 再绘制下一帧图像
  requestAnimationFrame(draw);
}
draw();
```

2. 使用 `canvas.width` 重新赋值也能清空内容：

```javascript
canvas.width = canvas.width; // 会清空内容，并重置状态（慎用）
```

但这种方式也会 **清除样式设置（如 fillStyle）**，不建议频繁使用。

------

如果你说的“清楚”是其他意思，也欢迎补充具体问题，我马上为你解释。

### 💡 实战小例子：绘制一个五角星

```javascript
function drawStar(ctx, cx, cy, spikes, outerRadius, innerRadius) {
  const step = Math.PI / spikes;

  ctx.beginPath();
  for (let i = 0; i < 2 * spikes; i++) {
    const radius = i % 2 === 0 ? outerRadius : innerRadius;
    const angle = i * step - Math.PI / 2;
    const x = cx + Math.cos(angle) * radius;
    const y = cy + Math.sin(angle) * radius;
    if (i === 0) ctx.moveTo(x, y);
    else ctx.lineTo(x, y);
  }
  ctx.closePath();
  ctx.fillStyle = 'gold';
  ctx.fill();
  ctx.strokeStyle = 'black';
  ctx.stroke();
}

drawStar(ctx, 100, 100, 5, 50, 20);
```

------

