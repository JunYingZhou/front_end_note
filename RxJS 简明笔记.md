# RxJS 简明笔记

## 📌 什么是 RxJS？

RxJS（Reactive Extensions for JavaScript）是一个用于响应式编程的库，基于 **Observable（可观察对象）** 的概念。它提供了一套强大的操作符，用来以声明式方式处理异步数据流（如事件、请求、定时器等）。

> 简单理解：RxJS 就是一个工具库，用来优雅地处理异步事件和数据流。

------

## 🧠 为什么使用 RxJS？

- 更优雅地处理复杂异步逻辑（多次请求、节流、防抖、错误处理等）
- 操作符可组合性强（像乐高一样搭积木）
- 提高代码可读性和维护性
- 强大的流控制能力

------

## 🧩 核心概念

- **Observable**：可观察对象，表示一个数据流，可以被订阅
- **Observer**：观察者，定义对数据流的处理逻辑（next, error, complete）
- **Subscription**：表示订阅行为，可用于取消订阅（unsubscribe）
- **Operators**：操作符，用于转换、过滤、合并等（如 `map`、`filter`、`mergeMap`）
- **Subject**：既是 Observable 也是 Observer，可实现多播（多个订阅共享同一个数据源）

------

## 🔧 示例：基本使用

```ts
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

const source$ = of(1, 2, 3); // 创建一个 Observable 发出 1,2,3

source$
  .pipe(
    map(x => x * 2) // 使用 map 操作符转换数据
  )
  .subscribe(value => {
    console.log(value); // 输出：2, 4, 6
  });
```

------

## 💡 常见使用场景

- 表单输入防抖（debounceTime）
- 搜索建议（自动补全）
- 串行或并行 API 请求
- 实时数据流处理（如 WebSocket）
- DOM 事件响应（如点击、滚动、拖拽）

------

## 📚 常用操作符简表

- `map`：数据映射转换
- `filter`：过滤符合条件的数据
- `debounceTime`：延迟一定时间后再发出最后一次数据
- `mergeMap`：将每个值映射成 Observable 并合并
- `switchMap`：取消前一个内部 Observable，切换到新的
- `catchError`：错误处理
- `take`：取前 N 个值

------

## ⚙️ 在哪些框架中常用？

- **Angular**：RxJS 是核心组成部分，广泛用于 HTTP、路由、表单等模块。
- **React/Vue**：可选用，适合处理复杂的异步交互、状态管理、组件通信等场景。

------

## 📌 一句话总结

**RxJS = 可观察的数据流 + 操作这些流的强大工具集**

------



好的，下面是两个你提到的 Angular 中 **RxJS 实战场景**示例：

------

## ✅ 1. 表单防抖（如搜索建议）

这是 Angular 中常见的场景，比如输入框内容变化后，防抖 500ms 发出搜索请求：

### 示例代码（Reactive Forms）

```ts
// search.component.ts
import { Component, OnInit } from '@angular/core';
import { FormControl } from '@angular/forms';
import { debounceTime, distinctUntilChanged, switchMap } from 'rxjs/operators';
import { SearchService } from './search.service';

@Component({
  selector: 'app-search',
  template: `<input type="text" [formControl]="searchControl" placeholder="搜索...">`
})
export class SearchComponent implements OnInit {
  searchControl = new FormControl();

  constructor(private searchService: SearchService) {}

  ngOnInit() {
    this.searchControl.valueChanges.pipe(
      debounceTime(500),               // 防抖：延迟500ms
      distinctUntilChanged(),          // 值不变则不发请求
      switchMap(value => this.searchService.search(value)) // 取消前一个请求，发最新的
    ).subscribe(results => {
      console.log('搜索结果:', results);
    });
  }
}
// search.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({ providedIn: 'root' })
export class SearchService {
  constructor(private http: HttpClient) {}

  search(query: string) {
    return this.http.get(`/api/search?q=${query}`);
  }
}
```

------

## ✅ 2. 多个请求并发（如页面初始化获取多个接口数据）

使用 `forkJoin` 实现多个请求并发，全部成功后再继续处理。

### 示例代码

```ts
// dashboard.component.ts
import { Component, OnInit } from '@angular/core';
import { forkJoin } from 'rxjs';
import { DataService } from './data.service';

@Component({
  selector: 'app-dashboard',
  template: `<p>加载完成</p>`
})
export class DashboardComponent implements OnInit {
  constructor(private dataService: DataService) {}

  ngOnInit() {
    forkJoin({
      userInfo: this.dataService.getUserInfo(),
      messages: this.dataService.getMessages(),
      tasks: this.dataService.getTasks()
    }).subscribe(result => {
      console.log('用户信息:', result.userInfo);
      console.log('消息列表:', result.messages);
      console.log('任务列表:', result.tasks);
    });
  }
}
// data.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({ providedIn: 'root' })
export class DataService {
  constructor(private http: HttpClient) {}

  getUserInfo() {
    return this.http.get('/api/user');
  }

  getMessages() {
    return this.http.get('/api/messages');
  }

  getTasks() {
    return this.http.get('/api/tasks');
  }
}
```

------

## 💡 补充说明

- `switchMap`：用于表单防抖时避免同时发多个请求，自动取消旧请求。
- `forkJoin`：等待所有请求完成后再统一返回所有结果，适合页面初始化场景。
- 如果是“任意一个返回就响应”，可以用 `combineLatest`、`merge`、`race` 等。



## ✅ 2. 多个请求并发（如页面初始化获取多个接口数据）

1. 创建一个专用的事件服务（EventBusService）。
2. 使用 `Subject` 或 `BehaviorSubject` 发布和订阅事件。
3. 各组件通过该服务进行通信，无需父子关系。

------

### 🛠️ 实现步骤

#### 第一步：创建事件总线服务

```ts
// event-bus.service.ts
import { Injectable } from '@angular/core';
import { Subject } from 'rxjs';

@Injectable({ providedIn: 'root' })
export class EventBusService {
  private eventSubject = new Subject<{ name: string; payload?: any }>();

  // 发送事件
  emit(eventName: string, payload?: any) {
    this.eventSubject.next({ name: eventName, payload });
  }

  // 监听事件
  on(eventName: string) {
    return this.eventSubject.asObservable().pipe(
      filter(event => event.name === eventName),
      map(event => event.payload)
    );
  }
}
```

> 记得引入 `filter` 和 `map` 操作符：

```ts
import { filter, map } from 'rxjs/operators';
```

------

#### 第二步：组件中使用

A组件 - 发出事件

```ts
// component-a.component.ts
constructor(private eventBus: EventBusService) {}

sendData() {
  this.eventBus.emit('custom-event', { message: 'Hello from A!' });
}
```

B组件 - 监听事件

```ts
// component-b.component.ts
constructor(private eventBus: EventBusService) {}

ngOnInit() {
  this.eventBus.on('custom-event').subscribe(data => {
    console.log('B组件收到事件：', data);
  });
}
```

------

### 🔄 其他可选方式

| 方式              | 说明                                   |
| ----------------- | -------------------------------------- |
| `Subject`         | 无初始值，适合事件流                   |
| `BehaviorSubject` | 有初始值，订阅即拿到最新值（适合状态） |
| `ReplaySubject`   | 可以缓存过去 N 个值                    |

------

### 🧠 场景举例

- 页面中多个组件之间传递数据（如弹窗、通知）
- 非父子组件通信（如导航栏控制主区域）
- 模块解耦，事件触发不依赖具体组件结构

------

### ✅ 小结

事件总线服务 = `Subject` + `RxJS` 操作符（`filter/map`）+ Angular 单例服务。

它是 Angular 中组件通信的经典手法，尤其在大型项目中，可以提升可维护性和灵活性。

------

