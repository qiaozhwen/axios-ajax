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