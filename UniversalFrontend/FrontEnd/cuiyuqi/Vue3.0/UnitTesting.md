###  1.什么是单元测试

> 是指对软件中的最小可测试单元进行检查和验证
>
> 单元就是人为规定的最小的被测功能模块
>
> 单元测试是在软件开发过程中要进行的最低级别的测试活动，软件的独立单元将在与程序的其他部分相隔离的情况下进行测试

### 2.前端代码都在浏览器里，如何做单元测试

> \* 对于 Javascript 来讲，当然是可以进行单元测试的，并且也通常是针对函数、模块、对象进行测试
>
> \* 前端单元测试狂阶也有不少，比如 `QUnit`、`Sinon`、`Mocha` 等等，单元测试的执行环境可以是我们日常使用的浏览器 `ie`、`Chrome` 等，也可以是无界面浏览器比如 `PhantomJS`、`Headless Chrome`
>
> ```
> * 测试管理工具：`是用来组织和运行整个测试的工具，它能够将测试框架、断言库、测试浏览器、测试代码和被测试代码组织起来，并运行被测试代码进行测试。我们经常使用`Karma
> * `断言库：提供了用于描述你的具体测试的 API，有了它们你的测试代码便能简单直接，也更为语义化，理想状态下你甚至可以让非开发人员来撰写单元测试。我们使用`sinon-chai
> * 可选工具包括
> 测试浏览器 ：`测试代码所执行的浏览器环境。我们使用 `PhantomJS` 或者`Headless Chrom
> ```
>
> 测试覆盖率统计工具
>
> 我们使用和 `Karma` 配套的`Karma-coverage`

### 3.怎么做

1.安装

```
npm i -g @vue/cli-init
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.创建项目

```
vue init webpack project-name
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在这个过程中，你可能会遇到几个提示。大多数提示比较简单易懂，你可以直接选择默认选项。需要注意的是，我们需要是否安装 `vue-router`、`Karma`、`Mocha`的提示后输入YES来引入这些工具。

![img](https://img-blog.csdnimg.cn/20210716150713816.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 3.进入文件

```
cd project-name
npm install
npm run dev
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.依赖

Webpack (2.3) 是一个打包器，它可以合并打包JavaScript，CSS，HTML文件，并且提供给应用运行。Bable (v6.22) 是一个编译器，用来把ES6编译成ES5。目前有很多 JavaScript 标准在许多浏览器中还没有被支持，所以需要将ES6转成ES。

### 5.测试依赖

Karma (v1.4) 是一个运行时，它产生一个 Web 服务环境来运行项目代码，并且执行测试。Mocha (v3.2) 是一个 JavaScript 测试框架。Chai (v3.5) 是一个 Mocha 可以使用的断言库。

在你的项目中，你可以找到下面这些目录：`build`、`config`、`node_modules`、`src`、`static` 和 `test`。对于本教程来说最重要的是`src`，它包括我们应用的代码，用来测试。

**第一次测试**

> 在 `src/components` 里创建一个新文件叫做 `List.vue` 并且将下面代码写进去。

```
    <template>
      <div>
        <h1>My To Do List</h1>
        </br>
        <!--displays list -->
        <ul>
          <li v-for="item in listItems">{{ item }}</li>
        </ul>
      </div>
    </template>

    <script>
    export default {
      name: 'list',
      data () {
        return {
          listItems: ['buy food', 'play games', 'sleep'],
        }
      }
    }
    </script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  我们可以创建一个新的路由来展示这个组件，`src/router/index.js`中创建一个路由，添加完了代码应该是下面这样的：

```
import Vue from 'vue'
import Router from 'vue-router'
import HelloWorld from '@/components/HelloWorld'
import List from '../components/List.vue'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    },
    {
      path: '/list',
      name: 'List',
      component: List
    }
  ]
})
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  访问我们写的这个组件http://localhost:8080/#/List

   首先，我们要测试的是数据的正确性。在`test/unit/specs`目录下创建一个`List.spec.js`，并且写入下面的代码：

```
import List from '@/components/List';
import Vue from 'vue';

describe('List.vue', () => {

  it('displays items from the list', () => {
      // our test goes here
  })
})
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 在这个文件中，我们*describing*了`List.vue`组件，并且我们创建了一个空的测试，他将要检查这个组件的列表展示。这是一个基本的 Mocha 测试文件。

我们首先要安装我们的Vue组件。复制下面代码放在测试文件的'our test goes here'下面： 

```
  // build component
    const Constructor = Vue.extend(List);
    const ListComponent = new Constructor().$mount();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 我们继承了Vue组件并且安装这个
>
> 组件
>
> 安装组件很重要，只有这样我们才能将通过模板来渲染HTML。
>
> 也就是说，HTML已经被创建，并且我们模板中的变量（比如 `item`）已经被填充内容，这样我们就可以获取HTML了（使用`$el`）。
>
> 我们的组件准备好了，我们可以写第一个断言。在这个例子中，我们使用Chai 断言库提供的 'expect' 模式，还有 'should' 和 'assert'模式。将下面的代码放到，启动组件的后面。
>
> ```
>    // assert that component text contains items from the list
>     expect(ListComponent.$el.textContent).to.contain('play games');
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 之前提到过，我们可以使用`ListComponent.$el`来获取组件的HTML，如果想去获取HTML内的内容（比如 文本），我们可以使用`ListComponent.$el.textContent`。这个断言用来检查HTML列表中的文本是否和组件的data里的数据列表吻合。 
>
> 为了检查所有的事情都符合我们的预期，我们可以运行测试！通过 vue-cli 创建的项目，我们可以简单的使用`npm run unit`来运行`cross-env BABEL_ENV=test karma start test/unit/karma.conf.js --single-run`。
>
> ```
>     npm run unit
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](https://img-blog.csdnimg.cn/20210719180909275.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  如果测试都通过了，将会有一个绿色的列表来显示测试报告，让你了解测试都覆盖了哪些代码。

###  **模拟用户输入**

> 下一步我们要做到是添加新的项目到to-do list中
>
> 我们创建了一个input框来输入内容，然后创建一个button用来提交内容。下面是更新后的 List.vue：

```
<template>
  <div>
    <h1>My To Do List</h1>
    <br />
    <input type="text" v-model="newItem" />
    <button @click="addItemToList">Add</button>
    <ul>
      <li v-for="item in listItems" :key="item">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "list",
  data() {
    return {
      listItems: ["buy food", "play games", "sleep"],
      newItem: "",
    };
  },
  methods: {
    addItemToList() {
      this.listItems.push(this.newItem);
      this.newItem = "";
    },
  },
};
</script>

<style>
</style>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 使用`v-model`，输入框里面的内容将和newItem进行双向绑定。当按钮被点击后，执行`addItemToList`，将`newItem`添加到to-do list数组里面，并且清空`newItem`里面的内容，新的项目将会被添加到列表中。
>
> 可以为新功能写测试文件了，创建`List.spec.js`，并且添加以下测试代码。



```
  it('adds a new item to list on click', () => {
        // our test goes here
    })
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 第一步，我们需要创建我们的组件，并且模拟一个用户在输入框的输入行为。因为 VueJs 将输入框和 `newItem` 变量进行了绑定，我们可以给`newItem`设置内容。

```
  // build component
    const Constructor = Vue.extend(List);
    const ListComponent = new Constructor().$mount();

    // set value of new item
    ListComponent.newItem = 'brush my teeth';
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  下一步，我们需要点击按钮。我们需要在HTML中找到按钮，在`$el`中即可找到。这是，我们可以使用`querySelector`，像选择真是元素一样选择这个按钮。也可以使用class(`.buttonClass`)、ID（`#buttonID`）或者标签名(`button`)来选择。

```
// find button
    const button = ListComponent.$el.querySelector('button');
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  为了模拟点击，我们需要给按钮一个新的事件对象。在测试环境中，List组件不会监听任何事件，因此我们需要手动运行`watcher`。

```
// simulate click event
    const clickEvent = new window.Event('click');
    button.dispatchEvent(clickEvent);
    ListComponent._watcher.run();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  最后，我们需要检查我们添加的新项目是否显示在HTML中，这个在前面已经介绍过。我们也需要检查`newItem`是否被存储在了数组里面。

```
   //assert list contains new item
    expect(ListComponent.$el.textContent).to.contain('brush my teeth');
    expect(ListComponent.listItems).to.contain('brush my teeth');
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 整个测试的内容

```
    import List from '@/components/List';
    import Vue from 'vue';

    describe('List.vue', () => {
      it('displays items from the list', () => {
        const Constructor = Vue.extend(List);
        const ListComponent = new Constructor().$mount();
        expect(ListComponent.$el.textContent).to.contain('play games');
      })

      it('adds a new item to list on click', () => {
        // build component
        const Constructor = Vue.extend(List);
        const ListComponent = new Constructor().$mount();

        // set input value
        ListComponent.newItem = 'brush my teeth';

        // simulate click event
        const button = ListComponent.$el.querySelector('button');
        const clickEvent = new window.Event('click');
        button.dispatchEvent(clickEvent);
        ListComponent._watcher.run();

        // assert list contains new item
        expect(ListComponent.$el.textContent).to.contain('brush my teeth');
        expect(ListComponent.listItems).to.contain('brush my teeth');
      })
    })
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 现在跑一次这个测试，应该全是绿色的。

![img](https://img-blog.csdnimg.cn/20210720102156858.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 有一个VueJS实用程序库，它将一些复杂的代码进行了封装。如果想使用它，可以在项目的根目录下输入以下命令安装 

```
    npm install avoriaz
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 下面这个测试实际上和上面测试相同，只不过写法上有些不同。我们使用了`mount()`法来安装Vue组件，使用`find()`获取按钮，使用`dispatch()`来触发点击。

```
 import { mount } from 'avoriaz';
    import List from '@/components/List';
    import Vue from 'vue';

    describe('List.vue', () => {
      // previous tests ..

      it('adds new item to list on click with avoriaz', () => {
           // build component
        const ListComponent = mount(List);

        // set input value
        ListComponent.setData({
          newItem: 'brush my teeth',
        });

        // simulate click event
        const button = ListComponent.find('button')[0];
        button.dispatch('click');

        // assert list contains new item
        expect(ListComponent.text()).to.contain('brush my teeth');
        expect(ListComponent.data().listItems).to.contain('brush my teeth');
      })
    })
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)