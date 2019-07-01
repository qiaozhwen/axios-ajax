api实例
get
axios:
axios.get('/user?ID='+'xxxxx')
          .then(function (response) {
            console.log(response);
          })
          .catch(function (error) {
            console.log(error);
          });
ajax:
$.ajax({
    type: "get",
    url:后台给出接口地址,
    data: 'xxxxxx',
    success: function (res) {
        console.log(res)
    },
    error:function(err){
        console.log(err)
    }
});
XMLHttpRequest:
var xhr = new XMLHttpRequest();
xhr.open('GET', '/server', true);

更多请参考官方文档
https://api.jquery.com/jquery.ajax/
https://github.com/axios/axios
简单数据上传
简单类型数据上传可分为三种，一种为url传值，另一种为Path传值，最后一种为body传值
url常用于get请求，主要应用场景为查询某值的情况下，而body主要应用于插入或者更新某条数据的情况下

url:
axios.get('/user?ID=12345')
 .then(function (response) {
    处理业务逻辑
  })
path:
axios.get(`abc${12345}def`)
 .then(function (response) {
    处理业务逻辑
  })
body:
axios.get('/user',{params:{id:12345}})
 .then(function (response) {
    处理业务逻辑
  })
然而我们不管使用ajax或axios发request的时候，最终都是由浏览器编译后发出，而浏览器选择以什么格式发出则是根据content-type字段决定

1、application/json：

消息主体是序列化后的 JSON 字符串，
图片: https://uploader.shimo.im/f/jDIJRYUcJMUVioZV.png

2、application/x-www-form-urlencoded：

提交的数据按照 key1=val1&key2=val2 的方式进行编码，key 和 val 会进行了 URL 转码。
图片: https://uploader.shimo.im/f/Sb1LPmDlA10rOukG.png

3、multipart/form-data： 

数据被编码为控件名/控件值上传到后台
图片: https://uploader.shimo.im/f/uRG6qI5moUUyUoC9.png

4、text/plain：

数据以纯文本形式(text/json/xml/html)进行编码，其中不含任何控件或格式字符。
图片: https://uploader.shimo.im/f/98OhOsmhy3cPKuvo.png

针对不同请求对应的content-type也不同
get
GET 请求不存在请求实体部分，键值对参数放置在 URL 尾部，浏览器把form数据转换成一个字串
（name1=value1&name2=value2...）然后把这个字串追加到url后面，用?分割，加载这个新的url。
因此请求头不需要设置 Content-Type 字段
post
1.application/x-www-form-urlencoded：数据被编码为名称/值对。

a='1123'&b='123'&c='5645'


2.multipart/form-data(一般用来上传文件)：页面上的每一个控件对应一个值且用

txt1=hello&text2=world
     

3.application/json

数据被编码为json格式的数据类型，也是axios的默认类型

{"txt1":"hello","text2":"text2","c":"3"}


4.text/xml

数据以纯文本形式(text/json/xml/html)进行编码，其中不含任何控件或格式字符。

针对复杂数据的操作
一般来说上传复杂数据，我们采用的是json格式传输到后台，但是后台不是都支持json格式的数据，所以我们需要在特定情况下对一些复杂操作做一些封装/降维操作。
ajax
1、application/x-www-form-urlencoded 
ajax(封装了发送复杂数据格式的方法)，所以直接传输复杂的数据即可
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
上传截图:
                       图片: https://uploader.shimo.im/f/LkyMehuJptElb0pq.png
2、application/json
  $.ajax({
  type: "post",
  url:  "asda",
  contentType: "application/json",
  data:JSON.stringify(需要上传的数据),
  dataType: "json",
  success: function(data) {
    console.log(data);
  },
  error: function(msg) {
    console.log(msg)
  }
})
上传截图:
                        图片: https://uploader.shimo.im/f/HEUUR17x4EMj4XwK.png
axios
axios没有封装这样的功能,这里需要根据不同的content-type做不同操作
1、application/x-www-form-urlencoded 

application/x-www-form-urlencoded处理复杂数据时是无法将信息传到后台
第一种做法是在属性transformRequest设置
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
处理后的数据:
                       
                    图片: https://uploader.shimo.im/f/1OcLUXuHRWskmN8U.png
第二种做法(qs插件)
 axios.post(
    url, 
    qs.stringify(data), 
    {headers: {'Content-Type': 'application/x-www-form-urlencoded'}}
).then(result => {
    // do something
})

2、application/json

将数据以json对象的格式传递，默认content-type，在发送数据之前需格式化数据JSON.stringify()

let data = {
                    id:1,
                    name:'李四',
                    arr:['张三','王五','赵六','刘七'],
                    list:[
                        {id:1,name:'周八',sex:1},
                        {id:2,name:'卢九',sex:0},
                        {id:3,name:'齐十',sex:1},
                    ],
                    obj:{
                        title:'axios请求学习',
                        time:'2018-9-11'
                    }
                }
                // console.log(data)
                axios({
                        method: "POST",
                        url: 'jiekou.php',
                        data:data,
                        headers: {
                            'Content-Type': 'application/json;charset=UTF-8',  //指定消息格式
                        },
                    })
                    .then((res) => {
                        console.log(res)
                    })
                    .catch((err) => {
                        console.log(err)
                    })

XMLHttpRequest
1、application/x-www-form-urlencoded
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
转换数据格式为
图片: https://uploader.shimo.im/f/cOGQ277MEO07pVax.png

2、application/json
let xhr = new XMLHttpRequest();
xhr.open('post', '/requestUrl');
xhr.setRequestHeader('content-type', 'application/json; charset=UTF-8');
let data = JSON.stringify({username: 'xxx', pass: 'xxx'});
xhr.send(data);
