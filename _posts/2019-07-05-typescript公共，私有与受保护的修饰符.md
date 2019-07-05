---
layout:     post
title:      typescript 公共，私有与受保护的修饰符
subtitle:   typescript
date:       2019-07-05
author:     Jacob
header-img: img/post-bg-keybord.jpg
catalog: true
tags:

    - typescript
---

# typescript 公共，私有与受保护的修饰符

## public理解

当你在程序中没有指明修饰符时，默认为public，也就是在类内类外都可以访问，我们以下面的例子来解释。

```typescript
class Person{
    name:string
    sex:string
    age:number // 默认设置为public
    constructor(name:string, sex:string, age:number){
        this.name = name
        this.sex = sex
        this.age = age
    }
    show_name():void{
        console.log('类内函数输出的：', this.name)
    }
}

let lcs = new Person('lcs', 'man', 21)

console.log('类外输出的：', lcs.name)
lcs.show_name()
```



![image-20190705141015777](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/image-20190705141015777.png?raw=true)

## private理解

在类内定义这个变量时，我们可以定义为private，他就不可以在类外进行访问，例子如下：

```typescript
class Person{
    private name:string // 这里将name改为了private
    sex:string
    age:number
    constructor(name:string, sex:string, age:number){
        this.name = name
        this.sex = sex
        this.age = age
    }
    show_name():void{
        console.log('类内函数输出的：', this.name)
    }
}

class Teacher extends Person{
    salary: number
    constructor(name:string, sex:string,  age:number,salary:number){
        super(name,sex,age)
        this.salary = salary
    }
    show():void{
        console.log('继承类内输出的：', this.name, this.salary.toString())
    }
}

let lcs = new Person('lcs', 'man', 21)
let t = new Teacher('lcs', 'man',21,31232)
t.show()
console.log('类外输出的：', lcs.name)
lcs.show_name()
```

在编译的时候编译器报错

![image-20190705142913114](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/image-20190705142913114.png?raw=true)

编译器指出，name变量时private，只能在类Person内使用，在**继承类**和**类外**都是可以访问的，但是这个时候在浏览器内还是可以正常运行的，报错的目的是为了让你规范代码

![image-20190705142927316](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/image-20190705142927316.png?raw=true)

## protected理解

定义为protected之后的变量只能在类内和继承类内进行访问，在类外访问就会报错

```typescript
class Person{
    protected name:string // 将name改为protected
    sex:string
    age:number
    constructor(name:string, sex:string, age:number){
        this.name = name
        this.sex = sex
        this.age = age
    }
    show_name():void{
        console.log('类内函数输出的：', this.name)
    }
}

class Teacher extends Person{
    salary: number
    constructor(name:string, sex:string,  age:number,salary:number){
        super(name,sex,age)
        this.salary = salary
    }
    show():void{
        console.log('继承类内输出的：', this.name, this.salary.toString())
    }
}

let lcs = new Person('lcs', 'man', 21)
let t = new Teacher('lcs', 'man',21,31232)
t.show()
console.log('类外输出的：', lcs.name)
lcs.show_name()
```

编译器报错如下

![image-20190705143216822](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/image-20190705143216822.png?raw=true)

同样，在浏览器还是可以正常运行的

![image-20190705142927316](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/image-20190705142927316.png?raw=true)

