# web 前端性能优化

- [web 前端性能优化](#web-%E5%89%8D%E7%AB%AF%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96)
    - [浏览器访问优化](#%E6%B5%8F%E8%A7%88%E5%99%A8%E8%AE%BF%E9%97%AE%E4%BC%98%E5%8C%96)
    - [CDN 加速](#cdn-%E5%8A%A0%E9%80%9F)
    - [反向代理](#%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86)
    - [Reference](#reference)

## 浏览器访问优化

- 减少 http 请求

  http 协议是无状态的应用层协议，意味着每次 http 请求都需要建立通信链路、进行数据传输，而在服务器端，每个 http 都需要启动独立的线程去处理。减少 http 请求的数目可有效提高访问性能。
  主要手段：合并JavaScript 合并CSS 合并图片

- 使用浏览器缓存

  一些静态文件几乎每次 http 请求都需要的，可以将它们缓存在浏览器中。
  主要手段：设置 http 头中 Cache-Control 和 Expires 的属性

- 启用压缩

  在服务器端对文件进行压缩，在浏览器端对文件解压缩
  主要手段：在服务器上启用 GZip 压缩

- CSS 放在页面最上面，JavaScript 放在页面最下面

  浏览器会在下载完全部 CSS 之后才对整个页面进行渲染，所以要放在前面
  浏览器加载 JavaScript 后立即执行，有可能阻塞页面，所以要放在后面，但页面解析时用到 JavaScript 的情况除外

- 减少 Cookie 传输

  Cookie 包含在每次请求和响应中，尽量减少 Cookie 中传输的数据量
  静态资源用独立域名访问，避免请求静态资源时发送 Cookie，减少 Cookie 传输的次数

## CDN 加速

见图4.5 利用 CDN 的网站架构

离网站访问者最近的服务器响应网络请求。内容分发网络复制了一个网站的页面，然后发给一个依不同的地理位置分布的服务器。这台服务器将缓存下该页面。当用户请求一个在内容分发网络中已有的页面时，内容分发网络将把“请求”从来源网站的服务器转发到内容分发网络中的离用户最近的一台服务器上，然后内容分发网络把缓存内容分发给该用户。如果内容分发网络中没有已缓存的页面，它将和来源网站的服务器通信，把还没有被缓存的内容发送给该用户。

详见“ACADEMIC -> Network -> Server Infrastructure -> CDN”

## 反向代理

见图4.6 利用反向代理的网站架构

正向代理：代理服务器替代访问方【用户A】去访问目标服务器【服务器B】
反向代理：反向代理正好与正向代理相反，对于客户端而言代理服务器就像是原始服务器，并且客户端不需要进行任何特别的设置。客户端向反向代理的命名空间(name-space)中的内容发送普通请求，接着反向代理将判断向何处(原始服务器)转交请求，并将获得的内容返回给客户端。

详见“ACADEMIC -> Network -> Server Infrastructure -> Proxy -> Reverse Proxy“

## Reference

- [CDN - Content Delivery Network](http://www.webopedia.com/TERM/C/CDN.html)
- [图解正向代理、反向代理、透明代理](http://z00w00.blog.51cto.com/515114/1031287)
