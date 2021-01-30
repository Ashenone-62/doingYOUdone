# doingYOUdone
todo类型，

WEB APP，

Vue开发，

练手作品

敏感肌也能用，

用了的都说好，

喜欢给个⭐



## 踩坑

### this指向

用`localStorageSave()`缓存保存来举例说，此处我们使用了箭头函数，但是总所周知箭头函数的特性是会保存外部的this指向，此处`this`的指向为`window`并非实例`Vue`，此处我们需要操作的是`data`里面`todoList`数组。所以解决方法是要么你使用`app.todoList`；要么就传统匿名函数写法`function()`，用`this.todoList`。

```javascript
let app = new Vue({
        //挂载
        el: "#app",
        data: {
            //要做的事情数组
            todoList: [],
        },
        methods: {
            //缓存保存
            localStorageSave: () => {
                //将todoList里的内容转为JSON格式保存在缓存中
                localStorage.todoList = JSON.stringify(app.todoList)
            },
        }
```

### check勾选

代码中勾选选框绑定了一个`click`事件，但是请不要忽略`check`本来有个默认事件（如提交按钮一样会默认发送一个POST请求），所以我们需要使用`Vue`的事件修饰符`.prevent`停掉默认事件，不然会导致，未完成和已完成相同索引值的内容被勾选上，无论你设置没设置唯一标志。

### transition-group的key值

如果你要使用`Vue`的`transition-group`来给列表绑定动画，请一定要配合官方文档食用，不要漏掉这种低级错误，一定要设置`v-for`元素的属性`key`，不然动画无法渲染。

```javascript
<transition-group enter-active-class = "animate__animated animate__bounceInLeft" leave-active-class = "animate__animated animate__bounceOutRight">
             <div class="todoItem" v-for="item,index in doingList" :key = "'doing'+index">
                  <input type="checkbox" @click.prevent = "doneOrNot(item.id)">
                  <div class="todoContent">{{item.content}}</div>
                  <button class="del" @click = "del">删除</button>
             </div>
</transition-group>
```

## 展示

### 主界面

<img src=".\images\1.jpg" alt="1" style="zoom:50%;" />

### 输入代办

<img src=".\images\2.jpg" alt="2" style="zoom:50%;" />

### 添加代办

<img src=".\images\3.jpg" alt="3" style="zoom:50%;" />

### 勾选代办

<img src=".\images\4.jpg" alt="4" style="zoom:50%;" />

### 删除事情

<img src=".\images\5.jpg" alt="5" style="zoom:50%;" />

