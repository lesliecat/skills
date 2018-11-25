## live-server 简易服务器
```
npm i live-server -g
```
右键文件夹路径打开shell输入    live-server

查看配置 npm config ls

## axios拦截器

```
// http request 拦截器
axios.interceptors.request.use(
    config => {
        if (store.state.token) {  // 判断是否存在token，如果存在的话，则每个http header都加上token
            config.headers.Authorization = `token ${store.state.token}`;
        }
        return config;
    },
    err => {
        return Promise.reject(err);
    });
 
// http response 拦截器
axios.interceptors.response.use(
    response => {
        return response;
    },
    error => {
        if (error.response) {
            switch (error.response.status) {
                case 401:
                    // 返回 401 清除token信息并跳转到登录页面
                    store.commit(types.LOGOUT);
                    router.replace({
                        path: 'login',
                        query: {redirect: router.currentRoute.fullPath}
                    })
            }
        }
        return Promise.reject(error.response.data)   // 返回接口返回的错误信息
    });
```  
## moment 时间格式化
1.先安装moment.js包：npm install moment --save

2.在过滤器的方法体中可以写入如下代码实现日期的格式化：

import moment from 'moment'    

Vue.filter('datefmt',function(input,fmtstring){

    return moment(input).format(fmtstring)

}) 

3.在需要使用这个datefmt过滤器的组件中如何使用呢？

{{item.add_time | datefmt('YYYY-MM-DD HH:mm:ss')}}



实例：main.js文件中
```

import moment from 'moment'
Vue.config.productionTip = false
 
 
//定义一个全局过滤器实现日期格式化
Vue.filter('datafmt',function (input,fmtstring) {
  // 使用momentjs这个日期格式化类库实现日期的格式化功能
  return moment(input).format(fmtstring);
});
.vue组件中{{item.add_time | datefmt('YYYY-MM-DD HH:mm:ss'}}

```
### watch检测对象属性

'msg.name' 使用字符串

immediate属性，刚绑定监测值时酒之行一次


可以监测路由 ,监测路由可以做权限管理
```
watch: {
    $route: {
        handler(nv, ov) {

        }
    }
}
```
 this.$router.push({path: '/', query: {num: 3}})
