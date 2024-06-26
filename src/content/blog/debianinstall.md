---
title: 'Debian的安装和配置'
description: '基于debian12'
pubDate: 'Jun 26 2024'
heroImage: '/debian12.png'
pinned: true
---

#### 总的来说具体的浏览器可以搜到，这里只说我自己安装的一些不同...
大体的我按照这个来安装的
https://blog.csdn.net/weixin_44200186/article/details/131970040

##### 1 出现执行某个步骤失败，尝试重新运行这个项目 的问题
解决原理不明，总之我磁盘分区改为

- | Guided-use entire disk | 带引导模式方式直接使用整块磁盘 |

- 不使用镜像源

就解决了

##### 2 怎么让字符拼出debian的logo
```bash
$ sudo apt-get install screenfetch
$ screenfetch
```
假如出现了提权问题，即提示不是 `sudoers`文件等等

我是参照了这篇文章
https://www.mulingyuer.com/archives/940/

结果：
https://live.staticflickr.com/65535/53814829922_251592d412_b.jpg
