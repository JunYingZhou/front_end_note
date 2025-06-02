# uni-app

**是一个使用vue.js开发所有前端的框架，可以发布到IOS,Android,H5,以及小程序**

![image-20240228185714837](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228185714837.png)

开发工具 （HBuilderX,VS等）

# 一、环境配置

![image-20240228191128950](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228191128950.png)

## 1.1 创建uni-app项目

文件-> 新建-> 项目-> uni-app项目模板

## 1.2 目录结构

![image-20240228191957434](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228191957434.png)

## 1.3 将uni-app 运行到微信开发者工具

![image-20240228192154393](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228192154393.png)

![image-20240228192329431](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228192329431.png)

![image-20240228192454517](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228192454517.png)

![image-20240228192550542](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228192550542.png)

## 1.4 Git管理

![image-20240228193553749](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228193553749.png)

生成公钥

![image-20240228194324732](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228194324732.png)

# 二.TabBar

## 2.1 创建tabar分支

```
git checkout -b tabbar
```

![image-20240228195038850](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228195038850.png)

![image-20240228195101458](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228195101458.png)

在pages.json当中

```js
"tabBar": {
		"color": "#7A7E83",
		"selectedColor": "#007AFF",
		"borderStyle": "black",
		"backgroundColor": "#F8F8F8",
		"list": [{
				"pagePath": "pages/home/home",
				"iconPath": "static/tab_icons/home.png",
				"selectedIconPath": "static/tab_icons/home-active.png",
				"text": "首页"
			},
			{
				"pagePath": "pages/cate/cate",
				"iconPath": "static/tab_icons/cate.png",
				"selectedIconPath": "static/tab_icons/cate-active.png",
				"text": "分类"
			}, {
				"pagePath": "pages/Cart/Cart",
				"iconPath": "static/tab_icons/cart.png",
				"selectedIconPath": "static/tab_icons/cart-active.png",
				"text": "购物车"
			}, {
				"pagePath": "pages/my/my",
				"iconPath": "static/tab_icons/my.png",
				"selectedIconPath": "static/tab_icons/my-active.png",
				"text": "我的"
			}
		]
	}
```

微信小程序当中的，需要将为tabbar的放置到最前面

![image-20240228201456510](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228201456510.png)

## 2.2 导航栏

![image-20240228202028302](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240228202028302.png)

## 2.3 分支的提交与合并

```
git add .添加到缓冲区
git commit -m 'asdadsa' 提交代码

将分支推送到远程仓库
git push -u origin tabbar

将本地的tabbar分支合并到本地的master:
git chechout master
git merge tabber

删除本地的tabbar分支：
git branch -d tabbar
```

## 2.4 home分支

![image-20240229230213069](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240229230213069.png)

## 2.5 配置网络请求

![image-20240229230539313](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240229230539313.png)

```
import { Shttp ) from
'@escook/request-miniprogram
uni.Shttp = Shttp
//配置请求根路径
Shttp.baseUrl = https://www.uinav .com
//请求开始之前做一些事情
Shttp.beforeRequest = function (options) (
uni .showLoading(f
title:"数据加载中
// 请求完成之后做一些事情
Shttp
afterRequest
function ()(
uni .hideLoading()
```

安装

```
npm install @escook/request-miniprogram
```

导入

```
按需导Shttp对象
import {$http} from @escook/request-miniprogram
fron
将按需导入的
挂载到 顶级对象之上，方便全局调用
wx.Shttp = Shttp
在 uni-app 项月中，可以把 Shttp 挂裁到 uni 顶级对象之上，方便全局调用
uni.Mttp = Shttp
```

使用

![image-20240229231002799](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240229231002799.png)

 请求拦截器

```js
$http.beforeRequest= function () {

​     	// do something....

}
```

响应拦截器

```
$http.afterRequest= function () {

​     	// do something....

}
```

## 操作步骤：

1. 初始化npm包

2. ```
   npm init -y
   ```

3. ![image-20240229231548066](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240229231548066.png)

再输入

```
npm install @escook/request-miniprogram
```

```js
// 导入网络请求的包
import {$http} from '@escook/request-miniprogram'

uni.$http = $http

// 请求拦截
$http.beforeRequest = function(options) {
  uni.showLoading({
    title: '数据加载中...'
  })
}

// 响应拦截器
$http.afterRequest = function(){
   uni.hideLoading()
 }
```

# 三、轮播图

![image-20240229233309499](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240229233309499.png)

## 3.1 uni-app 配置小程序打包

![image-20240301000928855](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301000928855.png)

创建分包

![image-20240301001023804](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301001023804.png)

![image-20240301001002848](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301001002848.png)

## 3.2 点击轮播图跳转页面

![image-20240301001245346](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301001245346.png)

## 3.3 封装uni.$showMsg()方法

```js
 // 封装弹框的方法
 uni.$showMsg = function(title = '数据请求失败',duration = 1500){
   uni.showToast({
     title:,
     duration,
     icon:'none'
   })
 }
```

![image-20240301001937678](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301001937678.png)

## 3.4获取分类导航方法

![image-20240301004239150](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301004239150.png)

### 3.4.1 渲染UI

![image-20240301004351701](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301004351701.png) 

### 3.4.2 点击分类事件

![image-20240301005529641](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301005529641.png)

# 四、分类区域

## 4.1 页面基本结构

![image-20240301214742942](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240301214742942.png)

## 4.2 获取系统信息

调用API

![image-20240303011154752](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303011154752.png)

![image-20240303011226340](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303011226340.png)

# 五、搜索框

## 5.1.1 搜索框基本结构

![image-20240303013315322](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303013315322.png)

## 5.1. 2 吸顶

![image-20240303013146762](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303013146762.png)

## 5.1.3 自动获取焦点

![image-20240303012848501](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303012848501.png)

## 5.1.4 获取输入

![image-20240303013444187](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303013444187.png)

## 5.1.5 防抖处理

![image-20240303013717769](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303013717769.png)

## 5.1.6 关键字重复

![image-20240303021149724](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303021149724.png)

## 5.1.7 将搜索历史存储到本地

![image-20240303021427234](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303021427234.png)

## 5.1.8 清空数据

![image-20240303021718026](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303021718026.png)

## 5.1.9 点击跳转

![image-20240303021804850](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303021804850.png)

# VUEX

## 初始化

![image-20240303023711403](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303023711403.png)

## 实例化Store对象

![image-20240303023813449](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303023813449.png)

## 导入store对象，挂载到Vue实例上

![image-20240303023950052](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303023950052.png)

## 初始化购物车的vuex模块

![image-20240303024221016](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303024221016.png)

## 在store模块中导入购物车的vuex模块

![image-20240303024442033](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303024442033.png)

## 在页面中使用对应的store数据

![image-20240303024706458](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303024706458.png)

## 对store数据进行操作

![image-20240303025814352](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303025814352.png)

![image-20240303025920485](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303025920485.png)

## 设置tabbar的数字

![image-20240303030939342](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303030939342.png)

![image-20240303030953133](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303030953133.png)

# 登录/支付

 

![image-20240303023204514](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303023204514.png)

设置user.js中的token

![image-20240303221854996](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303221854996.png)

![image-20240303221814408](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303221814408.png)

# 登录

## 1.创建组件

![image-20240303222106527](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303222106527.png)

![image-20240303222141069](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303222141069.png)

## 2.在组件中导入token字符串

![image-20240303222218350](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303222218350.png)

## 登录API

![image-20240303222720488](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303222720488.png)

## 点击获取用户基本信息（）

![image-20240303222903471](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303222903471.png)

![image-20240303223301239](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303223301239.png)

```vue
<template>
	<view class="content">
		<image src="logo.png"></image>
		<view class="title">申请获取以下权限</view>
		<text class="msg">获取你的公开信息（昵称、头像、地区等）</text>
		<!-- #ifdef MP-WEIXIN -->
		<button class="btn" @click="wxgetUserInfo">授权登录</button>
		<!-- #endif -->
		<!-- #ifdef MP-ALIPAY -->
		<button class="btn" open-type="getAuthorize" @getAuthorize="alipaygetUserInfo" @error="onAuthError" scope='userInfo'>授权登录</button>
		<!-- #endif -->
	</view>
</template>

<script>
	import { loginByWx, loginByAlipay } from '@/api/user.js'
	export default {
		data() {
			return {
				code: new String()
			}
		},
		async onLoad() {
			this.code = await this.getAppCode()
		},
		methods: {
			// 获取微信用户信息
			async wxgetUserInfo() {
				try {
					// 微信登录
					// #ifdef MP-WEIXIN
					let userData = await this._getwxUserData()
					// 调用后台接口登录
					let loginRes = await this.appLogin(userData)
					// savecache
					uni.setStorageSync('isLogin', true)
					uni.setStorageSync('userInfo', {
						headImg: loginRes.headImg,
						userName: loginRes.userName
					});
					uni.setStorageSync('token', loginRes.token)
					uni.setStorageSync('userId', loginRes.userId)
					uni.navigateBack({
						delta: 1
					});
					// #endif					
				} catch(err) {
					this.onAuthError()
				}
			},
			// 支付宝用户登录
			async alipaygetUserInfo() {
				try {
					// 支付宝登录
					// #ifdef MP-ALIPAY
					let userData = await this._getalipayUserData()
					// 调用后台接口登录
					let loginRes = await this.appLogin(userData)
					loginRes.userName = userData.nickName
					loginRes.headImg = userData.avatar
					// savecache
					uni.setStorageSync('isLogin', true)
					uni.setStorageSync('userInfo', {
						headImg: loginRes.headImg,
						userName: loginRes.userName
					})
					uni.setStorageSync('token', loginRes.token)
					uni.setStorageSync('userId', loginRes.userId)
					uni.navigateBack({
						delta: 1
					})
					// #endif					
				} catch(err) {
					this.onAuthError()
				}
			},
			// 授权失败
			onAuthError() {
				uni.showToast({
					title: '授权失败，请确认授权已开启',
					mask: true,
					icon: 'none'
				})
			},
			// 获取支付宝用户加密数据
			_getalipayUserData() {
				return new Promise((resolve, reject) => {
					my.getOpenUserInfo({
						success: res => {
							let userInfo = JSON.parse(res.response).response
							resolve(userInfo)
						},
						fail: err => {
							reject(err)
						}
					})
				})
			},
			// 获取微信用户加密数据
			_getwxUserData() {
				// 用户信息接口调整，使用uni.getUserInfo() 获取到的用户信息是一个灰色的头像和微信用户
				// 需要使用 uni.getUserProfile() 获取用户信息，此方法需要按钮触发 @click=func
				return new Promise((resolve, reject) => {
					uni.getUserProfile({
						desc: '完善用户信息',
						success: data => {
							console.log("用户信息：", data)
							resolve(data)
						},
						fail: err => {
							reject(err)
						}
					})
				})
			},
			// 获取 临时登录凭证code
			getAppCode() {
				return new Promise((resolve, reject) => {
					// #ifdef MP-WEIXIN
					uni.login({
						provider: 'weixin',
						success(res) {
							resolve(res.code)
						},
						fail(err) {
							reject(err)
						}
					})
					// #endif
					// #ifdef MP-ALIPAY
					// 系统建议使用支付宝原生写法
					my.getAuthCode({
					  scopes: 'auth_base',
					  success(res) {
					  	resolve(res.authCode)
					  },
					  fail(err) {
					  	reject(err)
					  }
					 })
					// #endif
				})
			},
			// 用户登录
			appLogin(detail) {
				return new Promise(async(resolve, reject) => {
					try {
						// 微信登录
						// #ifdef MP-WEIXIN
						let params = {
							code: this.code,
							source: 'MP',
							encryptedData: detail.encryptedData,
							iv: detail.iv
						}
						let wxloginRes = await loginByWx(params)
						if(wxloginRes.code == 200) {
							resolve(wxloginRes.data)
						} else {
							reject(wxloginRes)
						}
						// #endif
						// #ifdef MP-ALIPAY
						// 系统建议使用支付宝原生写法
						let alipayloginRes = await loginByAlipay({
							code: this.code
						});
						if(alipayloginRes.code == 200) {
							resolve(alipayloginRes.data)
						} else {
							reject(alipayloginRes)
						}
						// #endif
					} catch(err) {
						reject(err)
					}
				});
			},
		}
	}
</script>

<style lang="less">
	view, text, image, input {
		box-sizing: border-box;
	}
	
	.content {
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
		height: 100vh;
		padding: 160rpx 40rpx 0;
		
		image {
			width: 275rpx;
			height: 104rpx;
		}
		.title {
			width: 100%;
			margin-top: 80rpx;
			font-size: 30rpx;
			font-weight: 600;
			color: rgba(0, 0, 0, 0.85);
			text-align: left;
		}
		.msg {
			display: block;
			width: 100%;
			margin-top: 16rpx;
			font-size: 28rpx;
			color: rgba(0, 0, 0, 0.65);
			text-align: left;
		}
		
		.btn {
			position: absolute;
			bottom: 160rpx;
			width: 670rpx;
			height: 96rpx;
			background: #00B391;
			border-radius: 8rpx;
			font-size: 34rpx;
			font-weight: 400;
			color: #FFFFFF;
			line-height: 96rpx;
		}
	}
</style>


```

## 登录获取Token

![image-20240303231746733](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240303231746733.png)

## 大体流程

![image-20240305015747330](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240305015747330.png)

// 用户授权之后，获取用户的基本信息
      getUserInfo(e) {
        console.log(e)

```js
    if (e.detail.errMsg === 'getUserInfo:fail auth deny') return uni.$showMsg('您取消了登录授权！')

    console.log(e.detail.userInfo)
    this.updateUserInfo(e.detail.userInfo)

    this.getToken(e.detail)
  },
  
  async getToken(info) {
    // 获取 code 对应的值
    // const [err, res] = await uni.login().catch(err => err)
    uni.login({
      success(lres) {
        console.log(lres,123)
        if (err || lres.res.errMsg !== 'login:ok') return uni.$showMsg('登录失败！')
      }
    })
    // 准备参数
    const query = {
      code: res.code,
      encryptedData: info.encryptedData,
      iv: info.iv,
      rawData: info.rawData,
      signature: info.signature
    }

    const { data: loginResult } = await uni.$http.post('/api/public/v1/users/wxlogin', query)
    if (loginResult.meta.status !== 200) return uni.$showMsg('登录失败！')

    // 直接把 token 保存到 vuex 中
    this.updateToken(loginResult.message.token)
    this.navigateBack()
  },
```