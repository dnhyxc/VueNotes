[toc]

## Vue概述

[Vue官网](https://cn.vuejs.org/)

#### 1，Vue简介及作用

1.1，Vue是一个渐进式的JavaScript框架。能够动态构建用户界面。

#### 2，Vue的特点

2.1，遵循MVVM模式。

- ![image](https://upload-images.jianshu.io/upload_images/13877849-b4bb9dec8cac3164.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/685/format/webp)

- ![image](https://img2020.cnblogs.com/blog/1675628/202004/1675628-20200402114547507-1864982578.png)

2.2，编码简洁，体积小，运行效率高，适合移动/PC端开发。

2.3，它本身只关注UI，可以轻松引入Vue插件或其它第三方库开发项目。

## Vue模板语法

#### 1，模板的理解

1.1，动态的html页面，包含了一些`JS语法代码`，`双大括号表达式`，`指令（以v-开头的自定义标签属性）`。

#### 2，双大括号表达式

2.1，语法：**{{exp}}**。

2.2，功能：向页面输出数据。

2.3，作用：可以调用对象的方法。

## 指令

#### 1，v-html

1.1，可将数据解析成html标签内容。

#### 2，v-text

2.1，可将数据解析成文本内容。

#### 3，v-bind(强制数据绑定)

3.1，v-bind可以指定变化的属性值。

3.2，v-bind完整写法为：`v-bind:xxx = "yyy"`。

- v-bind语法糖：`:xxx = "yyy"`。

3.3，强制绑定class和style

- 在应用界面中，某些元素的样式是变化的。class和style绑定就是专门用来实现动态样式效果的技术。

- :class = "XXX"用于动态绑定class属性

- ：style = "{ color: activeColor, fontSize: fontSize + "px"}"用于动态绑定color属性和fontSize属性。

    - activeColor与fontSize是data属性。

#### 4.v-on(绑定事件监听)

4.1，v-on可以绑定事件监听。

4.2，v-on完整写法为：`v-on:click = "xxx"`。

- v-on语法糖：`@click = "xxx"`。

## 计算属性与监视属性

#### 1，计算属性理解

1.1，在computed属性对象中定义计算属性的方法。

1.2，在页面中使用{{方法}}来显示计算的结果。

#### 2，监视属性

2.1，通过Vue对象的**$watch()**或**watch**配置来监视指定的属性。

2.2，当属性变化时，回到函数自动调用，在函数内部进行计算。

#### 3，计算属性高级

3.1，通过getter/setter实现对属性数据的显示和监视。

3.2，计算属性存在缓存，多次读取只执行一次getter计算。

#### 4，计算属性之数据绑定DEMO

```
<div id="app">
    姓: <input type="text" v-model="firstName">
    名: <input type="text" v-model="lastName">
    姓名1(单向）: <input type="text" v-model="fullName1">
    姓名2(单向）: <input type="text" v-model="fullName2">
    姓名3(双向）: <input type="text" v-model="fullName3">
</div>

<script>
    const vm = new Vue({
        el:'app',
        data:{
            firstName:'A',
            lastName:'B',
            fullName1:'A B',
            fullName2:'A B'
        },
        computed:{
            firstName1(){
                return this.firstName + this.lastName
            },
            
            fullName3:{
                <!--get为回调函数，当需要读取当前属性值时回调，根据相关的数据计算并返回当前属性的值。-->
                get(){
                    return this.firstName + this.lastName 
                },
                <!--回调函数，监视当前属性值的变化，当属性值发生改变时回调，更新相关的属性数据。-->
                set(value){ // value就是fullName3的最新属性值
                    const names = value.split(' ') // 以空格为分割截取字符串
                    this.firstName = name[0]
                    this.lastName = name[1]
                }
            }
        },
        watch:{
            firstName:function (newValue , oldValue){
                this.fullName1 = newValue + " " + this.lastName
            }
        }
    })
    
    vm.$watch("lastName", (newValue , oldValue) => {
        this.fullName2 = this.firstName + " " + value
    })
</script>
```