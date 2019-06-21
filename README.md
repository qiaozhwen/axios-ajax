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
    后端接收：let {ID} = req.request.query['query']
demo2:
    let request = axios.create({
       baseUrl:'后台给出接口地址'
    })
    request({
       method:'get'//可选，默认为get
       params:'xxxxxx'
    })
    后端接收：let {ID} = req.request.query****
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
      后端接收：let {ID} = req.request.query
  demo2:
      let request = axios.create({
         baseUrl:'后台给出接口地址'
      })
      request({
         method:'post'//可选，默认为get
         data:'xxxxxx'
      })
      后端接收：let {ID} = req.request.query
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
 ``` bash
  前端数据格式:
       {
          字段名(ID):字段值，
       }
  demo1:
   delete: function (query, cb) {
      axios.get('后台给出接口地址，query).then(response => {
        cb(response)
      }).catch(function (error) {
        console.log(error)
      })
      后端接收：let {ID} = req.request.body
  demo2:
      let request = axios.create({
         baseUrl:'后台给出接口地址'
      })
      request({
         method:'post'//可选，默认为get
         data:{id:'xxxxxxxxxxx'}
      })
     后端接收：let {ID} = req.request.body
```
# 接口规范(ajax)
## post
```bash
$.ajax({
    type: "post",
    url:后台给出接口地址,
    data: JSON.stringify(需要包裹的数据),
    contentType : 'application/json',
    success: function (res) {
        console.log(res)
    },
    error:function(err){
        console.log(err)
    }
});
```
##get
```bash
$.ajax({
    type: "get",
    url:后台给出接口地址,
    contentType : 'application/json',
    data: JSON.stringify(需要包裹的数据),
    success: function (res) {
        console.log(res)
    },
    error:function(err){
        console.log(err)
    }
});
```
##参数名及意义
```bash
1.url:

要求为String类型的参数，（默认为当前页地址）发送请求的地址。

2.type: 
要求为String类型的参数，请求方式（post或get）默认为get。注意其他http请求方法，例如put和delete也可以使用，但仅部分浏览器支持。

3.timeout: 
要求为Number类型的参数，设置请求超时时间（毫秒）。此设置将覆盖$.ajaxSetup()方法的全局设置。

4.async: 
要求为Boolean类型的参数，默认设置为true，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为false。注意，同步请求将锁住浏览器，用户其他操作必须等待请求完成才可以执行。

5.cache: 
要求为Boolean类型的参数，默认为true（当dataType为script时，默认为false），设置为false将不会从浏览器缓存中加载请求信息。

6.data: 
要求为Object或String类型的参数，发送到服务器的数据。如果已经不是字符串，将自动转换为字符串格式。get请求中将附加在url后。防止这种自动转换，可以查看　　processData选项。对象必须为key/value格式，例如{foo1:”bar1”,foo2:”bar2”}转换为&foo1=bar1&foo2=bar2。如果是数组，JQuery将自动为不同值对应同一个名称。例如{foo:[“bar1”,”bar2”]}转换为&foo=bar1&foo=bar2。

7.dataType: 
要求为String类型的参数，预期服务器返回的数据类型。如果不指定，JQuery将自动根据http包mime信息返回responseXML或responseText，并作为回调函数参数传递。可用的类型如下： 
xml：返回XML文档，可用JQuery处理。 
html：返回纯文本HTML信息；包含的script标签会在插入DOM时执行。 
script：返回纯文本JavaScript代码。不会自动缓存结果。除非设置了cache参数。注意在远程请求时（不在同一个域下），所有post请求都将转为get请求。 
json：返回JSON数据。 
jsonp：JSONP格式。使用SONP形式调用函数时，例如myurl?callback=?，JQuery将自动替换后一个“?”为正确的函数名，以执行回调函数。 
text：返回纯文本字符串。

8.beforeSend： 
要求为Function类型的参数，发送请求前可以修改XMLHttpRequest对象的函数，例如添加自定义HTTP头。在beforeSend中如果返回false可以取消本次ajax请求。XMLHttpRequest对象是惟一的参数。 
function(XMLHttpRequest){ 
this; //调用本次ajax请求时传递的options参数 
} 
9.complete： 
要求为Function类型的参数，请求完成后调用的回调函数（请求成功或失败时均调用）。参数：XMLHttpRequest对象和一个描述成功请求类型的字符串。 
function(XMLHttpRequest, textStatus){ 
this; //调用本次ajax请求时传递的options参数 
}

10.success： 
要求为Function类型的参数，请求成功后调用的回调函数，有两个参数。 
(1)由服务器返回，并根据dataType参数进行处理后的数据。 
(2)描述状态的字符串。 
function(data, textStatus){ 
//data可能是xmlDoc、jsonObj、html、text等等 
this; //调用本次ajax请求时传递的options参数 
}

11.error: 
要求为Function类型的参数，请求失败时被调用的函数。该函数有3个参数，即XMLHttpRequest对象、错误信息、捕获的错误对象(可选)。ajax事件函数如下： 
function(XMLHttpRequest, textStatus, errorThrown){ 
//通常情况下textStatus和errorThrown只有其中一个包含信息 
this; //调用本次ajax请求时传递的options参数 
}

12.contentType： 
要求为String类型的参数，当发送信息至服务器时，内容编码类型默认为”application/x-www-form-urlencoded”。该默认值适合大多数应用场合。

13.dataFilter： 
要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。提供data和type两个参数。data是Ajax返回的原始数据，type是调用jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处理。 
function(data, type){ 
//返回处理后的数据 
return data; 
}

14.dataFilter： 
要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。提供data和type两个参数。data是Ajax返回的原始数据，type是调用jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处理。 
function(data, type){ 
//返回处理后的数据 
return data; 
}

15.global： 
要求为Boolean类型的参数，默认为true。表示是否触发全局ajax事件。设置为false将不会触发全局ajax事件，ajaxStart或ajaxStop可用于控制各种ajax事件。

16.ifModified： 
要求为Boolean类型的参数，默认为false。仅在服务器数据改变时获取新数据。服务器数据改变判断的依据是Last-Modified头信息。默认值是false，即忽略头信息。

17.jsonp： 
要求为String类型的参数，在一个jsonp请求中重写回调函数的名字。该值用来替代在”callback=?”这种GET或POST请求中URL参数里的”callback”部分，例如{jsonp:’onJsonPLoad’}会导致将”onJsonPLoad=?”传给服务器。

18.username： 
要求为String类型的参数，用于响应HTTP访问认证请求的用户名。

19.password： 
要求为String类型的参数，用于响应HTTP访问认证请求的密码。

20.processData： 
要求为Boolean类型的参数，默认为true。默认情况下，发送的数据将被转换为对象（从技术角度来讲并非字符串）以配合默认内容类型”application/x-www-form-urlencoded”。如果要发送DOM树信息或者其他不希望转换的信息，请设置为false。

21.scriptCharset： 
要求为String类型的参数，只有当请求时dataType为”jsonp”或者”script”，并且type是GET时才会用于强制修改字符集(charset)。通常在本地和远程的内容编码不同时使用。
```
#具体传输DEMO
##JQury.ajax
```base
JQuery在AJAX另有封装，所以当我们不管是传基本数据类型还是复杂数据类型，最终在发出request的时候，会自动解析成一维的数组OR对象
  $.ajax({
                    type: 'POST',
                    url: 'http://www.skybseo.cn/php/jiekou.php',
                    data: {
                        firstName: "Fred",
                        lastName: "Flintstone",
                        boj:{
                            n:1,
                            name:'张三',
                            sex:0
                        },
                        list:['张三','李四','王五','赵六'],
                        listobj:[
                            {id:1,name:'张三'},
                            {id:2,name:'李四'}
                        ]
                    },
                    success: (res)=>{
                        console.log(res)
                    },
                    // dataType: dataType
   });
```
   ![Image text](./img/20180911221408367.png)
```base
后台可根据content-type的类型选择解析的方式
```
##axios
#####application/x-www-form-urlencoded
```base
1、降维复杂数据
2、let 传输数据 = ''
for(let val in data){
   传输数据='&'+val+'='+data[val]
}
具体:
传输复杂类型
1、在属性transformRequest设置
transformRequest: [
function (e) {
                            // 数据转换的核心代码，来自我公司的前端大佬
                            function setDate(e){
                                var t, n, i, r, o, s, a, c = "";
                                for (t in e)
                                if (n = e[t], n instanceof Array)
                                    for (a = 0; a < n.length; ++a)
                                    o = n[a], i = t + "[" + a + "]", s = {}, s[i] = o, c += setDate(s) + "&";
                                else if (n instanceof Object)
                                    for (r in n) o = n[r], i = t + "[" + r + "]", s = {}, s[i] = o, c += setDate(s) + "&";
                                else void 0 !== n && null !== n && (c += encodeURIComponent(t) + "=" + encodeURIComponent(n) + "&");
                                return c.length ? c.substr(0, c.length - 1) : c
                            }
                          return setDate(e)
}],
将数据转为1维
//这个待测试
2、transformRequest:[
function downlevel (data, result={},key) {
    for (let val in data){
      if(typeof data[val] === 'object'){
        if(key){
          downlevel(data[val],result,key+'-'+val)
        } else {
          downlevel(data[val],result, val)
        }
      } else {
        if(key){
          result[key+'-'+val] = data[val]
        }
        else {
          result[val] = data[val]
        }
      }
    }
    return result
  }]
3、npm install qs
传输数据直接包裹qs.stringify
```
#####application/json
```base
JSON.stringify(需要传输的数据)
```
#####multipart/form-data 
```base
直接上传表单数据
 let formData = new FormData();
 formData.append("name", "xxxx");
 formData.append("number", xxxx);
 formData.append("name", "xxxx")
```
#####text/xml 
```base
较少人使用，可忽略
```