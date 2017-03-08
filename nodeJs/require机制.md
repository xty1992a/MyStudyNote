#require机制

##一个有趣的小问题

```
// a.js
exports.x = 'a1';
console.log('a.js ', require('./b.js').x);
exports.x = 'a2';

// b.js
exports.x = 'b1';
console.log('b.js ', require('./a.js').x);
exports.x = 'b2';

// main.js
console.log('main.js ', require('./a.js').x);
console.log('main.js ', require('./b.js').x);

```

以上三段代码分属不同的js文件,运行main.js得到的结果如下

```
$ node main.js
b.js  a1
a.js  b2
main.js  a2
main.js  b2
```

首先明确两点:
1. require()函数的本质是把相应的文件运行一次,然后将运行后的结果作为对象缓存到内存中,下次调用都是调用缓存中的对象;
2. js在执行代码之前,有一个预处理的过程,预处理没有完成,代码不会执行.require()函数会被预处理;

**推论**
1. 加载main.js,将main.js放入栈底,开始初始化两个函数,引入两个模块;
2. 初始化到`require('./a.js').x`;加载a.js,将a.js放入栈;
3. 初始化a.js,a的module.exports暴露,并加载了一个属性x,值为'a1';
4. 再次遇到require('./b.js').x,暂停a.js的初始化工作,加载b.js,将b.js放在栈顶;
5. 初始化b.js,b的module.exports暴露,并加载属性x,值为'b1';
6. 初始化到`require('./a.js').x`,由于此时缓存中已有a的module.exports对象,并且取得了x的值,为a1;继续初始化,重置exports的x属性,将其置为'B2';
7. 执行栈顶的b.js,打印b.js  a1;
8. 














