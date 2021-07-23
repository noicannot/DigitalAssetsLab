 1.toRaw

> 响应式数据中获取原始数据 

```
<script>
import {reactive,toRaw} from 'vue'
export default {
  name: "App",
  setup() {
    let obj = {name:'cui',age:18};
    /* 
      ref/ractive数据类型的特点:
      每次修改都会被追踪，都会更新ui界面，但这样其实是非常消耗性能的
      所以如果我们有一些操作不需要追踪，不需要ui界面的更新，那么我们就可以通过toRaw方法拿到他的
      原始数据
    **/
    let state = reactive(obj)
    let obj2 = toRaw(state);
    // console.log(obj == obj2);//true
    //state和obj的关系:
    // 引用关系，state的本质是一个proxy对象，在这个对象中引用了obj
    function myFn1 (){
      //如果直接修改obj则无法触发页面更新
      // 只有通过包装后的对象来修改，才会触发界面更新
      obj2.name='cuiyuqi'
      console.log(obj);//{name: "cuiyuqi", age: 18}
      console.log(state);//Proxy {name: "cuiyuqi", age: 18}
    }
    return{obj,state,myFn1}
  },
};
</script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 2.markRaw

```
<script>
import {reactive,markRaw} from 'vue'
export default {
  name: "App",
  setup() {
    let obj = {name:'cui',age:18};
    obj = markRaw (obj)//数据永远不要被追踪 页面就不更新了
    let state = reactive(obj)
    
    function myFn1 (){
      
      state.name='cuiyuqi'
    }
    return{state,myFn1}
  },
};
</script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3.toRef

> toref 和 ref 方法一样都是来创建响应式数据的 

```
<script>
import {ref} from 'vue'
export default {
  name: "App",
  setup() {
    let obj = {name:'cui'};
    /**
     * ref(obj.name)->ref(cui)->reactive({value:cui})
     */
    let state=ref (obj.name)//把name变成响应式数据
    
    function myFn1 (){
      state.value='cuiyuqi'
      console.log(obj);//原数据
      console.log(state);
    }
    return{state,myFn1}
  },
};
</script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 结论:如果利用ref讲某个对象中的属性变成响应式的数据
>
> 我们修改响应式的数据是不会影响原始数据的

```
引入toRef然后
let state = toRef(obj.name); 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> ref和toRef的区别
>
> ref->复制，修改响应式数据不会影响以前的数据
>
> toRef-> 引用，修改响应式数据会影响以前的数据
>
> ref->数据发生改变，界面就会自动更新
>
> toRef->数据发生改变，界面也并不会自动更新
>
> *toRef应用场景：
>
>  如果想让响应数据和以前的数据关联起来，并且更新响应式数据之后还不想更新ui

4.toRefs 

>  多个属性需要变成响应式的用

```
<script>
import { toRefs} from "vue";
export default {
  name: "App",
  setup() {
    let obj = { name: "cui",age:18 };
    let state =toRefs(obj); //把name变成响应式数据

    function myFn1() {
      state.name.value = "cuiyuqi";
      state.age.value = 666
      console.log(obj);
      console.log(state);
    }
    return { state, myFn1 };
  },
};
</script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)