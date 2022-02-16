### 有哪些常见的 web 攻击方式

- CSRF: 跨站请求伪造

跨站请求伪造: 引诱用户打开黑客的网站，在黑客的网站中，利用用户的登录状态发起的跨站请求

CSRF 产生的条件:

1. 目标站点一定要有 CSRF 漏洞
2. 用户登录过目标站点，并且在浏览器中保持有该站点的登录状态
3. 需要用户打开一个第三方站点，可以是攻击者的站点，也可以是一些论坛

**防御方式**:

1. 充分利用好 Cookie 的 SameSite 属性
2. 验证请求的来源站点
3. 在请求地址中添加 token 并验证
4. 在 HTTP 头中自定义属性并验证
5. 利用浏览器的同源策略
6. 验证 HTTP Referer 字段

通过请求头中的 referer 和 origin 判断来源是否合法

- XSS: 跨站脚本攻击

通过代码注入的方式达到攻击的目的。恶意攻击者往 Web 页面里插入恶意 Script 代码，当用户浏览该页之时，嵌入其中 Web 里面的 Script 代码会被执行，从而达到恶意攻击用户的目的。

分类:

- Reflected XSS(基于反射的 XSS 攻击)
- STored XSS(基于存储的 XSS 攻击)
- DOM-based or local XSS(基于 DOM 或本地的 XSS 攻击)

**防御方式**:

总体应对措施: 对于一切用户的输入、输出、客户端的输出内容视为不可信，在数据添加到 DOM 或者执行了 DOM API 的时候，我们需要对内容进行 HtmlEncode 或 JavaScriptEncode，以预防 XSS 攻击。

1. 将 cookie 等敏感信息设置为 httponly，禁止 Javascript 通过 document.cookie 获得
2. 对所有的输入做严格的校验尤其是在服务器端，过滤掉任何不合法的输入，比如手机号必须是数字，通常可以采用正则表达式.
3. 净化和过滤掉不必要的 html 标签，比如：iframe, script 等 ;净化和过滤掉不必要的 Javascript 的事件标签，比如：onclick, onfocus 等
4. 转义单引号，双引号，尖括号等特殊字符，可以采用 htmlencode 编码 或者过滤掉这些特殊字符
5. CSP，全称为 Content Security Policy，即内容安全策略。主要以白名单的形式配置可信任的内容来源，在网页中，能够使白名单中的内容正常执行（包含 JS，CSS，Image 等等），而非白名单的内容无法正常执行，从而减少跨站脚本攻击（XSS），当然，也能够减少运营商劫持的内容注入攻击。

要开启 CSP 可以通过以下两种方式:

一. 设置 HTTP Header 中的 Content-Security-Policy

二. 设置 meta 标签的方式

- SQL 注入

预防策略:

1. 禁止目标网站利用动态拼接字符串的方式访问数据库
2. 减少不必要的数据库抛出的错误信息
3. 对数据库的操作赋予严格的权限控制
4. 净化和过滤掉不必要的 SQL 保留字，比如：where, or, exec 等

- 点击劫持/UI 覆盖攻击

防御方式:

1. 服务端添加 X-Frame-Options 响应头,这个 HTTP 响应头是为了防御用 iframe 嵌套的点击劫持攻击。这样浏览器就会阻止嵌入网页的渲染。
2. JS 判断顶层视口的域名是不是和本页面的域名一致，不一致则不允许操作，top.location.hostname === self.location.hostname；
3. 敏感操作使用更复杂的步骤（验证码、输入项目名称以删除）。

- 中间人攻击

- 文件上传漏洞

- window.opener 安全问题

预防策略: 设置 a 标签的 rel 属性，设置为 noopener noreferrer
