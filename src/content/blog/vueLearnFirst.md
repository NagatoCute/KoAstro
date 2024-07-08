---
title: 'vue基础学习'
description: '以一个blog的形式作为例子'
pubDate: 'Jul 8 2024'
heroImage: '/vuelogo.png'
pinned: true
notCompleted: false
---
## 想法
感觉和Astro其实差不太多
开始的时候因为一些和想法上的区别感觉难以忍受
但是后来一想共同点还是很多的
总之不太难,就是,,麻烦

## 配置环境

创建项目：
```bash

D:\vue3test>npm init vue@latest
Need to install the following packages:
create-vue@3.10.4
Ok to proceed? (y) y

Vue.js - The Progressive JavaScript Framework

√ 请输入项目名称： ... vueTutorial
√ 请输入包名称： ... vuetutorial
√ 是否使用 TypeScript 语法？ ... 否 / 是
√ 是否启用 JSX 支持？ ... 否 / 是
√ 是否引入 Vue Router 进行单页面应用开发？ ... 否 / 是
√ 是否引入 Pinia 用于状态管理？ ... 否 / 是
√ 是否引入 Vitest 用于单元测试？ ... 否 / 是
√ 是否要引入一款端到端（End to End）测试工具？ » 不需要
√ 是否引入 ESLint 用于代码质量检测？ ... 否 / 是   y
√ 是否引入 Prettier 用于代码格式化？ ... 否 / 是   y
√ 是否引入 Vue DevTools 7 扩展用于调试? (试验阶段) ... 否 / 是

正在初始化项目 D:\vue3test\vueTutorial...

项目初始化完成，可执行以下命令：

  cd vueTutorial
  npm install
  npm run format
  npm run dev
```

之后：
`npm install`

运行：
`yarn dev`


## 实操
删掉`compoments`下面的全部文件

App.vue改为
```vue
<script setup>

</script>

<template>

</template>

<style scoped>

</style>


```

## 上手
```vue
<script setup>
import { computed, ref } from 'vue';

// 使用 `ref` 创建响应式引用类型
const blogs = ref([/*...*/]);

// 使用 `computed` 创建一个基于 `blogs` 数组长度的计算属性
const total = computed(() => blogs.value.length);
const showTotal = ref(true);

// 创建一个初始表单数据对象
const initialBlogForm = {
  title: '',
  content: '',
  link: ''
};

// 使用 `ref` 创建一个表单数据的响应式引用，通过扩展运算符 `...` 复制 `initialBlogForm` 的属性
const blogForm = ref({ ...initialBlogForm });

// 添加博客条目的函数
function addPost() {
  // 向 `blogs` 数组添加新条目
  blogs.value.push({
    id: blogs.value.length + 1,
    title: blogForm.value.title,
    content: blogForm.value.content,
    link: blogForm.value.link
  });
}

// 模板部分
</script>

<template>
  <!-- 使用 `v-for` 循环遍历 `blogs` 数组，渲染博客列表 -->
  <div v-for="blog in blogs" :key="blog.id">
    <!--    :代表会自动刷新-->
    <h1><a :href="blog.link">{{ blog.title }}</a></h1>
    <article>
      <div>{{ blog.content.slice(0, 100) }}</div>
      <!-- 使用 `v-if` 控制 "Read More" 按钮的显示，仅当博客内容超过100个字符时显示 -->
      <footer v-if="blog.content.length > 100">
        <button>Read More</button>
      </footer>
    </article>
  </div>

  <!-- 使用 `v-if` 控制总文章数的显示 -->
  <h3 v-if="showTotal">共 {{ total }} 篇文章</h3>
  <!-- 用于切换显示总数的按钮 -->
  <button @click="showTotal = !showTotal">{{ showTotal ? '隐藏' : '显示' }}总数</button>

  <!-- 创建表单，使用 `v-model` 实现双向数据绑定 -->
  <form @submit.prevent="addPost">
    <!--    ，@submit.prevent 是一种事件监听器的语法糖，用于在表单提交时阻止默认的提交行为。-->
    <label for="blogTitle">博客标题</label>
    <input type="text" id="blogTitle" v-model="blogForm.title">
    <label for="blogContent">博客内容</label>
    <textarea id="blogContent" cols="30" rows="10" v-model="blogForm.content"></textarea>
    <label for="link">链接</label>
    <input type="text" id="link" v-model="blogForm.link">
    <button type="submit">提交</button>
  </form>
</template>


<style scoped>
  form{
    display: grid;
    margin-top: 2rem;
  }
</style>
```
## 分离组件

BlogPost.vue
```vue
<template>
  <!-- 组件模板 -->
  <div>
    <h1>
      <a :href="link" @click.prevent="() => $emit('titleClick',title)">
        {{ title }}
      </a>
      <!-- 动态绑定链接和标题 -->
    </h1>
    <article>
      <div>
        {{ content.slice(0, 100) }} <!-- 显示前100个字符 -->
      </div>

      <p>阅读量: {{ viewCount }}</p>
      <footer v-if="content.length > 100"> <!-- 如果内容超过100个字符，显示 "Read More" 按钮 -->
        <button>Read More</button>
      </footer>
    </article>

    <slot></slot>
    <!-- slot 可以插入 HTML 内容，在这里对应主组件的 button -->
  </div>
</template>

<script setup>
// 使用 defineProps 定义组件的 props
import { onMounted, ref } from "vue";

const props = defineProps({
  title: String,
  content: String,
  link: String
});

// 使用 defineEmits 定义可以发出的事件
const emit = defineEmits(['titleClick'])

// 定义一个响应式引用，用于存储视图的阅读计数
const viewCount = ref(0);

// onMounted 是 Vue 3 的组合式 API 中的一个生命周期钩子函数
onMounted(() => {
  // 当组件被挂载到 DOM 后，此回调函数会被执行
  // 这里是在组件首次渲染并插入到 DOM 树后执行的代码

  // 使用 setTimeout 来模拟异步操作，比如从服务器获取数据或执行其他延时任务
  setTimeout(() => {
    // 1 秒后，将 viewCount 的值更新为 10000
    // 因为 viewCount 是一个响应式引用，所以这个赋值操作会触发视图的更新
    // 这意味着如果组件中有依赖于 viewCount 的数据绑定，那么这些绑定将会自动更新以反映新的值
    viewCount.value = 10000;
  }, 1000); // 延迟时间单位为毫秒，这里是 1000 毫秒即 1 秒
  // 1s 后修改阅读量为 1w，这里的修改会自动触发视图的更新，因为 viewCount 是响应式的
});
</script>
```
App.vue
```vue
<script setup>
import {computed, ref} from "vue"; // 导入 Vue 的 computed 和 ref

// 导入 BlogPost 组件
import BlogPost from "@/components/BlogPost.vue";

// 使用 ref 定义一个响应式变量 blogs
const blogs = ref([
  {
    id: 1,
    title: 'Vue3基础教程1',
    content: 'Vue3 is a new version of Vue.js',
    link: '/vue-3-tutorial'
  },
  {
    id: 2,
    title: 'Vue3基础教程2',
    content: 'Vue3 is a new version of Vue.js',
    link: '/vue-3-tutorial'
  },
  {
    id: 3,
    title: 'Vue3基础教程3',
    content: 'Vue3 is a new version of Vue.js',
    link: '/vue-3-tutorial'
  }
]);

// 使用 computed 定义一个计算属性 total，表示 blogs 的长度
const total = computed(() => blogs.value.length);

// 使用 ref 定义一个响应式变量 showTotal
const showTotal = ref(true);

// 初始 blog 表单数据
const initialBlogForm = {
  title: '',
  content: '',
  link: ''
};

// 使用 ref 定义一个响应式变量 blogForm，并使用拓展运算符 {...} 创建新对象
const blogForm = ref({...initialBlogForm});

// 添加新博客的函数
function addPost() {
  blogs.value.push({
    id: blogs.value.length + 1,
    title: blogForm.value.title,
    content: blogForm.value.content,
    link: blogForm.value.link
  });
  // 重置表单
  blogForm.value = {...initialBlogForm};
}

// 添加新的点击处理函数 handletitleClick
function handletitleClick(title) {
  console.log(title)
}
</script>

<template>
  <!-- 使用 BlogPost 组件渲染每个博客 -->
  <BlogPost
      @titleClick="handletitleClick"
  v-for="blog in blogs"
  :key="blog.id"
  v-bind="blog"
  >
    <!-- v-bind 用于绑定对象的所有属性 -->
  <!-- 监听 titleClick 事件 -->
  <button>这里对应slot</button> <!-- 插槽内容 -->
  </BlogPost>

  <!-- 显示文章总数 -->
  <h3 v-if="showTotal">共 {{ total }} 篇文章</h3>

  <!-- 切换显示总数的按钮 -->
  <button @click="showTotal = !showTotal">{{ showTotal ? '隐藏' : '显示' }} 总数</button>

  <!-- 表单提交，@submit.prevent 用于阻止默认表单提交行为 -->
  <form @submit.prevent="addPost">
    <label for="blogTitle">blog标题 </label>
    <input type="text" id="blogTitle" v-model="blogForm.title"> <!-- v-model 双向绑定输入值 -->

    <label for="blogContent">blog内容 </label>
    <textarea
        id="blogContent"
        cols="30"
        rows="10"
        v-model="blogForm.content"
    ></textarea>

    <label for="link">链接</label>
    <input type="text" id="link" v-model="blogForm.link"> <!-- v-model 双向绑定输入值 -->

    <button type="submit">提交</button>
  </form>
</template>

<style scoped>
/* scoped 表示样式仅应用于当前组件 */
form {
  display: grid;
  margin-top: 2rem;
}
</style>

```

## 一些杂项
### 关于defineEmits(['titleClick'])和const emit = defineEmits(['titleClick'])
在 Vue 3 的 `<script setup>` 语法中，`defineProps` 和 `defineEmits` 的返回值是可选的，但在某些情况下，使用返回值可能更清晰，特别是当需要在代码中直接引用这些返回值时。让我们详细解释一下。

### 使用 `const props = defineProps()` 和 `const emit = defineEmits()` 的好处：

1. **清晰性和可读性**：
    - 当你使用 `const props = defineProps()`，你明确地告诉读者这是组件的属性对象，它将被用于访问传入的属性。
    - 使用 `const emit = defineEmits()`，你明确地定义了一个变量 `emit`，它可以在代码的其他地方方便地调用来发出事件。这使得代码更加自解释和易读。

2. **代码复用和灵活性**：
    - 当你需要多次访问 `props` 或 `emit` 时，使用返回值会更方便。例如，如果你在多个函数中需要发出相同的事件，使用 `emit` 变量比直接调用 `defineEmits()` 更直观和简洁。

3. **一致性**：
    - 如果你的项目中有多个开发者参与，采用这种明确的写法可以减少理解和维护代码的难度。

### 为什么可以直接使用 `defineEmits([])`：

如果你只需要在事件发出时调用 `defineEmits()`，而不需要在其他地方引用它，直接调用 `defineEmits([])` 是完全可以的。这种用法适用于简单的场景，比如只在模板中使用事件发出。

### 示例代码：

#### 使用返回值：

```vue
<script setup>
// 使用 defineProps 定义组件的 props，并存储在 props 变量中
const props = defineProps({
  title: String,
  content: String,
  link: String
});

// 使用 defineEmits 定义可以发出的事件，并存储在 emit 变量中
const emit = defineEmits(['titleClick']);

// 示例函数，发出 titleClick 事件
function handleClick() {
  emit('titleClick', props.title);
}
</script>
```

#### 不使用返回值：

```vue
<script setup>
// 使用 defineProps 定义组件的 props
defineProps({
  title: String,
  content: String,
  link: String
});

// 直接使用 defineEmits 定义可以发出的事件
defineEmits(['titleClick']);
</script>
```

在这种情况下，如果你需要在模板中发出事件，你可以这样做：

```vue
<template>
  <div @click="$emit('titleClick', title)">
    <!-- 其他内容 -->
  </div>
</template>
```

### 总结

使用 `const props = defineProps()` 和 `const emit = defineEmits()` 的方法更适合复杂的组件或项目，因为它提供了更高的可读性和灵活性。而对于简单的组件，直接调用 `defineProps()` 和 `defineEmits()` 也完全可以。选择哪种方式取决于你的具体需求和代码风格偏好。