---
title: 给Github Pages添加自定义域名
date: 2022-07-11 17:36:15
categories:
- [Notes, GitHub]
tags:
- github
- notes
---

博客网站搭建好了，但访问的时候只能是以固定的域名形式（用户名.github.io）进行访问。这时可以通过购买域名的方式行实现自定义域名访问。可以去国外买或者国内，国内都是需要备案的。

## 购买域名后：

1. 首先是用ping命令找到存放你的github pages的主机的IP地址(或者去Github Pages Doc里找)，在终端里面用命令ping
    xxx.github.io便可完成，下图中红框内的就是我们要找的IP地址：

![使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages_GitHub](https://s2.51cto.com/images/blog/202105/20/0512eaedbd589700a91cc59d3e37b64c.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

2. 在购买域名的提供商为域名添加解析。我是在阿里云买的域名，因此我以阿里云的为例。在域名控制台选择想要绑定的域名，并点击解析：
    
![使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages_GitHub Pages_02](https://s2.51cto.com/images/blog/202105/20/35b942d661269dd6b40f3d8a32853fe8.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

* 记录类型：CNAME 将一个域名指向例外一个域名，再由另一个域名提供IP地址，就需要添加 CNAME 记录。
主机记录：www 表示访问域名的时候以www开头为一级域名。如果是二级域名的话就在前面加上自己想要的参数，访问的时候也是以二级域名的形式访问。

![使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages_GitHub Pages_03](https://s2.51cto.com/images/blog/202105/20/60c6863f819cb45d4d1460947bf0ae71.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

* 记录类型：A 将域名指向一个IPv4地址，如果需要将域名指向一个 IP 地址（外网地址），就需要添加 A 记录
主机记录：@ 表示访问的时候直接用 yunxdr.top 形式访问，前面不加任何参数。如果是www，就要以 www.yunxdr.top访问。这里设置的@形式与下面GitHub上自定义的域名要对应


![使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages_GitHub Pages_04](https://s2.51cto.com/images/blog/202105/20/71ffdd069477ff0f54c6e99a3a6a4e71.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)


3. 在上面存放静态网站的Repository Settings里面GitHubPages Custom domain（自定义域名）填上自己的域名点击save；

![使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages_GitHub Pages_05](https://s2.51cto.com/images/blog/202105/20/464684d5f94bae03fc7f9b78d3b9e200.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)
![使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages_GitHub Pages_06](https://s2.51cto.com/images/blog/202105/20/d70a389b9f4a2c5a65673dd0e8d29147.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

    设置完成后就可以通过 yunxdr.top 访问部署在GitHub上的hugo的网站了
![使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages_GitHub_07](https://s2.51cto.com/images/blog/202105/20/22dcdbfc29349c3bf60028f2d9a679c4.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

## 例外如果不太懂解析域名的可以参考如下资料：

![渲染结果](https://s2.51cto.com/images/blog/202105/20/645eab10e04fdad97fb283e5b49ba03b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)
![渲染结果](https://s2.51cto.com/images/blog/202105/20/12f8d9b219674566e500a98dbf42b3fe.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)
    关于记录值www和@的区别

*  创建 www.dns-example.com 的子域名。
![渲染结果](https://s2.51cto.com/images/blog/202105/20/9e9a4bccd513ffb7f8eddcf0ed53ef72.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

* 创建 dns-example.com 的子域名。
![渲染结果](https://s2.51cto.com/images/blog/202105/20/fcaa518bb5d34d486ed8b981155c03ab.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

---
## Ref:
> [使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages](https://blog.51cto.com/xdr630/2795777)