# 多Ability模型

## 一、大概步骤

### 1.UIAbility的启动模式

![image-20240428172443249](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428172443249.png)

### 2.配置信息

![image-20240428172535190](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428172535190.png)

## 二、操作

### 1.新建一个ablilty

![image-20240428172626700](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428172626700.png)

### 2.自动创建一个目录

![image-20240428172728111](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428172728111.png)

### 3.修改ablilty启动页面

![image-20240428173739866](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428173739866.png)

### 4.DevEco会自动帮我们创建module.json5，修改启动模式

![image-20240428173915017](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428173915017.png)

## 三、准备跳转

### 1.准备context

在对应的跳转事件页面

```ts
  // 商城模块
  // 1.创建一个context
  private context = getContext(this) as common.UIAbilityContext
```

![image-20240428175225878](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428175225878.png)

```ts
         // 进行商城跳转，开启新的ability
            // 商城模块
            // 2. 跳转到目的地的Want
            let want: Want = {
              // 设备id,不写就是当前应用
              deviceId: "",
              // 跳转到哪个应用，在AppScope里面的app.json5
              bundleName: "com.qhc.weyoung",
              // 在module.json5里面
              moduleName: "entry",
              // ability名称
              abilityName: "MailAbility",
              // 如果是Specify，则要加上
              parameters: {
                instanceKey: "idx_" + item.itemId
              }
            }
            // 3. 跳转
            this.context.startAbility(want)
```

### 2.新建一个MailAbilityStage目录

![image-20240428180020494](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428180020494.png)

### 3.进行配置

```ts
import AbilityStage from '@ohos.app.ability.AbilityStage';
import Want from '@ohos.app.ability.Want';
export default class MailAbilityStage extends AbilityStage{

  onAcceptWant(want: Want): string {
    // 如果是则处理
    if (want.abilityName === "MailAbility") {
      return `MailAbilityInstance_${want.parameters.instanceKey}`
    }
    // 如果不是
    return " "
  }


}
```

![image-20240428190319071](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240428190319071.png)

## 四、进行回调

```ts
//返回上页面
      Image($r('app.media.router_back'))
        .width(30)
        .height(30)
        .onClick(() => {
          // ability的返回不能使用router
          // router.back();
          // 进行商城回跳，开启新的ability
          // 商城模块
          // 2. 跳转到目的地的Want
          let want: Want = {
            // 设备id,不写就是当前应用
            deviceId: "",
            // 跳转到哪个应用，在AppScope里面的app.json5
            bundleName: "com.qhc.weyoung",
            // 在module.json5里面
            moduleName: "entry",
            // ability名称
            abilityName: "EntryAbility",
            // 如果是Specify，则要加上
            // parameters: {
            //   instanceKey: "idx_" + item.itemId
            // }
          }
          // 3. 跳转
          this.context.startAbility(want)
        })
```



