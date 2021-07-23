 1.递归监听

> 默认情况下，无论是通过ref还是reactive都是递归监听

```
<template>
  <div>
//验证reactive
    <p>{{ state.a }}</p>
    <p>{{ state.one.one }}</p>
    <p>{{ state.one.two.two }}</p>
    <p>{{ state.one.two.three.three }}</p>
    <button @click="myFn1">Fn1</button>
  </div>
</template> 

<script>
import { reactive } from "vue";
//验证ref
import { reactive } from "vue";

export default {
  name: "App",
  setup() {
    let state = reactive({//reactive 替换掉 ref
      a:'a',
      one:{
        one:'one',
        two:{
          two:'two',
          three:{
            three:'three'
          }
        }
      }
    });
    function myFn1 (){
      state.a='A';//验证ref需要加value 例如  state.value.a='A'
      state.one.one='1';
      state.one.two.two='2';
      state.one.two.three.three='3'
    }
    return{state,myFn1}//记得导处去
  },
};
</script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 2.递归监听存在的问题

> 如果数据多，消耗性能比较大

3.非递归监听 

> 只能监听我们的第一层
>
> reactive 可以通过 shallowReactive
>
> ref 可以通过 shallRef
>
> vue3只提供了 triggerRef的方法，没有提供triggerReactive的方法更新数据

```
<script>
import { shallowReactive } from "vue";
// import { shallowRef } from "vue";
export default {
  name: "App",
  setup() {
    let state = shallowReactive({ //shallRef
      a:'a',
      one:{
        one:'one',
        two:{
          two:'two',
          three:{
            three:'three'
          }
        }
      }
    });
    function myFn1 (){
      // shallRef
      // state.value.a='A';
      // state.value.one.one='1';
      // state.value.one.two.two='2';
      // state.value.one.two.three.three='3'

      //shallowReactive
      // state.a='A';//第一层 不发生改变 下面是不会更新的 ！！！！！！ 如果这层不注释则会更新
      state.one.one='1';
      state.one.two.two='2';
      state.one.two.three.three='3'

       //shallowReactive
      console.log(state);  //Proxy {a: "A", one: {…}} 只有第一层被包装成Proxy了
      console.log(state.one);//{one: "1", two: {…}}
      console.log(state.one.two);//{two: "2", three: {…}}
      console.log( state.one.two.three);//{three: "3"}

      //shallRef
        //注意点:如果是通过shallowRef创建数据，那么vue监听的是，value的变化，并不是第一层的变化
      // console.log(state);  //RefImpl {_rawValue: {…}, _shallow: true, __v_isRef:             true, _value: {…}}
      // console.log(state.value);//{a: "A", one: {…}}
      // console.log(state.value.one.two);//{two: "2", three: {…}}
      // console.log( state.value.one.two.three);//{three: "3"}
    }
    return{state,myFn1}
  },
};
</script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



4.应用场景

> 一般情况下，我们使用ref和reactive即可
>
> 只有在需要监听数据量比较大的时候，我们才使用shallowRef/shallReactive 