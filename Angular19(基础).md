# Angular19(基础)

------

## 1.📦 环境搭建与项目创建

------

✅ 一、前置环境

| 工具        | 版本要求              | 说明                        |
| ----------- | --------------------- | --------------------------- |
| Node.js     | 推荐 18.x 或 20.x     | Angular 19 最佳兼容版本     |
| npm / pnpm  | 推荐 npm 9+ / pnpm 8+ | pnpm 更快、磁盘占用小       |
| Angular CLI | 16.2+（或最新）       | 创建 Angular 项目的官方工具 |
| TypeScript  | 5.3+                  | Angular 19 内部依赖版本     |

📥 安装 Node.js

官网下载并安装：https://nodejs.org/

```bash
node -v
npm -v
```

------

✅ 二、安装 Angular CLI

```bash
npm install -g @angular/cli
```

或者使用 pnpm：

```bash
pnpm add -g @angular/cli
```

验证安装成功：

```bash
ng version
```

------

✅ 三、创建新项目（推荐使用 Standalone 模式）

Angular 19 官方推荐使用 **Standalone Component** 模式，模块更轻量、可维护性更高。

```bash
ng new my-app --standalone
```

CLI 交互提示：

- **Would you like to add Angular routing?** → Yes（添加路由）
- **Which stylesheet format?** → SCSS（推荐）/ CSS
- **Enable strict mode?** → Yes（开启严格模式）

进入项目目录并启动服务：

```bash
cd my-app
ng serve
```

访问：[http://localhost:4200](http://localhost:4200/)

------

✅ 四、项目结构说明（Standalone 模式）

```
my-app/
├── src/
│   ├── app/
│   │   └── app.config.ts      ← 应用路由和提供者配置
│   │   └── app.component.ts   ← 主组件，standalone
│   └── main.ts                ← 启动入口 bootstrapApplication()
├── angular.json              ← 项目配置文件
├── package.json              ← 依赖列表
```

🔹 启动入口（main.ts）

```ts
bootstrapApplication(AppComponent, appConfig)
  .catch(err => console.error(err));
```

🔹 路由配置（app.config.ts）

```ts
export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter([
      { path: '', component: HomeComponent },
      ...
    ])
  ]
};
```

------

✅ 五、使用 pnpm（推荐更高效的包管理器）

安装 pnpm：

```bash
npm install -g pnpm
```

创建项目（仍可使用 Angular CLI）：

```bash
ng new my-app --standalone --package-manager=pnpm
```

------

✅ 六、常用开发命令

| 命令                         | 说明                        |
| ---------------------------- | --------------------------- |
| `ng serve`                   | 启动开发服务器              |
| `ng build`                   | 构建生产包                  |
| `ng generate component name` | 生成组件（支持 standalone） |
| `ng test`                    | 运行单元测试                |
| `ng lint`                    | 检查代码风格问题            |

------

✅ 七、配置技巧与建议

🔧 设置文件别名路径（`tsconfig.json`）

```json
"paths": {
  "@app/*": ["src/app/*"]
}
```

配合使用：

```ts
import { HomeComponent } from '@app/pages/home/home.component';
```

------

🌍 设置 API 地址环境变量

编辑 `src/environments/environment.ts`：

```ts
export const environment = {
  apiUrl: 'http://localhost:3000/api'
};
```

构建时自动替换为 `environment.prod.ts` 内容。

------

✅ 八、常见问题解决

| 问题                | 解决方法                             |
| ------------------- | ------------------------------------ |
| `ng serve` 无法访问 | 检查是否被防火墙/杀毒软件拦截        |
| `ng new` 太慢       | 使用 `pnpm` + 科学上网               |
| 没有创建 module.ts  | Angular 19 Standalone 模式默认无模块 |
| 浏览器显示空白页    | 检查组件是否正确挂载路由             |

------



## 2.🧱  Component

------

✅ 一、什么是 Component？

在 Angular 中，**组件（Component）** 是 UI 的构建块。它控制模板（HTML）、样式（CSS/SCSS），并定义逻辑（TypeScript）。

每个组件都有：

- 一个装饰器 `@Component`
- 一个类 `ComponentClass`
- 可选的模板和样式文件

------

✅ 二、@Component 装饰器详解

```ts
@Component({
  selector: 'app-hello',             // 用于 HTML 中的标签名
  standalone: true,                  // Angular 14+ 独立组件标记
  templateUrl: './hello.component.html', // 模板路径
  styleUrls: ['./hello.component.scss'], // 样式路径
  imports: [CommonModule],          // 依赖的其他组件/指令/管道
})
export class HelloComponent {
  name = 'Angular';
}
```

📌 常用属性说明

| 属性名        | 类型     | 说明                                                      |
| ------------- | -------- | --------------------------------------------------------- |
| `selector`    | string   | 组件在 HTML 中的标签名，如 `<app-hello>`                  |
| `template`    | string   | 内联模板 HTML                                             |
| `templateUrl` | string   | 模板文件路径                                              |
| `styleUrls`   | string[] | 样式文件路径                                              |
| `imports`     | any[]    | Angular 14+ 中用于导入指令、组件、管道等（替代 NgModule） |
| `standalone`  | boolean  | 是否为独立组件（Angular 14+）                             |

------

✅ 三、定义一个最基本的 Standalone Component

```ts
// hello.component.ts
@Component({
  selector: 'app-hello',
  standalone: true,
  template: `<h1>Hello {{ name }}!</h1>`,
})
export class HelloComponent {
  name = 'Angular 19';
}
```

------

✅ 四、如何渲染一个组件？

✅ 1. 在父组件模板中通过 `<selector>` 引用

```html
<!-- app.component.html -->
<app-hello></app-hello>
```

确保在 `app.component.ts` 的 `imports` 中导入了 `HelloComponent`：

```ts
@Component({
  standalone: true,
  selector: 'app-root',
  imports: [HelloComponent], // 必须导入要用到的 standalone component
  templateUrl: './app.component.html',
})
export class AppComponent {}
```

------

✅ 2. 通过路由渲染组件

```ts
export const appRoutes: Routes = [
  {
    path: 'hello',
    loadComponent: () => import('./hello.component').then(m => m.HelloComponent),
  }
];
```

在模板中使用 `<router-outlet></router-outlet>` ：

```html
<!-- app.component.html -->
<router-outlet></router-outlet>
```

点击跳转：

```html
<a routerLink="/hello">Hello 页面</a>
```

------

✅ 3. 动态创建组件（高级）

```ts
constructor(private viewContainerRef: ViewContainerRef) {}

ngAfterViewInit() {
  this.viewContainerRef.createComponent(HelloComponent);
}
```

- 更适合用于动态插入的组件（弹窗、模态框等）

------

✅ 五、组件之间的组合与嵌套

```html
<!-- parent.component.html -->
<h2>父组件</h2>
<app-child></app-child>
```

确保在 `ParentComponent` 的 `imports` 中引入了 `ChildComponent`。

> 在 Standalone 模式下，所有要使用的组件都必须显式导入进 `imports: []` 中。

------

✅ 六、模板绑定简要预览（为后续章节铺垫）

```html
<h1>{{ title }}</h1>                 <!-- 插值 -->
<button (click)="handleClick()">点击</button> <!-- 事件绑定 -->
<input [(ngModel)]="username" />    <!-- 双向绑定 -->
```

------

✅ 七、最佳实践总结

| 建议                                         | 理由                              |
| -------------------------------------------- | --------------------------------- |
| 使用 `standalone: true` 创建组件             | 更轻量，易于组合，推荐方式        |
| 模板使用 `templateUrl`，样式使用 `styleUrls` | 有利于分离逻辑和视图              |
| 使用 `imports: []` 显式导入                  | 避免运行时找不到指令              |
| 不要忘记在使用组件的地方导入它               | Standalone 模式中每个组件互相独立 |

------

✅ 八、常见错误与排查

| 错误信息                           | 原因与解决方法                          |
| ---------------------------------- | --------------------------------------- |
| `app-hello is not a known element` | 没有在当前组件的 `imports` 中引入该组件 |
| `Can't bind to 'xxx'`              | 属性未定义，或需要的指令模块未引入      |
| `template parse errors`            | HTML 模板语法有误，或组件未正确识别     |

------



下面是 **Angular 19 中的数据绑定（Data Binding）** 的完整笔记，内容涵盖四种绑定方式（插值、属性绑定、事件绑定、双向绑定），并包含语法、示例、适用场景和注意事项。







## 3.🔗 数据绑定（Data Binding）

------

### ✅ 一、数据绑定的四种类型

| 类型       | 方向                | 语法                  | 说明                       |
| ---------- | ------------------- | --------------------- | -------------------------- |
| 1️⃣ 插值绑定 | 单向（组件 → 视图） | `{{ value }}`         | 用于显示字符串、表达式值   |
| 2️⃣ 属性绑定 | 单向（组件 → 属性） | `[attr]="value"`      | 绑定 HTML 属性、DOM 属性等 |
| 3️⃣ 事件绑定 | 单向（视图 → 组件） | `(event)="handler()"` | 监听用户事件，如点击、输入 |
| 4️⃣ 双向绑定 | 双向（视图 ↔ 组件） | `[(ngModel)]="value"` | 常用于 `<input>` 表单控件  |

------

### 📌 二、插值绑定（Interpolation）

✅ 语法：

```html
<h1>Hello {{ username }}</h1>
```

✅ 使用说明：

- 只能用在 HTML 内容（文本节点）
- 不可直接操作属性，如 `href`、`src` 等
- 支持表达式：

```html
{{ user.age + 1 }}
{{ isActive ? '开启' : '关闭' }}
```

------

### 📌 三、属性绑定（Property Binding）

✅ 语法：

```html
<img [src]="imageUrl" />
<button [disabled]="isDisabled">提交</button>
```

✅ 使用说明：

- 用方括号 `[]` 来绑定属性（组件值 → DOM 属性）
- 绑定目标必须是元素的**原生属性或 DOM 属性**

❌ 错误写法（这是字符串）：

```html
<img src="{{ imageUrl }}">   <!-- 有效，但不推荐 -->
<img src="imageUrl">         <!-- 错误：未绑定变量 -->
```

------

### 📌 四、事件绑定（Event Binding）

✅ 语法：

```html
<button (click)="onClick()">点击我</button>
<input (input)="onInputChange($event)" />
```

✅ 使用说明：

- 使用小括号 `()` 绑定 DOM 事件
- `$event` 表示原生事件对象

```ts
onInputChange(event: Event) {
  const value = (event.target as HTMLInputElement).value;
  console.log(value);
}
```

------

### 📌 五、双向绑定（Two-way Binding）

✅ 语法（需要引入 `FormsModule`）：

```html
<input [(ngModel)]="username" />
<p>Hello {{ username }}</p>
```

✅ 使用说明：

- 必须导入 `FormsModule` 或 `ReactiveFormsModule`
- 语法糖：其实是属性绑定 `[value]` + 事件绑定 `(input)`

```ts
@NgModule({
  imports: [FormsModule] // 如果是非 standalone 项目
})
```

或在 standalone 组件中：

```ts
@Component({
  standalone: true,
  imports: [FormsModule],
  ...
})
```

------

### 📌 六、属性 vs HTML 属性差异

```html
<input [value]="username" />     <!-- 属性绑定，动态更新 -->
<input value="{{ username }}" /> <!-- 插值绑定，一次性渲染 -->
```

| 类型     | 更新机制 | 是否响应变化   |
| -------- | -------- | -------------- |
| 插值     | 一次渲染 | 否（初始值）   |
| 属性绑定 | 动态绑定 | 是（实时响应） |

------

### 📌 七、样式和类绑定

✅ [style]、[class] 简单绑定

```html
<p [style.color]="'red'">红色文字</p>
<p [class.active]="isActive">动态类名</p>
```

✅ 使用 ngClass 和 ngStyle（复杂场景）

```html
<p [ngClass]="{ active: isActive, disabled: !canClick }"></p>
<p [ngStyle]="{ fontSize: size + 'px' }"></p>
```

------

### ✅ 八、总结对比

| 绑定方式      | 方向 | 用途             |
| ------------- | ---- | ---------------- |
| `{{ }}`       | 单向 | 插入文本、表达式 |
| `[property]`  | 单向 | 设置属性值       |
| `(event)`     | 单向 | 响应事件         |
| `[(ngModel)]` | 双向 | 表单输入交互     |

------

### ✅ 九、常见错误 & 排查建议

| 报错                      | 原因                                       |
| ------------------------- | ------------------------------------------ |
| `Can't bind to 'ngModel'` | 未导入 `FormsModule`                       |
| 插值表达式无效            | 使用了不支持的 JS 表达式，如函数调用副作用 |
| 属性绑定无效              | 目标不是标准属性或组件未声明对应输入属性   |
| `(click)="handler"`       | 少了 `()`，应该是 `(click)="handler()"`    |

------





非常好，我们现在来讲解 Angular 19 中 **结构型指令（Structural Directive）** 的使用方法。这是 Angular 中非常强大的一类指令，它允许你 **添加、移除或操作 DOM 元素的结构**。

------

## 4.🧱 Structural Directive

------

### ✅ 一、什么是结构型指令？

结构型指令用于控制 DOM 的“结构”，**它会增删 HTML 元素或模板片段**。

✅ 特点：

- 使用语法：`*directive`
- 常见的结构型指令：
  - `*ngIf`：条件渲染
  - `*ngFor`：循环渲染
  - `*ngSwitch`：条件切换
  - 自定义结构型指令（如 `*appUnless`）

------

### ✅ 二、内置结构型指令用法

------

#### 1️⃣ `*ngIf`：条件渲染

```html
<p *ngIf="isLoggedIn">欢迎回来！</p>
<p *ngIf="!isLoggedIn">请先登录。</p>
```

支持 `else` 分支：

```html
<ng-template #noLogin>请先登录</ng-template>
<p *ngIf="isLoggedIn; else noLogin">欢迎回来！</p>
```

------

#### 2️⃣ `*ngFor`：循4环渲染

```html
<ul>
  <li *ngFor="let item of items; index as i">
    第{{ i }}项：{{ item }}
  </li>
</ul>
```

常用的局部变量：

| 变量名         | 含义                  |
| -------------- | --------------------- |
| `index`        | 当前项索引            |
| `first`        | 是否为第一项          |
| `last`         | 是否为最后一项        |
| `even` / `odd` | 是否为偶数/奇数索引项 |

------

#### 3️⃣ `*ngSwitch`：条件分支匹配

```html
<div [ngSwitch]="status">
  <p *ngSwitchCase="'success'">成功</p>
  <p *ngSwitchCase="'error'">失败</p>
  <p *ngSwitchDefault>未知状态</p>
</div>
```

------

### ✅ 三、自定义结构型指令

------

🛠️ 示例：创建一个 `*appUnless`（和 *ngIf 相反）

Step 1: 创建指令

```bash
ng g directive unless --standalone
```

Step 2: 编写逻辑

```ts
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[appUnless]',
  standalone: true
})
export class UnlessDirective {
  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) {}

  @Input() set appUnless(condition: boolean) {
    if (!condition) {
      this.viewContainer.createEmbeddedView(this.templateRef);
    } else {
      this.viewContainer.clear();
    }
  }
}
```

------

Step 3: 使用方式

确保引入该指令：

```ts
@Component({
  standalone: true,
  selector: 'app-root',
  template: `<p *appUnless="isLoggedIn">请登录后查看内容</p>`,
  imports: [UnlessDirective]
})
export class AppComponent {
  isLoggedIn = false;
}
```

------

### ✅ 四、底层原理简析

```html
<p *ngIf="isShown">Hello</p>
```

实际上等价于：

```html
<ng-template [ngIf]="isShown">
  <p>Hello</p>
</ng-template>
```

结构型指令本质上是操作 `<ng-template>` 的视图渲染机制。

------

### ✅ 五、常见错误与排查

| 错误信息                                     | 原因                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| `Template parse errors: Can't bind to 'xxx'` | 指令没有正确声明或导入                                       |
| 指令不生效                                   | 忘记在使用者组件中 `imports: [YourDirective]`                |
| 结构指令放错位置                             | 必须用于 HTML 元素上，不能放在 `<ng-container>` 中嵌套多层结构错误 |

------

### ✅ 六、进阶技巧

✅ 使用 `ng-template` 明确控制模板：

```html
<ng-template [ngIf]="showContent">
  <p>这是可控的内容</p>
</ng-template>
```

可搭配 `<ng-container>` 无包裹结构使用：

```html
<ng-container *ngIf="isLoading">
  <p>加载中...</p>
</ng-container>
```

------

### ✅ 七、总结对比

| 指令         | 用途           |
| ------------ | -------------- |
| `*ngIf`      | 条件渲染       |
| `*ngFor`     | 列表渲染       |
| `*ngSwitch`  | 多条件分支     |
| `*appUnless` | 自定义反向渲染 |

------



## 5.📘Signal 

------

### ✅ 1. 什么是 Angular 中的 Signal？

在 **Angular 16+（包括 Angular 19）** 中，引入了一个新的响应式原语 —— **Signal（信号）**，用于管理本地状态。
 它是一种 **同步、细粒度且自动通知依赖方的响应式数据机制**，可以作为 `Observable` 的替代，用于组件内部的状态管理。

它的特点包括：

- 包裹一个值，并在该值变化时通知使用它的地方；
- 可以在组件模板中直接使用；
- 不需要手动订阅或取消订阅。

> 适用于本地 UI 状态、组件内状态，是 Angular 响应式系统的重要补充。

------

### ✅ 2. 如何创建一个 Signal？

通过 `signal()` 函数来创建：

```ts
import { signal } from '@angular/core';

const counter = signal(0);
```

在组件中使用示例：

```ts
import { Component, signal } from '@angular/core';

@Component({
  selector: 'app-counter',
  template: `
    <p>Count: {{ counter() }}</p>
    <button (click)="increment()">增加</button>
  `,
})
export class CounterComponent {
  counter = signal(0);

  increment() {
    this.counter.set(this.counter() + 1);
  }
}
```

------

### ✅ 3. 如何读取 Signal 的值？

使用 `signal()` 这个函数来读取当前值：

```ts
const current = counter();  // 读取当前值
```

> 注意：Signal 不是普通变量，而是一个 **函数**，调用它才返回值。

------

### ✅ 4. 如何更新 Signal？

更新 Signal 有三种方式：

#### a) `set()`：直接设置新值

```ts
this.counter.set(10);
```

#### b) `update()`：基于当前值更新

```ts
this.counter.update(value => value + 1);
```

#### c) `mutate()`：就地修改对象/数组（仅适用于复杂类型）

```ts
this.user = signal({ name: 'Ryan', age: 25 });

this.user.mutate(u => {
  u.age += 1;
});
```

------

### ✅ 5. 使用对象类型的 Signal 示例

```ts
user = signal({ name: 'Alice', age: 30 });

get userName() {
  return this.user().name;
}

updateName(newName: string) {
  this.user.update(user => ({ ...user, name: newName }));
}
```

------

### ✅ 6. 在模板中使用 Signal

你可以直接在模板中使用信号：

```html
<p>姓名：{{ user().name }}</p>
<button (click)="updateName('Bob')">修改姓名</button>
```

------

### ✅ 7. 总结

| 操作方式 | 示例                                        | 说明         |
| -------- | ------------------------------------------- | ------------ |
| 创建     | `const count = signal(0)`                   | 创建信号变量 |
| 读取     | `count()`                                   | 获取当前值   |
| 设置     | `count.set(5)`                              | 设置为新值   |
| 更新     | `count.update(v => v + 1)`                  | 基于旧值更新 |
| 变异     | `signalObject.mutate(obj => { obj.x = 1 })` | 修改对象内容 |

------







## Extension

### 📘 模板控制流语法

> 📌 适用版本：Angular 17+
>  ⚙️ 启用方法：`tsconfig.json` 中添加

```json
"angularCompilerOptions": {
  "controlFlow": true
}
```

------

#### ✅ 1. `@if` 条件渲染

基本语法

```html
@if (condition) {
  <p>条件为真</p>
} @else {
  <p>条件为假</p>
}
```

嵌套写法

```html
@if (user) {
  <p>用户名：{{ user.name }}</p>
  @if (user.isAdmin) {
    <p>管理员身份</p>
  }
}
```

------

#### ✅ 2. `@for` 循环渲染（替代 `*ngFor`）

基本语法

```html
@for (item of items) {
  <p>{{ item }}</p>
}
```

搭配 `track` 用法（性能优化）

```html
@for (item of items; track item.id) {
  <p>{{ item.name }}</p>
}
```

支持索引/布尔标识

```html
@for (item of items; let i = $index; let isFirst = $first) {
  <p>{{ i }} - {{ isFirst ? '第一项' : item }}</p>
}
```

| 特殊变量         | 含义              |
| ---------------- | ----------------- |
| `$index`         | 当前索引          |
| `$first`         | 是否为第一项      |
| `$last`          | 是否为最后一项    |
| `$even` / `$odd` | 是否为偶数/奇数项 |

------

#### ✅ 3. `@switch` 多条件分支（替代 `ngSwitch`）

```html
@switch (status) {
  @case ('loading') {
    <p>加载中...</p>
  }
  @case ('success') {
    <p>加载成功</p>
  }
  @default {
    <p>未知状态</p>
  }
}
```

------

#### ✅ 4. 控制流嵌套示例

```html
@for (user of users) {
  @if (user.active) {
    <p>{{ user.name }} 是活跃用户</p>
  } @else {
    <p>{{ user.name }} 非活跃</p>
  }
}
```

------

#### ✅ 5. 可组合性与灵活性

控制流语法支持多个嵌套与组合，非常适合：

- 表格或列表的嵌套渲染
- 条件布局切换
- 动态状态 UI 渲染

------

#### ✅ 6. 与传统语法对比

| 功能     | `*ngIf` / `*ngFor` | `@if` / `@for`         |
| -------- | ------------------ | ---------------------- |
| 书写风格 | 模板指令           | 类似 TypeScript        |
| 可读性   | 略差               | ✅ 更清晰               |
| 嵌套支持 | 复杂且冗长         | ✅ 自然                 |
| 控制能力 | 一般               | ✅ 强大                 |
| 默认启用 | 是                 | ❌ 需开启 `controlFlow` |

------

#### ✅ 7. 常见错误排查

| 错误信息                         | 可能原因             |
| -------------------------------- | -------------------- |
| `Parser Error: Unexpected token` | 未开启 `controlFlow` |
| 控制流语法无效                   | Angular 版本 < 17    |
| 使用 `@if`、`@for` 混合 `*ngIf`  | 不兼容，不能混用     |
| `track` 写法无效                 | 变量未定义或语法错误 |

------

#### ✅ 8. 适配建议

- 若是新项目，建议直接启用控制流语法，书写清晰简洁。
- 老项目迁移时，可以逐步替换复杂结构中的 `*ngIf`、`*ngFor`。
- 可与 `standalone components`、`Signal` 等新语法一起使用。





### 🧠 组件的 `changeDetection` 与 `encapsulation`

------

#### 🔁 一、`changeDetection` - 变更检测策略

------

✅ 什么是变更检测？

Angular 会自动检测组件中的数据变化，并更新视图。这个过程叫做 **变更检测（Change Detection）**。

Angular 默认的策略是：**整个组件树从上到下检查一遍所有组件和绑定** —— 可能带来性能问题。

------

✅ 策略类型

1️⃣ `ChangeDetectionStrategy.Default`

- 默认策略
- 每次组件或子组件的数据变化，都会触发从根组件开始整个组件树的检查。

```ts
import { ChangeDetectionStrategy } from '@angular/core';

@Component({
  selector: 'app-default',
  templateUrl: './default.component.html',
  changeDetection: ChangeDetectionStrategy.Default
})
export class DefaultComponent {}
```

2️⃣ `ChangeDetectionStrategy.OnPush`（推荐）

- 只在以下情况触发变更检测：
  - `@Input()` 的引用值发生改变
  - 主动调用 `ChangeDetectorRef.markForCheck()`
  - 异步事件（如 Observable、事件绑定等）

```ts
import { ChangeDetectionStrategy } from '@angular/core';

@Component({
  selector: 'app-onpush',
  templateUrl: './onpush.component.html',
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class OnPushComponent {}
```

------

✅ 对比总结

| 特性           | Default          | OnPush                   |
| -------------- | ---------------- | ------------------------ |
| 性能           | 较低（全树检查） | ✅ 更高（引用变化才检查） |
| 使用场景       | 快速开发         | ✅ 高性能场景、纯展示组件 |
| 可检测对象变化 | ✅ 是             | 否（需要引用变更）       |

------

✅ OnPush 使用注意事项

```ts
@Input() user: { name: string }  // ⚠️ 对象引用不变，视图不会更新

ngOnChanges() {
  // 修改属性不会触发视图更新（除非引用改变）
  this.user.name = '新名字'; // ❌ 无效
  this.user = { ...this.user, name: '新名字' }; // ✅ 有效
}
```

------

#### 🎨 二、`encapsulation` - 样式封装策略

------

✅ 什么是样式封装？

Angular 为组件的样式添加自动隔离，防止样式污染到全局或其他组件。

------

✅ 类型对比

1️⃣ `ViewEncapsulation.Emulated`（默认）

- 使用属性选择器隔离样式（如 `_ngcontent`）
- **推荐使用**，保证样式局部作用

```ts
@Component({
  encapsulation: ViewEncapsulation.Emulated
})
```

2️⃣ `ViewEncapsulation.None`

- 样式无隔离，**全局作用**
- 相当于在 `styles.css` 写全局样式

```ts
@Component({
  encapsulation: ViewEncapsulation.None
})
```

3️⃣ `ViewEncapsulation.ShadowDom`

- 原生 Web 标准的 Shadow DOM 隔离方式
- 样式彻底隔离（不能被外部样式覆盖）

```ts
@Component({
  encapsulation: ViewEncapsulation.ShadowDom
})
```

------

✅ 封装策略对比表

| 封装策略  | 样式作用范围 | 支持旧浏览器     | 推荐场景           |
| --------- | ------------ | ---------------- | ------------------ |
| Emulated  | ✅ 组件内部   | ✅ 是             | ✅ 推荐             |
| None      | ❌ 全局污染   | ✅ 是             | 需要全局覆盖       |
| ShadowDom | ✅ 完全隔离   | ❌ 不支持旧浏览器 | 高级定制组件库开发 |

------

✅ 使用示例完整代码

```ts
import { Component, ChangeDetectionStrategy, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-demo',
  templateUrl: './demo.component.html',
  styleUrls: ['./demo.component.css'],
  changeDetection: ChangeDetectionStrategy.OnPush,
  encapsulation: ViewEncapsulation.Emulated
})
export class DemoComponent {
  @Input() user = { name: '张三' };
}
```

------

✅ 最佳实践建议

- ✅ 使用 `OnPush` 提升性能，尤其是纯展示组件
- ✅ 默认使用 `Emulated` 样式封装防止污染
- ⛔ 避免大量使用 `None`（除非你明确知道为什么）
- ✅ 更改 `@Input` 属性时，推荐使用不可变数据结构（例如新对象）

------



### 🎨动态CSS/Class

------

#### ✅ 一、动态 CSS（Dynamic Style）

1. `[style]` 单属性绑定

```html
<div [style.color]="'red'">Red Text</div>
<div [style.font-size.px]="fontSize">Dynamic Font Size</div>
fontSize = 20;
```

2. `[ngStyle]` 多属性绑定

```html
<div [ngStyle]="{ 'color': color, 'font-size.px': fontSize }">
  Styled Text
</div>
color = 'blue';
fontSize = 18;
```

------

#### ✅ 二、动态类（Dynamic Class）

1. `[class.class-name]` 单类名绑定

```html
<div [class.active]="isActive">Single Class</div>
isActive = true;
```

2. `[ngClass]` 多类名绑定

写法1：使用对象形式（推荐）

```html
<div [ngClass]="{ 'active': isActive, 'highlight': isHighlighted }">
  Multiple Classes
</div>
isActive = true;
isHighlighted = false;
```

写法2：使用数组形式

```html
<div [ngClass]="[class1, class2]">Dynamic Classes</div>
class1 = 'active';
class2 = 'text-large';
```

写法3：直接传入字符串

```html
<div [ngClass]="dynamicClass">Dynamic Class</div>
dynamicClass = 'btn-primary';
```

------

#### ✅ 三、实战建议

- 动态样式适合用于样式值频繁变化的场景（比如颜色、宽度等）。
- 动态类适合用于控制状态相关的样式（比如是否选中、是否禁用等）。

------

#### ✅ 四、结合条件判断的例子

```html
<button
  [ngClass]="{
    'btn': true,
    'btn-primary': type === 'primary',
    'btn-danger': type === 'danger'
  }"
  [style.background-color]="bgColor"
>
  Button
</button>
type = 'primary';
bgColor = '#ccc';
```

------



非常好，下面是一个**最详细、分层次讲解 Angular 模块设计的版本**，将包括：

- `NgModule` 背后设计思想；
- Angular 模块的分层架构；
- 项目结构与模块拆分建议；
- Standalone 架构与融合策略；
- 实战示例与注意事项。

------

### 📦 Angular 模块设计

------

#### 🧠 一、设计思想：为什么 Angular 有模块系统？

##### 核心目标：

1. **功能隔离**（高内聚低耦合）；
2. **作用域控制**（组件/服务/指令只在需要范围内生效）；
3. **依赖管理**（组件使用谁、谁能使用我）；
4. **懒加载支持**（优化初次加载性能）；
5. **可维护性与可测试性提升**。

------

#### 🏗️ 二、传统 NgModule 架构设计

##### 💡 NgModule 是 Angular 的逻辑边界单位。

```ts
@NgModule({
  declarations: [...],  // 本模块定义的视图类（组件/指令/管道）
  imports: [...],       // 本模块依赖的其他模块
  exports: [...],       // 要让外部使用的视图类
  providers: [...]      // 服务注入（可限定作用域）
})
export class FeatureModule {}
```

------

##### 🧱 NgModule 分层分类

| 层级   | 模块名称        | 作用                                 |
| ------ | --------------- | ------------------------------------ |
| 根层   | `AppModule`     | 应用的唯一入口                       |
| 核心层 | `CoreModule`    | 全局服务、单例提供者、拦截器等       |
| 共享层 | `SharedModule`  | 通用组件/指令/管道（无服务）         |
| 功能层 | `FeatureModule` | 独立业务功能，如用户、订单、产品模块 |
| 页面层 | `PageModule`    | 通常配合路由，每个页面独立为模块     |
| 组件层 | `WidgetModule`  | 复杂通用组件（表格、上传等）         |

------

##### 📁 目录结构推荐（NgModule）

```
src/
├── app/
│   ├── app.module.ts
│   ├── core/                # CoreModule
│   ├── shared/              # SharedModule
│   ├── features/
│   │   └── user/
│   │       ├── user.module.ts
│   │       ├── components/
│   │       ├── pages/
│   │       └── services/
│   └── pages/
```

------

##### 💡 `forRoot()` 和 `forChild()` 用法（服务作用域控制）

- **SharedModule** 不应提供服务；
- **CoreModule** 中服务应以 `forRoot()` 方式提供；

```ts
@NgModule({})
export class SomeLibraryModule {
  static forRoot(): ModuleWithProviders<SomeLibraryModule> {
    return {
      ngModule: SomeLibraryModule,
      providers: [SomeService]
    };
  }
}
```

------

#### 🧭 三、路由与模块的关系

##### 路由懒加载（配合模块拆分）

```ts
const routes: Routes = [
  {
    path: 'user',
    loadChildren: () => import('./features/user/user.module').then(m => m.UserModule)
  }
];
```

##### 每个懒加载模块应：

- 拥有自己的 RoutingModule（`RouterModule.forChild()`）
- 不再出现在 AppRoutingModule 中

------

#### ✨ 四、Standalone 架构（Angular 15+ 新趋势）

##### ✅ 什么是 Standalone？

- 可以脱离 `NgModule` 独立存在的组件/指令/管道；
- 更轻量；
- 更符合现代组件开发模型（像 React）；
- Angular 17 起默认推荐。

```ts
@Component({
  standalone: true,
  imports: [CommonModule],
  template: `...`
})
export class HelloComponent {}
```

------

##### ✅ Standalone 使用示例

路由中直接使用：

```ts
const routes: Routes = [
  {
    path: 'home',
    component: HomeComponent // standalone: true
  }
];
```

嵌套组合：

```ts
@Component({
  standalone: true,
  imports: [MatButtonModule, SharedComponent],
  template: `<shared-button />`
})
export class PageComponent {}
```

------

#### 🧩 五、NgModule 与 Standalone 混合设计推荐

1. 渐进式迁移策略（企业项目适用）

| 推荐层                   | 使用类型                   |
| ------------------------ | -------------------------- |
| Page层（每页）           | Standalone Component       |
| Layout层                 | Standalone                 |
| Widget层（表格、卡片等） | Standalone                 |
| SharedModule             | 保留（兼容旧模块）         |
| CoreModule               | 可保留（用于服务、拦截器） |

------

2. 模块划分建议（基于 Standalone）

```
src/
├── app.config.ts             // providers + routes + bootstrap（新风格）
├── features/
│   ├── home/
│   │   ├── home.page.ts     // standalone page
│   │   ├── components/      // standalone UI 组件
│   │   └── services/
├── shared/                   // 纯组件库
├── core/                     // 单例服务（仍推荐 NgModule）
```

------

#### ✅ 六、模块设计实战经验总结

| 场景                       | 建议                                            |
| -------------------------- | ----------------------------------------------- |
| 组件被多个页面复用         | 放到 `shared/components/` 并设为 standalone     |
| 页面只属于一个业务功能模块 | 使用 feature 目录组织并懒加载                   |
| 全局服务                   | 放在 CoreModule 中，注册为 `providedIn: 'root'` |
| 指令/管道被多个地方使用    | 放入 SharedModule 并导出                        |
| 配合 SSR 或微前端          | 推荐继续使用 NgModule 组织公共资源              |

------

#### ⚠️ 七、常见误区与建议

| 问题                    | 解决方案                                 |
| ----------------------- | ---------------------------------------- |
| 模块循环依赖            | 拆分为更小模块或使用 InjectionToken 替代 |
| 服务多次实例化          | 使用 `providedIn: 'root'` 或 `forRoot()` |
| 导入未导出组件报错      | 确保导出声明到 exports 数组中            |
| 所有模块都放 AppModule  | ❌，应拆分为 Feature + Shared             |
| 把服务放在 SharedModule | ❌，应放 CoreModule 或使用 `providedIn`   |

------

#### 🔚 八、结语

Angular 的模块系统（NgModule + Standalone）在 Angular 19 中是双轨并行：

- `NgModule` 适合大型项目、复杂依赖；
- `Standalone` 更现代、更灵活，建议逐步迁移。

模块设计是 Angular 架构的核心，合理划分模块可以极大提升：

✅ 项目可维护性
 ✅ 团队协作效率
 ✅ 性能（懒加载）
 ✅ 可测试性（每个模块单测）

------

