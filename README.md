# axios与ajax

> histo

## 安装

``` bash
 axios: npm install axios
 ajax:  JQuery另有封装
```
# 接口规范(axios)
## get
``` bash
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
  // 上面的请求也可以这样做
  axios.get('/user', {
      params: {
        ID: 12345
      }
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
    后端接收：let {ID} = req.request.query
```
``` bash
 前端数据格式:
     {
        字段名:字段值，
        字段名:字段值，
        字段名:字段值，
        ...
     }
demo1:
 get: function (query, cb) {
    axios.get('后台给出接口地址?query=' + JSON.stringify(query)).then(response => {
      cb(response)
    }).catch(function (error) {
      console.log(error)
    })
demo2:
    let request = axios.create({
       baseUrl:'后台给出接口地址'
    })
    request({
       method:'get'//可选，默认为get
       params:'xxxxxx'
    })
```
## post
``` bash
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
  后端接收：let {ID} = req.request.query
  ```
  ``` bash
  前端数据格式:
       {
          字段名:字段值，
          字段名:字段值，
          字段名:字段值，
          ...
       }
  demo1:
   post: function (query, cb) {
      axios.get('后台给出接口地址，query).then(response => {
        cb(response)
      }).catch(function (error) {
        console.log(error)
      })
  demo2:
      let request = axios.create({
         baseUrl:'后台给出接口地址'
      })
      request({
         method:'post'//可选，默认为get
         data:'xxxxxx'
      })
```
## delete
``` bash
axios.delete('/user', 
  data: {
    "id":"a"
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```