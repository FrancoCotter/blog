---

layout:     post
title:      "POST 和 GET 的区别"
subtitle:   ""
date:       2017-03-19 22:00:00
author:     "Mariano"
header-img: "img/http.png"
tags:  

    - Ajax
    - Get 和 POST 的区别
    - HTTP
---

> 在面试的过程当中遇到了这个问题，总结一下  

HTTP 定义了一组请求方法，用来以 \ 指示针对给定资源要执行的期望动作。虽然他们也可以是名词，但这些请求方法有时被称为 HTTP 动词，每一个请求方法都实现不同的语义，但一些共同的特征由他们的组共享：例如一个请求方法可以是 safe，idempotent 或 cacheable.  

通常，常用的请求无外乎就是 GET 请求和 POST 请求，现在就这两种请求有什么区别展开讨论  

> GET  

GET 方法意味着检索由 Request-URI 标识的任何信息（以表单实体的形式）。如果 Request-URI 指的是数据生成的过程，那么生成的数据将作为响应中的实体而不是流程的源文本返回，除非文本恰好是流程的输出。  

如果请求消息包括 If-Modified-Since，If-Unmodified-Since，If-Match，If-None-Match或 If-Range 头字段，则 GET 方法的语义改变为“条件GET”。 条件 GET 方法请求仅在由条件头字段描述的情况下传送实体。 条件 GET方法旨在通过允许高速缓存的实体被刷新而不需要多个请求或者传送已经由客户端保存的数据来减少不必要的网络使用。  

如果请求消息包括 Range 头字段，那么 GET 方法的语义将更改为 “partial GET”。 部分  GET请求仅传输实体的一部分，如第 14.35 节所述。 部分 GET 方法旨在通过允许部分检索的实体被完成而不传送已经由客户端保持的数据来减少不必要的网络使用。

当且仅当它满足第 13 节中描述的 HTTP 缓存的要求时，对 GET 请求的响应才是可缓存的。



> POST 

POST 方法用于请求原始服务器接受请求中包含的实体作为请求行中的 Request-URI 所标识的资源的新从属。 POST 被设计为允许统一的方法来覆盖以下功能：

- 注释现有资源;
- 将消息发布到公告牌，新闻组，邮件列表，
     或类似的物品组;
- 提供一组数据，例如提交a的结果
     形式，到数据处理过程;
- 通过追加操作扩展数据库。 

POST 方法执行的实际功能由服务器确定，通常取决于Request-URI。发布的实体从属于该 URI，其方式与文件从属于包含它的目录，新闻文章从属于其发布到的新闻组或记录从属于数据库的方式相同。

POST 方法执行的操作可能不会导致可以由 URI 标识的资源。在这种情况下，根据响应是否包括描述结果的实体，200（OK）或204（无内容）是适当的响应状态。

如果在源服务器上创建了资源，则响应应该是 201（已创建），并包含描述请求状态并引用新资源的实体，以及位置头（请参阅第14.30节）。

对此方法的响应不可缓存，除非响应包括适当的 Cache-Control 或 Expires 标头字段。但是，303（请参阅其他）响应可以用于指示用户代理检索可缓存资源。

POST 请求必须遵守第8.2节中规定的消息传输要求。

完整描述请查看 [w3.org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)

> 在搞懂 GET 和 POST 的本质之后，我们在来看看他们之间到底有什么不同  

GET 方法请求指定的资源，使用 GET 的请求应该只用于获取数据  

POST 方法发送数据给服务器，请求主体的类型由 Content-type 首部指定，一个 POST 请求通常是通过 HTML 表单发送，并返回给服务器修改结果，在这种情况下，content type 是通过在 `<form>` 元素中设置正确的 enctype 属性，或是在 `<input>` 和 `<button>` 元素中设置 formenctype 属性来选择的：

* application/x-www-form-urlencodde:数据被编码以 '&' 分隔的键值对，同时以 '=' 分隔键和值，非字母或数字的字符会被 percent encoded，这也就是为什么这种类型不支持二进制数据的原因（应使用 application/form-data 代替）
* application/form-data
* text/plain

当 POST 请求是通过除 HTML 表单之外的方式发送时，例如使用 XMLHttpRequest,那么请求主体可以是任何类型

总而言之， GET 和 POST 的区别无外乎下面几种考虑

* GET 在浏览器回退时是无害的，而 POST 会再次提交请求
* GET 产生的 URL 地址可以被存为书签，而 POST 不可以
* GET 请求会被浏览器主动缓存，而 POST 不会，除非手动设置
* GET 请求只能进行 URL 编码，而 POST 支持多重编码方式
* GET 请求参数会被完整保留在浏览器历史记录里，而 POST 中的参数不会被保留
* GET 请求在 URL 中传送的参数是有长度限制的，而 POST 没有
* 对于参数的数据类型，GET 值接受 ASCII字符，而 POST 没有限制
* GET 比 POST 更不安全，因为参数直接暴露在 URL 上，所以不能用来传递敏感信息。
* GET 参数通过 URL 传递，POST 放在请求主体（Request body）中。