# Vue3

## 一、vue3表单校验

 **1.定义表单规则，为泛型填与其的类型FormRules**

```typescript
const rules = reactive<FormRules>({
    phone:[
{ required: true，message: "请输入手机号",trigger: "blur” },
{ pattern: /^1\d{10}$/ ,message:"请输入正确的手机号" ,trigger: "blur"},
   ],
password: [
{ required: true，message: "请输入密码" , trigger : "change"},
{ min: 6， max: 18，message:“密码长度为6~18位"， trigger: "blur”}，]，

```

**2.在表单的属性里面写入**

```vue
<el-form ........ :rules="rules" ref="formRef">
    <el-form-item prop="相关规则"></el-form-item>
</el_form>
```

**3.创建变量，并且与表单引用标识同名，为泛型填写具体的类型FormInstance,以后可通过formRef.value访问表单实例**

```typescript
const formRef = ref<FormInstance>()
```

**4.提交**

```typescript
const onSubmit = async () => {
    // 7.表单准备提交是，进行校验
    await formRef.value?.validate().catch(err => {
        ElMessage.error('error')
        throw err
    })
    // 正式发送登录请求
}
```

## 二、vue3-Token存储（pinia）

### 1.pinia

```typescript
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }

  return { count, doubleCount, increment }
})
```

在 *Setup Store* 中：

- `ref()` 就是 `state` 属性
- `computed()` 就是 `getters`
- `function()` 就是 `actions`

注意，要让 pinia 正确识别 `state`，你**必须**在 setup store 中返回 **`state` 的所有属性**。这意味着，你不能在 store 中使用**私有**属性。不完整返回会影响 [SSR](https://pinia.vuejs.org/zh/cookbook/composables.html) ，开发工具和其他插件的正常运行。



### 2.pinia代码

```typescript
export const useTokenStore = defineStore( "mytoken", () =>{
// ref 相当于state
const tokenJson = ref("")
//computed 相当于getters
const token = computed<Token>(()=> {
try{
return JSON.parse(tokenJson. value || window.localStorage.getItem("TokenInfo") || "{}")catch (err) {
ElMessage.error( "josn字符串格式不对,转化对象时失败..")
    window.localStorage.setItem("TokenInfo","{}")
throw err
}
})
// function相当于actions
function saveToken(data: string) {
tokenJson.value = data
window.localstorage.setItem( "TokenInfo", data)
//相外暴露
return { token,saveToken }
})

```

## 三、vue3-路由跳转（授权检验）

```typescript
import { createRouter, createWebHistory } from 'vue-router'
import { useUserStore } from '@/stores/index.js'
// import { useUserStore } from '@/stores/index.js'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/login',
      name: 'login',
      component: () => import('@/views/login/login.vue')
    },
    {
      path: '/',
      name: '',
      meta: { requiresAuth: true },
      component: () => import('@/views/layout/LayoutContainer.vue'),
      redirect: '/dataAnalysis',
      children: [
        {
          path: '/dataAnalysis',
          component: () => import('@/views/dataAnalysis/DataAnalysis.vue')
        },
        {
          path: '/patient',
          component: () => import('@/views/user/PatientManage.vue')
        },
        {
          path: '/personData',
          component: () => import('@/views/user/PersonData.vue')
        },
        {
          path: '/user',
          component: () => import('@/views/user/UserManage.vue')
        },
        {
          path: '/doctor',
          component: () => import('@/views/user/DoctorManage.vue')
        },
        {
          path: '/equipment',
          component: () => import('@/views/equipment/EquipmentManage.vue')
        },
        {
          path: '/community',
          component: () => import('@/views/community/CommunityManage.vue')
        },
        {
          path: '/cases',
          component: () => import('@/views/health/CasesManage.vue')
        },
        {
          path: '/weekAndMonthly',
          component: () => import('@/views/health/WeeklyAndMonthly.vue')
        },
        {
          path: '/userinfo',
          component: () => import('@/views/user/UserInfo.vue')
        }
      ]
    }
  ]
})

router.beforeEach((to, from, next) => {
  const store = useUserStore();
  const isAuthenticated = store.authorization // 根据实际情况获取用户登录状态
  const requiresAuth = to.matched.some((record) => record.meta?.requiresAuth)

  if (requiresAuth && !isAuthenticated) {
      // 登录过后，跳转到之前的页面
    next({ name: 'login', query: { redirect: to.fullPath } }) 
  } else {
    next();
  }
});

export default router

```

## 四、vue3_api的Header授权

**每次发起请求的时候，将token值作为Header传给后端**

```typescript
request.interceptors.request.use((config) =>{
    if (!config.headers) {
		config. headers = {} as AxiosRequestHeaders
    }
	const store = useTokenStore()
	config.headers.Authorization = store.token?.access_token
    
    return config
})

```

## 五、退出登录

```typescript
const handleLogout = async ( =>{
//退出-弹窗确认．点确认:返回成功promise点取消:返回失败promiseawait ElMessageBox.confirm("确认要退出吗?"，"提示"，{
confirmButtonText: "确认"，
cacelButtonText:"取消"，type: "warning",
}).catch(() =>{
ElMessage.error("操作已取消")
return new Promise(() =>) //取消退出操作时,阻止代码向后执行
})
                   
await logout().catch(() =>{})//告诉服务器端用户准备退出.(服务器端可能会有一个关闭清理动ElMessage.success("用户已登出")l/弹窗告诉用户成功退出
    
    
useTokenstore( ).saveToken("") //清空token
//需导入useTokenstore
router.push("/login")//跳转到登录页．(此处不能使用useRouter)需导入 useRouter}

```

## 六、token过期处理

Token过期处理

出于安全考虑（被第三方拿到)， token在一段时间后会失效。
首次获取tokenInfo时，含有三个相关信息:

access_token字符串。需要使用它，才能向接口请求到数据
expires_inaccess_token的过期时间
refresh_token用于刷新获取新的 access_token、expires_in、refresh_token

1.refreshToken API

```typescript
//定义接口返回类型
type RToken = {success: booleanstate: numbermessage: stringcontent: string}
//1.封装刷新token的接口函数
export const refreshToken = () =>{const store = useTokenstore()
return request<RToken>({
	method : "POST",
	url: "/front/user/refresh_token",
    params : {
		refreshtoken: store.token.refresh_token,
        //2.添加参数
    }，
})}

```



```typescript
//1.配置响应拦截器
request.interceptors.response.use(( response) => response,
async (error) =>{
	if (error.response.status === 401) {
	const { data } = await refreshToken() 
//这里不用catch，会默认生成reject的promise
	if (data.success) {
    	useTokenstore().saveToken(data.content)//保存新的 token
        	return request(error.config)
        	//使用原来的配置项，重新请求
    }else {
		ElMessage.error("刷新token失败，需重新登录!")
		router.push({ name: "login"，query: { redirect: 					router.currentRoute.value.fullPath } })
    	return
		}
	}
    // 包裹成一个失败的Promise
	return Promise.reject(error)
	}
)
export default request

```

## 七、避免重复刷新token

```typescript
let isRefreshing = false
// 1.1是否刷新中标志
let promiseRT: Promise<any>
// 1.2保存请求的promise对象
export const refreshToken = () =>{
	if (isRefreshing) {
		return promiseRT
    }
	isRefreshing = true
	const store = useTokenstore()
    promiseRT = request<RToken>({
	// 2.1把请求返回值保存到变量
	method: "POST",
	url: "/front/user/refresh_token",
     params: {
		refreshtoken: store.token.refresh_token,
     },
	}).finally(() => {
        isRefreshing = false
    })
	return promiseRT
}

```

