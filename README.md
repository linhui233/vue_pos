# awesomepos

> gh-pages提供预览

https://linhui233.github.io/vue_pos/index.html

如何设置参考了https://www.zhihu.com/question/24156818

传上gh-pages预览时出现了问题 
```
The page at 'https://linhui233.github.io/vue_pos/index.html#/' was loaded over HTTPS, but requested an insecure stylesheet 'http://at.alicdn.com/t/font_597851_w1hip3x5hiybvs4i.css'. This request has been blocked; the content must be served over HTTPS.

```
貌似涉及到跨域资源共享的问题
```
跨域资源共享的10种方式:http://www.blueidea.com/tech/web/2010/8049.asp
```

将阿里的图标库改为https,成功访问


但是后台数据不支持http访问，故使用了https://bird.ioliu.cn/ 

通过在http请求前加入了https://bird.ioliu.cn/v1?url= 将http转为https

解决~
