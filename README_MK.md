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