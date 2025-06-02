# ArkTs/Harmony快速上手

JS->TS->ArkTS

# 一、基础语法（TypeScript）

1.布尔值

TypeScript中可以使用boolean来表示这个变量是布尔值，可以赋值为true或者false。

```typescript
let isDone:boolean = false;
```

2.数字

TypeScript里的所有数字都是浮点数，这些浮点数的类型是number。除了支持十进制，还支持二进制、八进制、十六进制。

```typescript
let decLiteral:number = 2023;
let decLiteral:number = 0b11111100111;
let decLiteral:number = 0o3747;
let decLiteral:number = 9x7e7;
```

3.字符串

TypeScript里使用string表示文本数据类型，可以使用双引号("）或单引号（'）表示字符串。

```typescript
let name:string = 'jack';
name = "Tome";
name = 'rose';
```

4.数组

TypeScript支持以下两种方式声明数组:第一种，可以在元素类型后面接上门，表示由此类型元素组成的一个数组;第二种方式是使用数组泛型，Array<元素类型>。

```typescript
let list1:number[]=[1,2,3];
let list2:Array<number> = [1,2,4];
```

5.元组

元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。

```typescript
let x:[string,number];
x = ['hello',10]; //ok
x = [10,'hell0']; // Error
```

6.枚举

enum类型是对JavaScript标准数据类型的一个补充，使用枚举类型可以为一组数值赋予友好的名字。

```typescript
enum Color {Red,Green,Blue};
let c:Color = Color.Green
```

7.unknown

有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。那么我们可以使用unknown类型来标记这些变量。

```typescript
let notSure:unknown = 4;
notSure = 'maybe a string instead';
notSure = false;
```



8.void

当一个函数没有返回值时，通常返回值类型是void

```typescript
function test():void{
    cosole.log('this is functuion is void');
}
```

9.null 和 undefined

TypeScript里,undefined和null两者各自有自己的类型分别叫做undefined和null。

```typescript
let u:undefined = undefined;
let u:null = null;
```

10:联合类型

```typescript
let myFavoriteNumber: string|number;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```

# 二、条件语法

1.if-else if -else   (0, ,null,undefined，都是false)

![image-20231116132352340](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231116132352340.png)

2.switch

![image-20231116132455972](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231116132455972.png)

3 方法：

```typescript
function sayHello(name?: string){

name = name ? name : '陌生人'

}
```



对象：

```typescript
// 定义枚举
enum Msg{
    HI = 'Hi',
    HELLO = 'hello'
}
// 定义接口
interface A {
    say(msg: Msg) :void
}
// 实现接口
class B implements A {
    say(msg: Msg):void{
        consle.log
    }
}
// 初始化对象
let a:A = new B()
// 调用对象
a.say(Msg.HI)
```

模块开发：





# 三、ArkTS的开发规范

![img](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/103/404/958/0260086000103404958.20221102104418.97167608875006783664909326988909:50001231000000:2800:B0A2A3474E494DE620CBF58C0DBB2F835EBDAC07C87E2376865D3CA5ED979896.png)

装饰器：

用来装饰类、结构体、方法以及变量，赋予其特殊的含义，如上述示例中 @Entry 、 @Component 、 @State 都是装饰器。具体而言， @Component 表示这是个自定义组件； @Entry 则表示这是个入口组件； @State 表示组件中的状态变量，此状态变化会引起 UI 变更。

自定义组件：

可复用的 UI 单元，可组合其它组件，如上述被 @Component 装饰的 struct Hello。

UI描述：

声明式的方式来描述 UI 的结构，如上述 build() 方法内部的代码块。

内置组件：

框架中默认内置的基础和布局组件，可直接被开发者调用，比如示例中的 Column、Text、Divider、Button。

事件方法：

用于添加组件对事件的响应逻辑，统一通过事件方法进行设置，如跟随在Button后面的onClick()。

属性方法：

用于组件属性的配置，统一通过属性方法进行设置，如fontSize()、width()、height()、color() 等，可通过链式调用的方式设置多项属性。

### 1.自定义组件

ArkTS通过struct声明组件名，并通过@Component和@Entry装饰器，来构成一个自定义组件。

使用@Entry和@Component装饰的自定义组件作为页面的入口，会在页面加载时首先进行渲染。

```typescript
@Entry

@Component

struct ToDoList{.....}
```

使用@Component装饰的自定义组件，如ToDoItem这个自定义组件则对应如下内容，作为页面的组成部分。

```ty
@Component
struct ToDoItem {...}
```

在ToDoList当中需要使用build方法进行UI描述

```typescript
@Entry
@Component
 struct ToDoList
   ...
   build() {
    ...
  } 
}
```

ROW和COLUMN

![image-20231116213854628](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231116213854628.png)

COLUMN

![image-20231116213914604](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231116213914604.png)

forEach:

1.定义数组

```typescript
total_Tasks:Array<string> = [
  '早起晨练',
  '准备早餐',
  '阅读名著',
  '学习ArkTS',
  '看剧放松'
]
```

遍历数组：

```typescript
@Entry
@Component
struct ToDoList {
   ...
   build() {
     Row() {
       Column() {
         Text(...)
           ...
         ForEach(this.totalTasks,(item) => {
           TodoItem({content:item})
         },...)
       }
       .width('100%')
     }
     .height('100%')
   }
 }
```

### 2.应用程序入口----AbilityUI

UIAbility是一种包含用户界面的应用组件，主要用于和用户进行交互。UIAbility也是系统调度的单元，为应用提供窗口在其中绘制界面。

每一个UIAbility实例，都对应于一个最近任务列表中的任务。

一个应用可以有一个UIAbility，也可以有多个UIAbility，如下图所示。例如浏览器应用可以通过一个UIAbility结合多页面的形式让用户进行的搜索和浏览内容；而聊天应用增加一个“外卖功能”的场景，则可以将聊天应用中“外卖功能”的内容独立为一个UIAbility，当用户打开聊天应用的“外卖功能”，查看外卖订单详情，此时有新的聊天消息，即可以通过最近任务列表切换回到聊天窗口继续进行聊天对话。

一个UIAbility可以对应于多个页面，建议将一个独立的功能模块放到一个UIAbility中，以多页面的形式呈现。例如新闻应用在浏览内容的时候，可以进行多页面的跳转使用。

UIAbility的生命周期

![image-20231116222252408](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231116222252408.png)

# 四、基础组件的使用

### 1.组件介绍

组件（Component）是界面搭建与显示的最小单位，HarmonyOS ArkUI声明式开发范式为开发者提供了丰富多样的UI组件，我们可以使用这些组件轻松的编写出更加丰富、漂亮的界面。

组件根据功能可以分为以下五大类：基础组件、容器组件、媒体组件、绘制组件、画布组件。其中基础组件是视图层的基本组成单元，包括Text、Image、TextInput、Button、LoadingProgress等，例如下面这个常用的登录界面就是由这些基础组件组合而成。

1.text

```typescript
@Entry
@Component
struct TextDemo {
  build() {
    Row() {
      Column() {
        Text('HarmonyOS')
        Text('HarmonyOS')
          .fontColor(Color.Blue)
          .fontSize(20)
          .fontStyle(FontStyle.Italic)
          .fontWeight(FontWeight.Bold)
          .fontFamily('Arial')
      }
      .width('100%')
    }
    .backgroundColor(0xF1F3F5)
    .height('100%')
  }
}
```

![image-20231116222642935](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231116222642935.png)

2.TextInput (输入框)

```ty
TextInput()
  .fontColor(Color.Blue)
  .fontSize(20)
  .fontStyle(FontStyle.Italic)
  .fontWeight(FontWeight.Bold)
  .fontFamily('Arial') 
```

提示信息：

```ty
TextInput({ placeholder: '请输入帐号' })
  .placeholderColor(0x999999)
  .placeholderFont({ size: 20, weight: FontWeight.Medium, family: 'cursive', style: FontStyle.Italic })
```

输入值类型：

```ty
TextInput({ placeholder: '请输入密码' })
  .type(InputType.Password)
```

​	有normal,password,Email,Number

获取输入文本

```ty
@Entry
@Component
struct TextInputDemo {
  @State text: string = ''
 
  build() {
    Column() {
      TextInput({ placeholder: '请输入账号' })
        .caretColor(Color.Blue)
        .onChange((value: string) => {
          this.text = value
        })
      Text(this.text)
    }
    .alignItems(HorizontalAlign.Center)
    .padding(12)
    .backgroundColor(0xE6F2FD)
  }
}
```

Button

```ty
Button('登录', { type: ButtonType.Capsule, stateEffect: true })
  .width('90%')
  .height(40)
  .fontSize(16)
  .fontWeight(FontWeight.Medium)
  .backgroundColor('#007DFF')
  .onClick(() => {
  // 处理点击事件逻辑
  })
```

LoadingProgress 加载

```ty
LoadingProgress()
  .color(Color.Blue)
  .height(60)
  .width(60)
```

使用资源引用类型

这是硬编码

```ty
Button('登录', { type: ButtonType.Capsule, stateEffect: true })
  .width(300)
  .height(40)
  .fontSize(16)
  .fontWeight(FontWeight.Medium)
  .backgroundColor('#007DFF')
```

将这是硬编码可以写到资源当中（entry/src/main/rescource）

```ty
{
  "string": [
    {
      "name": "login_text",
      "value": "登录"
    }
  ]
} 
```

比如这样就可以去引用

```
Button($r('app.string.login_text'), { type: ButtonType.Capsule })
```

# 黑马

### 001 入门

```arktes
@Entry // 入口
@Component  // 标识为组件
struct Index {     // 自定义组件： 可复用的UI单元
  @State times: number = 0  // 以上是装饰器  状态器，改变就UI刷新

  build() {   // 进行UI描述
    Row() {
      Button(`你好啊${this.times}`)  // 内置组件
        .backgroundColor('#36D')    //  属性方法
        .onClick(() => this.times++)   // 事件方法
    }
    .height('100%')
    .width('100%')
    .justifyContent(FlexAlign.Center)
  }
}
```

![image-20231130152256781](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130152256781.png)

### 002 Image

项目启动权限

**![image-20231130153300286](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130153300286.png)**

### 004 text

```ty
@Entry // 入口
@Component  // 标识为组件
struct Index {     // 自定义组件： 可复用的UI单元
  @State times: number = 0  // 以上是装饰器  状态器，改变就UI刷新

  build() {   // 进行UI描述
    Row() {
      Column(){
        Image($r('app.media.picture')) // 读取本地文件
          .width(100)
          .width(200)
          .borderRadius(10)
          .interpolation(ImageInterpolation.High)
        Text($r('app.string.width_label'))
          .fontSize(20)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

配置resouces

![image-20231130160024484](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130160024484.png)

![image-20231130160040263](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130160040263.png)

三个文件都有配置

### 004 TextInput

![img](file:///C:\Users\34975\Documents\Tencent Files\3497577844\Image\C2C\CO2}}}$K[@D5B~K$LY8CAYE.png)

```typescript
@Entry // 入口
@Component  // 标识为组件
struct Index {     // 自定义组件： 可复用的UI单元
  @State pic_width: number = 50  // 以上是装饰器  状态器，改变就UI刷新

  build() {   // 进行UI描述
    Row() {
      Column(){
        Image($r('app.media.picture')) // 读取本地文件
          .width(this.pic_width)
          .borderRadius(10)
          .interpolation(ImageInterpolation.High)
        Text($r('app.string.width_label'))
          .fontSize(20)
          .fontWeight(FontWeight.Bold)
        TextInput({
          // text: this.pic_width.toFixed(0)
          placeholder:'请输入图片大小'
          // text: 'itcast' // 初始化文本
        })
          .width(150)
          .height(50)
          .backgroundColor('#FFF')
          .type(InputType.Number)  // 输入框类型
          .onChange(value => {  // 事件方法  将内容传递给我们  一个参数
            // 将value变成int
            this.pic_width = parseInt(value)
          })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

![image-20231130162220868](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130162220868.png)

### 005 Button

![img](file:///C:\Users\34975\Documents\Tencent Files\3497577844\Image\C2C\TW$3{I`NG(U2C31)GIUS1FQ.png)

```typescript
@Entry // 入口
@Component  // 标识为组件
struct Index {     // 自定义组件： 可复用的UI单元
  @State pic_width: number = 50  // 以上是装饰器  状态器，改变就UI刷新

  build() {   // 进行UI描述
    Row() {
      Column(){
        Image($r('app.media.picture')) // 读取本地文件
          .width(this.pic_width)
          .borderRadius(10)
          .interpolation(ImageInterpolation.High)
        Text($r('app.string.width_label'))
          .fontSize(20)
          .fontWeight(FontWeight.Bold)
        TextInput({
          text: this.pic_width.toFixed(0)
          // placeholder:'请输入图片大小'
          // text: 'itcast' // 初始化文本
        })
          .width(150)
          .height(50)
          .backgroundColor('#FFF')
          .type(InputType.Number)  // 输入框类型
          .onChange(value => {  // 事件方法  将内容传递给我们  一个参数
            // 将value变成int
            this.pic_width = parseInt(value)
          })
        Button('缩小')
          .width(80)
          .fontSize(20)
          .type(ButtonType.Capsule)
          .onClick(() => {
            if (this.pic_width >= 10) {
              this.pic_width -= 10
            }
          })

        Button('放大')
          .width(80)
          .fontSize(20)
          .onClick(() => {
            if (this.pic_width < 100 ) {
              this.pic_width += 10
            }
          })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### 006 Slider

```typescript
 Slider({
          min: 0,
          max: 300,
          value: this.pic_width,
          step: 10, // 步长
          style: SliderStyle.OutSet, // OutSet
          direction: Axis.Horizontal, // 锤子方向
          reverse: false // 是否反向滑动
        })
          .width('90%')
          .showTips(true)//展示百分比
          .blockColor('#36D')
          .trackThickness(7)
          .onChange(value => {
            //
            this.pic_width = value
          })
```

![img](file:///C:\Users\34975\Documents\Tencent Files\3497577844\Image\C2C\M`O4DTNSI5K[Y%}XLBTK2TK.png)

### 007 页面布局

![img](file:///C:\Users\34975\Documents\Tencent Files\3497577844\Image\C2C\AQL8T49GS320IV@U[%UYH]R.png)

![image-20231130165004047](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130165004047.png)

![image-20231130165142021](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130165142021.png)

![image-20231130165208065](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130165208065.png)

![image-20231130165320410](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130165320410.png)

```typescript
@Entry // 入口
@Component  // 标识为组件
struct Index {     // 自定义组件： 可复用的UI单元
  @State pic_width: number = 200  // 以上是装饰器  状态器，改变就UI刷新

  build() {   // 进行UI描述
    Column(){
      Row(){
        Image($r('app.media.picture')) // 读取本地文件
          .width(this.pic_width)
          .borderRadius(10)
          .interpolation(ImageInterpolation.High)
      }
      .width('100%')
      .height(400)
      .justifyContent(FlexAlign.Center) // 主轴

      Divider()

      Row(){
        Text($r('app.string.width_label'))
          .fontSize(20)
          .fontWeight(FontWeight.Bold)
        TextInput({
          text: this.pic_width.toFixed(0)
          // placeholder:'请输入图片大小'
          // text: 'itcast' // 初始化文本
        })
          .width(150)
          .height(50)
          .backgroundColor('#FFF')
          .type(InputType.Number)  // 输入框类型
          .onChange(value => {  // 事件方法  将内容传递给我们  一个参数
            // 将value变成int
            this.pic_width = parseInt(value)
          })
      }
      // .padding(20)
      .padding({left: 14,right: 14})
      .width('100%')
      .justifyContent(FlexAlign.SpaceBetween)
      .margin({top: 10})

      Divider()

      Row(){
        Button('缩小')
          .width(80)
          .fontSize(20)
          .type(ButtonType.Capsule)
          .onClick(() => {
            if (this.pic_width >= 10) {
              this.pic_width -= 10
            }
          })

        Button('放大')
          .width(80)
          .fontSize(20)
          .onClick(() => {
            if (this.pic_width < 300 ) {
              this.pic_width += 10
            }
          })
      }
      .width('100%')
      .margin({top: 10})
      .justifyContent(FlexAlign.SpaceEvenly)

      Divider()

      Row(){
        Slider({
          min: 0,
          max: 300,
          value: this.pic_width,
          step: 10, // 步长
          style: SliderStyle.OutSet, // OutSet
          direction: Axis.Horizontal, // 锤子方向
          reverse: false // 是否反向滑动
        })
          .width('90%')
          .showTips(true)//展示百分比
          .blockColor('#36D')
          .trackThickness(7)
          .onChange(value => {
            //
            this.pic_width = value
          })
      }
      .width('100%')
      .margin({top: 10})


    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Center)
  }
}
```

### 008 循环控制

数组：

![img](file:///C:\Users\34975\Documents\Tencent Files\3497577844\Image\C2C\THKPRK}C@NHZOF%H[$3U6YA.png)

### 009 List （支持滚动）

当元素太多，页面显示不完，

list 同时具备Coloum和Row功能

![img](file:///C:\Users\34975\Documents\Tencent Files\3497577844\Image\C2C\WV6XS]Y17NU8]0N$]S$3}AK.png)

![image-20231130180414225](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231130180414225.png)

List里面必须要有ListIteam(),ListItem里面必须要有一个跟组件

### 010 自定义组件

![image-20231206231156126](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231206231156126.png)

父类：

![image-20231206231215425](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231206231215425.png)

## 011 状态管理

### 011.1 @State状态装饰器

![image-20231206232329858](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231206232329858.png)

### 011.2 任务统计案例

### 011.3 Prop和Link

![image-20231207014838623](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231207014838623.png)

当用Link装饰的时候要用$

![image-20240328010540403](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240328010540403.png)

### 011.4 @Provide和@Consume

父组件

```typescript
@Extend(Text) function finishedTask(){
  .decoration({type:TextDecorationType.LineThrough})
  .fontColor('#B1B2B1')
}

import {JinDuCard} from '../components/JinDuCard'
import {TaskListPage} from '../components/TaskList'

class Stat{
  finishedTask: number = 0;
  totalTask: number = 0;
}

@Entry
@Component
struct Mission3{

  @Provide stat: Stat = new Stat()   // 通过对象传递


  build(){
    Column({space: 10}){
      // 1.任务进度卡片
      JinDuCard()  // 用Consume接受数据，不用传参数

      // 新增任务按钮
      TaskListPage()
    }
    .width('100%')
    .height('100%')
    .backgroundColor('#F1F2F3')
  }
}
```

子组件

```typescript
@Styles function card(){
  .width('95%')
  .padding(20)
  .backgroundColor(Color.White)
  .borderRadius(15)
  .shadow({radius: 6,color: '#1F000000',offsetX:2,offsetY: 4})
}


@Extend(Text) function finishedTask(){
  .decoration({type:TextDecorationType.LineThrough})
  .fontColor('#B1B2B1')
}

class Stat{
  finishedTask: number = 0;
  totalTask: number = 0;
}

@Component
export struct  JinDuCard{

  @Consume stat: Stat


  build() {
    Row(){
      Text('任务进度：')
        .fontSize(30)
        .fontWeight(FontWeight.Bold)
      Stack(){
        Progress({
          value: this.stat.finishedTask,
          total: this.stat.totalTask,
          type: ProgressType.Ring
        })
          .width(110)
        Row(){
          Text(this.stat.finishedTask.toString())
            .fontSize(24)
            .fontColor("36D")
          Text(' / ' + this.stat.totalTask.toString())
            .fontSize(24)
            .fontColor("36D")
        }
      }
    }
    .justifyContent(FlexAlign.SpaceEvenly)
    .card()
  }
}
```

### 011.5 @ObjectLink和@Observe

作用：在涉及嵌套对象或者数组元素为对象时的场景进行双向数据绑定

1. 给嵌套的对象上面加上@Observe的类型

### 037.欢迎页业务

相当于存入token

![image-20240320013113727](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013113727.png)

#### 037.1.自定义弹窗

![image-20240320013204528](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013204528.png)

![image-20240320013325126](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013325126.png)

#### 037.2.欢迎页

![image-20240320013354382](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013354382.png)

#### 037.3.Preference(在Ability生命周期的创建)

![image-20240320013458283](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013458283.png)

#### 037.4.欢迎事件处理

![image-20240320013648889](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013648889.png)

![image-20240320013707932](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013707932.png)

#### 037.5.修改启动页面

![image-20240320013750741](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320013750741.png)

### 038.首页Tabs

![image-20240320014035942](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320014035942.png)

父组件：定义变量，当页面显示的时候修改状态值，并将变量传递给子组件

![image-20240321084714877](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240321084714877.png)

![image-20240321085110425](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240321085110425.png)

子组件：用@Prop进行接受父组件的参数，并用@Watch进行数据监视

1. 当观察到状态变量的变化（包括双向绑定的AppStorage和LocalStorage中对应的key发生的变化）的时候，对应的@Watch的回调方法将被触发；
2. @Watch方法在自定义组件的属性变更之后同步执行；
3. 如果在@Watch的方法里改变了其他的状态变量，也会引起状态变更和@Watch的执行；
4. 在第一次初始化的时候，@Watch装饰的方法不会被调用，即认为初始化不是状态变量的改变。只有在后续状态改变时，才会调用@Watch回调方法

![image-20240321085318592](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240321085318592.png)

### 040.统计卡片

#### 040.2 Swiper

![image-20240320011644935](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320011644935.png)

#### 040.2.卡路里组件

小组件

![image-20240320012153997](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320012153997.png)

 组件内容

![image-20240320012356574](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320012356574.png)

Stack():层级关系

![image-20240320012547796](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320012547796.png)

### 043.面板

#### 043.1.Panel() 

![image-20240320175408460](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320175408460.png)

通过点击子组件控制父组件的@State

![image-20240320175002109](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320175002109.png)

父组件：

![image-20240320183814761](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320183814761.png)

子组件：
![image-20240320175130573](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320175130573.png)

![image-20240320175214707](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320175214707.png)

父组件

![image-20240320175449581](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320175449581.png)

#### 043.2.数字键盘

Grid():![image-20240320180213537](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320180213537.png)

![image-20240320180904550](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320180904550.png)

GridItem(): 必须用，相当于ForEach()当中的ListItem()  

![image-20240320181220377](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320181220377.png)

给按键绑定事件：

使用@Link，进行父子组件双向绑定（当使用@Link的时候，需要用$，而不是用this.）

父组件：

![image-20240320181530849](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320181530849.png)

子组件：

```ts
@Link amount: number;

Grid(){
ForEach(this.numbers, num =>
GridItem(){
Text(num).fontsize(20).fontweight(CommonConstants.FONT WEIGHT 900)
.keyBoxStyle()
.onclick(() => this.clickNumber(num) )
})
GridItem(){
Text('删除').fontsize(20).fontweight(CommonConstants.FONT_WEIGHT_900)
keyBoxStyle()
.onclick(()=> this.clickDelete())
```

点击事件：
![image-20240320182943464](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320182943464.png)

```typescript
clickDelete(){
    if(this.value.length <= 0){
        this.value = i
        this.amount = 0
        return
    }
    this.value = this.value.substring(0, this.value.length - 1)
    this.amount = this.parseFloat(this.value)
}
```

### 045.一端发布，多端部署

效果：

![image-20240320184031052](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320184031052.png)

#### 045.1.媒体查询

![image-20240320184605100](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320184605100.png)

#### 步骤：

1.创建工具类：

```typescript
import mediaQuery from '@ohos.mediaquery'
import BreakpointConstants from '../constants/BreakpointConstants'

export default class BreakpointSystem{

  // sm,md,lg的三个listener
  private smListener: mediaQuery.MediaQueryListener = mediaQuery.matchMediaSync(BreakpointConstants.RANGE_SM)
  private mdListener: mediaQuery.MediaQueryListener = mediaQuery.matchMediaSync(BreakpointConstants.RANGE_MD)
  private lgListener: mediaQuery.MediaQueryListener = mediaQuery.matchMediaSync(BreakpointConstants.RANGE_LG)

  smListenerCallback(result: mediaQuery.MediaQueryResult){
    if(result.matches){
      this.updateCurrentBreakpoint(BreakpointConstants.BREAKPOINT_SM) // sm
    }
  }

  mdListenerCallback(result: mediaQuery.MediaQueryResult){
    if(result.matches){
      this.updateCurrentBreakpoint(BreakpointConstants.BREAKPOINT_MD)
    }
  }

  lgListenerCallback(result: mediaQuery.MediaQueryResult){
    if(result.matches){
      this.updateCurrentBreakpoint(BreakpointConstants.BREAKPOINT_LG)
    }
  }

   // 将存储到AppStorage当中（key-value类型）
  updateCurrentBreakpoint(breakpoint: string){
    AppStorage.SetOrCreate(BreakpointConstants.CURRENT_BREAKPOINT, breakpoint)
  }

  register(){
    // 执行回调函数,当我设备发生改变时执行
    this.smListener.on('change', this.smListenerCallback.bind(this))
    this.mdListener.on('change', this.mdListenerCallback.bind(this))
    this.lgListener.on('change', this.lgListenerCallback.bind(this))
  }

  unregister(){
    this.smListener.off('change', this.smListenerCallback.bind(this))
    this.mdListener.off('change', this.mdListenerCallback.bind(this))
    this.lgListener.off('change', this.lgListenerCallback.bind(this))
  }
}
```

2.在首页获取初始值：

```typescript
  @StorageProp('currentBreakpoint') currentBreakpoint: string = BreakpointConstants.BREAKPOINT_SM //使用@StorageProp时必须初始化

// 使用组件生命周期，组件初始化时进行监听
  aboutToAppear(){
    this.breakpointSystem.register()
  }
// 使用组件生命周期，组件销毁时，取消监听
  aboutToDisappear(){
    this.breakpointSystem.unregister()
  }
```

3.利用键值类型实现获取对应的Value

```js
let p = {k:'v'}
p['k']获取到v
```

4.创建bean

```typescript
// 不确定是否是什么类型，使用泛型
declare interface BreakpointTypeOptions<T>{
  sm?:T,
  md?:T,
  lg?:T
}

export default class BreakpointType<T>{
   // 属性
  options: BreakpointTypeOptions<T>
  // 构造方法
  constructor(options: BreakpointTypeOptions<T>) {
    this.options = options
  }
  // 
  getValue(breakpoint: string): T{
    return this.options[breakpoint]
  }
}
```

5.示例

```typescript
.vertical(new BreakpointType({
      sm: false,
      md: true,
      lg: true
    }).getValue(this.currentBreakpoint))
```

# ArkTs文件上传：

# 1.导入模块

![image-20240320014500577](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320014500577.png)

# 2.导入依赖

![image-20240320014524994](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320014524994.png)

# 3.添加页面

![image-20240320014605307](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320014605307.png)

# 4.开启权限

![image-20240320014658810](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240320014658810.png)

# 封装Axios