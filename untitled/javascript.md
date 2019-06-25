# JavaScript



### 异步和同步、阻塞和非阻塞、并行和并发、事件驱动

* [事件](https://luminousmen.com/post/asynchronous-programming-blocking-and-non-blocking)
* [EventLoop](https://zhuanlan.zhihu.com/p/41543963)

### defineProperty\(get和set的双向绑定实现\)

```text
var $watch=function(myObject,callback){
    initWatch(myObject);
    function initWatch(obj){
        for(var i in obj){
            if(typeof obj!='object'){
                return;
            }
            (function(value,o,attr){
                var v=value;
                var oldValue=value;
                Object.defineProperty(o,attr,{
                    get:function(){
                        return v;
                    },
                    set:function (newValue){
                        oldValue=v;
                        v=newValue;
                        callback(newValue,oldValue)
                    }
                });
            })(obj[i],obj,i);
            initWatch(obj[i]);
        }
    }
};
var a = {
　　count:'1',
　　count2:{
　　　　count2_1:'2_1',
　　　　count2_2:'2_2'
　　}
}
Object.prototype.setValue = function(key,value){//设置新Key数据
    this[key] = value;
    $watch(this,function(newValue,oldValue){
        console.log('旧数据~'+oldValue+'    '+'新数据~'+newValue);
    })
}
$watch(a,function(newValue,oldValue){
    console.log('旧数据'+oldValue+'    '+'新数据'+newValue);
})
```



### ow JS类型检查

* [ow](https://github.com/sindresorhus/ow)
* JavaScript 语言没有类型检查，运行时无法知道函数的参数是否为指定的类型。这个库就用来检查函数参数的类型，如果不符合要求就抛错。

## 其他

* [ES6](http://es6.ruanyifeng.com/)
* [React](https://reactjs.org/)
* [React-native](https://facebook.github.io/react-native/)
* [Vue](https://cn.vuejs.org/)
* [Canvas](https://github.com/supperjet/H5-Animation)
* [鲜为人知的JS](https://www.infoq.cn/article/QMteVFAMMeBpDhWE-m01)
* [Prettier](https://www.infoq.cn/article/IzAMXQtkJv3N0rXX_G6a)
* [模块化加载详解](https://github.com/ljianshu/Blog/issues/48)
* [PWA实践](https://www.w3cplus.com/pwa/your-first-pwapp.html)
* [MPVUE](http://mpvue.com/mpvue/simple/)
* [React国外视频教程](https://scrimba.com/g/glearnreact)
* [Facebook 技术栈](https://opensource.fb.com/)
* [expo](https://docs.expo.io/versions/v32.0.0/)
* [WebAssembly](https://www.ibm.com/developerworks/cn/web/wa-lo-webassembly-status-and-reality/index.html)
* [Ant design](https://ant.design/index-cn)

