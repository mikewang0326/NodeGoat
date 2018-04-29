一，XSS

0, Example
   0-1  把用户lastname保存为<script>alert('Hello World')</script>

1, How to prevent XSS attacks

    1-1 Input validation and sanitization
    1-2 Output encoding for correct context
    1-3 HttpOnly cookie flag
        特定Cookie只允许服务端使用，不允许客户端本地js调用
    1-4 Implement Content Security Policy(CSP)
        通过制定不同的policy，可以指定网页中各个内容的加载来源。
        eg1， Content-Security-Policy: default-src 'self' 只从主域名访问
        eg2， Content-Security-Policy: default-src 'self' *.trusted.com ，从主域名和子域名访问
        eg3，Content-Security-Policy: default-src 'self'; img-src *; media-src media1.com media2.com;
              script-src userscripts.example.com， 指定图片和媒体的访问来源
    1-5 Apply encoding on both client and server side
2, Fix
   2-1
   swig.setDefaults({
           // Autoescape disabled
           autoescape: true (from false to true)
           /*
           // Fix for A3 - XSS, enable auto escaping
           autoescape: true // default value
           */
       });

二，Injection Attacks

0, Example
   0-1 修改某字段为process.kill(process.pid)
   0-2 修改某字段为res.end(require('fs').readdirSync('.').toString())

1, How to prevent injection attacks
   1-1 Validate user input on server side before process
   1-2 Do not use the eval() function to parse user inputs. Avoid using other commands with similar effect,
       such as setTimeOut(), setInterval() and Function().
   1-3 For parsing JSON input, instead of using eval(), use a safer alternative such as JSON.parse().
       For type conversition, use type relateparseXXX() methods.
   1-4 Include "use strict"; at the top of each source file.

2，Fix
   2-1,
   // Insecure use of eval() to parse inputs
   // var preTax = eval(req.body.preTax);
   ---->
   //Fix for A1 -1 SSJS Injection attacks - uses alternate method to eval
   var preTax = parseInt(req.body.preTax);

三，Broken authentication vulnerabilities
0, Example (Scenario)
   0-1 用户使用公共电脑访问，未登出。之后有其他使用这个电脑，就可以访问之前用户已经登录的网页。
   0-2 通过获取其他用户的session_id, Attacker 就可以连接而不需要用户名和密码
   0-3 Attacker获取系统数据库密码， 用户的密码没有加密，用户的密码泄露

1，How to avoid Broken authentication vulnerabilities
   1-1 密码加密
   1-2 错误提示信息不要具体
   1-3 Sesstion和Cookie的优化，例如设置security或者HttpOnly
   1-4 使用第三方中间件授权，eg，passportjs

