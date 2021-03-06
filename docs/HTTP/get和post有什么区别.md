### get 和 post 有什么区别

请求参数: get 请求参数是通过 url 传递的，多个参数以&拼接；post 请求放在 request body 中

请求缓存: get 请求会被缓存，post 请求不会，除非手动设置(如何设置？)

相对的安全性: get 是将参数通过 url 传递的，会被浏览器缓存，容易被他人获取，post 相对较安全

请求参数长度限制: get 通过 url 传参，浏览器会限制 url 的长度

编码方式: get 请求只能进行 url 编码，而 post 支持多种编码方式

实际上 HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对 get 请求参数的限制是来源与浏览器或 web 服务器，浏览器或 web 服务器限制了 url 的长度。为了明确这个概念，我们必须再次强调下面几点:

HTTP 协议 未规定 GET 和 POST 的长度限制

GET 的最大长度显示是因为 浏览器和 web 服务器限制了 URI 的长度

不同的浏览器和 WEB 服务器，限制的最大长度不一样

要支持 IE，则最大长度为 2083byte，若只支持 Chrome，则最大长度 8182byte

补充补充一个 get 和 post 在缓存方面的区别：

get 请求类似于查找的过程，用户获取数据，可以不用每次都与数据库连接，所以可以使用缓存。

post 不同，post 做的一般是修改和删除的工作，所以必须与数据库交互，所以不能使用缓存。因此 get 请求适合于请求缓存。
