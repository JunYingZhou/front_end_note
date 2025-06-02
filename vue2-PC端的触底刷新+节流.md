# vue2-PC端的触底刷新+节流

## 一、浏览器的scroll事件

```js
window.addEventListener('scroll', func, true)
```

我们可以在vue的生命周期中，对浏览器的scroll事件进行监听，然后在函数中对我们的盒子高度进行判断等操作。

```js
mounted() {
    window.addEventListener('scroll', func, true)
 },
```

## 二、高度的判断

在原生的vue2和浏览器中没有像小程序那样的钩子可以自动进行触底刷新的操作onReachBottom()，但是我们可以通过对dom属性的获取，从而进行高度的计算。

### 2.1 通过dom的参数进行高度属性的获取

```vue
<template>
  <div class="scroll-container" @scroll="handleScroll">
    <!-- 列表内容 -->
    <ul>
      <li v-for="(item, index) in items" :key="index">
        {{ item }}
      </li>
    </ul>
    <!-- 加载提示 -->
    <div v-if="isLoading" class="loading">加载中...</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [], // 列表数据
      isLoading: false, // 是否在加载中
      hasMore: true, // 是否有更多数据
      page: 1 // 当前分页页码
    };
  },
  mounted() {
    this.loadMore(); // 初次加载数据
  },
  methods: {
    // 监听滚动事件
    handleScroll(event) {
      const scrollTop = event.target.scrollTop;
      const clientHeight = event.target.clientHeight;
      const scrollHeight = event.target.scrollHeight;

      // 判断是否滚动到底部
      if (scrollTop + clientHeight >= scrollHeight - 10) {
        this.loadMore();
      }
    },
    // 加载更多数据
    loadMore() {
      if (this.isLoading || !this.hasMore) return;

      this.isLoading = true;
      setTimeout(() => {
        // 模拟获取新数据
        const newItems = Array.from({ length: 10 }, (_, i) => `Item ${i + (this.page - 1) * 10}`);
        this.items = [...this.items, ...newItems];

        // 假设总页数为3，之后不再加载
        if (this.page >= 3) {
          this.hasMore = false;
        } else {
          this.page++;
        }

        this.isLoading = false;
      }, 1000);
    }
  }
};
</script>

<style scoped>
.scroll-container {
  height: 400px;
  overflow-y: auto;
  border: 1px solid #ccc;
}
.loading {
  text-align: center;
  padding: 10px;
}
</style>

```

通过vue的@scorll()方法，传递该dom元素的属性进行操作

```js
handleScroll(event) {
   const scrollTop = event.target.scrollTop; // 获取当前滚动条滚动的高度。
   const clientHeight = event.target.clientHeight; // 可视区域的高度。
   const scrollHeight = event.target.scrollHeight; // 内容的总高度。

   // 判断是否滚动到底部
    if (scrollTop + clientHeight >= scrollHeight - 10) 		{
       this.loadMore(); // 我们可以在此方法当中进行数据请求和分页操作
      }
 },
```

### 2.2 通过ref

```vue
<template>
  <div ref="scrollContainer" class="scroll-container">
    <!-- 列表内容 -->
    <ul>
      <li v-for="(item, index) in items" :key="index">
        {{ item }}
      </li>
    </ul>
    <!-- 加载提示 -->
    <div v-if="isLoading" class="loading">加载中...</div>
  </div>
</template>

<script>
import throttle from 'lodash/throttle'; // 使用 lodash 的 throttle 函数

export default {
  data() {
    return {
      items: [], // 列表数据
      isLoading: false, // 是否在加载中
      hasMore: true, // 是否有更多数据
      page: 1 // 当前分页页码
    };
  },
  mounted() {
    this.loadMore(); // 初次加载数据

    // 监听滚动事件并加上节流
    this.$refs.scrollContainer.addEventListener(
      'scroll',
      throttle(this.handleScroll, 200) // 每 200ms 触发一次
    );
  },
  beforeDestroy() {
    // 移除滚动事件监听
    this.$refs.scrollContainer.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    // 监听滚动事件
    handleScroll() {
      const container = this.$refs.scrollContainer;
      const scrollTop = container.scrollTop;
      const clientHeight = container.clientHeight;
      const scrollHeight = container.scrollHeight;

      // 判断是否滚动到底部
      if (scrollTop + clientHeight >= scrollHeight - 10) {
        this.loadMore();
      }
    },
    // 加载更多数据
    loadMore() {
  	}
};
</script>

<style scoped>
.scroll-container {
  height: 400px;
  overflow-y: auto;
  border: 1px solid #ccc;
}
.loading {
  text-align: center;
  padding: 10px;
}
</style>

```

## 三、节流操作（throttle）

在 Vue 2 中使用 `ref` 和节流（throttle）可以提高滚动事件的性能。节流是防止滚动事件频繁触发的有效方法，尤其是在处理触底刷新时。我们可以使用 Lodash 的 `throttle` 函数，或者手动实现一个简单的节流函数。

### 3.1 什么是节流

**节流（throttle）** 是一种优化技术，用于控制高频率触发的事件（如滚动、窗口调整大小、输入等）执行的频率。它的主要目的是在一定的时间间隔内，限制函数的执行次数，避免资源消耗过高。

原理：当高频事件持续触发时，节流会在规定的时间间隔内只允许执行一次函数，忽略其余时间段内的触发。例如，设定时间间隔为 200ms，则即使用户频繁触发事件，函数也只会每 200ms 执行一次。

节流的实现：

1. Lodash

```js
import throttle from 'lodash/throttle';

function handleScroll() {
  console.log('滚动事件触发');
}

// 每 200ms 执行一次 handleScroll
window.addEventListener('scroll', throttle(handleScroll, 200));

```

2. 定时器

   ```js
   function throttle(func, wait) {
     let lastTime = 0;
     return function (...args) {
       const now = Date.now();
       if (now - lastTime >= wait) {
         lastTime = now;
         func.apply(this, args);
       }
     };
   }
   
   // 使用节流函数
   function handleResize() {
     console.log('窗口调整');
   }
   
   // 每 200ms 执行一次 handleResize
   window.addEventListener('resize', throttle(handleResize, 200));
   3.2 触底刷新+节流
   ```

### 3.2 触底刷新+节流

```vue
<template>
  <div ref="scrollContainer" class="scroll-container">
    <!-- 列表内容 -->
    <ul>
      <li v-for="(item, index) in items" :key="index">
        {{ item }}
      </li>
    </ul>
    <!-- 加载提示 -->
    <div v-if="isLoading" class="loading">加载中...</div>
  </div>
</template>

<script>
import throttle from 'lodash/throttle'; // 使用 lodash 的 throttle 函数

export default {
  data() {
    return {
      items: [], // 列表数据
      isLoading: false, // 是否在加载中
      hasMore: true, // 是否有更多数据
      page: 1 // 当前分页页码
    };
  },
  mounted() {
    this.loadMore(); // 初次加载数据

    // 监听滚动事件并加上节流（500ms 内只能执行一次）
    this.$refs.scrollContainer.addEventListener(
      'scroll',
      throttle(this.handleScroll, 500) // 每 500ms 触发一次
    );
  },
  beforeDestroy() {
    // 移除滚动事件监听
    this.$refs.scrollContainer.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    // 监听滚动事件
    handleScroll() {
      const container = this.$refs.scrollContainer;
      const scrollTop = container.scrollTop;
      const clientHeight = container.clientHeight;
      const scrollHeight = container.scrollHeight;

      // 判断是否滚动到底部
      if (scrollTop + clientHeight >= scrollHeight - 10) {
        this.loadMore();
      }
    },
    // 加载更多数据
    loadMore() {
      if (this.isLoading || !this.hasMore) return;

      this.isLoading = true;
      setTimeout(() => {
        // 模拟获取新数据
        const newItems = Array.from({ length: 10 }, (_, i) => `Item ${i + (this.page - 1) * 10}`);
        this.items = [...this.items, ...newItems];

        // 假设总页数为3，之后不再加载
        if (this.page >= 3) {
          this.hasMore = false;
        } else {
          this.page++;
        }

        this.isLoading = false;
      }, 1000);
    }
  }
};
</script>

<style scoped>
.scroll-container {
  height: 400px;
  overflow-y: auto;
  border: 1px solid #ccc;
}
.loading {
  text-align: center;
  padding: 10px;
}
</style>

```

