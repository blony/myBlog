# Vue中this使用的注意事项

## 一、 axios中this的指向问题
在vue中使用axios做网络请求的时候，会遇到this不指向vue，而为undefined。
### 解决方法
#### 1. 使用箭头函数 "=>"
 "=>" 内部的this是词法作用域，由上下文确定（也就是由外层调用者vue来确定）。
``` javascript
methods: {
      loginAction(formName) {
        this.$axios.post("……")
          .then(function(response){
               console.log(this); //这里 this = undefined
          })
          .catch((error)=> {
              console.log(this); //箭头函数"=>"使this指向vue
          });

        });
      }
}
```
#### 2. 使用hack写法
定义变量绑定this至vue对象。
```javascript
methods: {
      loginAction(formName) {
        let _this = this;
        this.$axios.post("……")
          .then(function(response){
               console.log(_this); //这里 _this 指向 vue
          })
        });
      }
}
```
