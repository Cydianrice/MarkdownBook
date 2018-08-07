

**多方面分析国内外公开的CDN**

==原创：Cydia·Rice（可能存在表达错误或者测试失误,请耐心提问或者指出错误），转载需注明==
==部分功能未参与此次分析，你可以在下面的评论提出来。部分分析不到位，请耐心指出，切勿大肆吐槽。==

多方便分析了这些CDN，各有利弊。公开的静态资源库是本次分析的重点，两大厂的自建CDN也加入本次分析。从中，我们或许可以了解哪些CDN比较可靠，哪些CDN服务的内容或区域更加适合我们。
**参与分析的CDN**

由于第二个CDN官网未有名称，根据域名，暂且和同域名的图床同名。BootCDN官网不稳定（因为引用了自家的CDN啊，所以----）。JSDelivr因部分地区algolia搜索框加载慢，官网体验不佳。

![参与分析的CDN](https://i.imgur.com/KZXcKdn.png)


**CDN服务**

绿色的CDN服务较多。其中，公开CDN-SM.MS和75CDN，较其他CDN，提供更多服务。自建CDN的服务内容主要看源站了，这里不做比较。

![CDN服务比较](https://i.imgur.com/wPgtWJA.png)

**CDN资源来源**

绿色表明资源多，有些相当少，百度中规中矩。（对于国内的公共CDN来源并不唯一，这里注明主要来源。大多数都提供了“申请添加资源”功能，但只有75CDN能够及时响应并添加或手动更新，其他的一般申请都不了了之。）

![来源分析](https://i.imgur.com/knArA36.png)

**公开CDN域名、链接、证书安全性**

百度、BootCDN、CDNJS、Microsoft的CDN域名或与主服务的证书一致，或为可自动续期的证书。理论上，上述CDN的HTTPS证书可得到保障。（我没有歧视证书的不同=.= ）。也可以从中看出，多数公开CDN均使用了泛域名证书。

![CDN域名以及证书](https://i.imgur.com/JUiNR7w.png)

SM.MS,CDNJS,JSDelivr采用了更安全的策略（Use HTTPS-HTTPS only 指 HTTP不会跳转到HTTPS，但HTTPS访问后不可降级，将会带上strict-transport-security头；SM.MS的安全策略颇为奇怪，部分CDN服务域名使用Use HTTPS-HTTPS only，部分CDN服务域名HTTPS和HTTP可任意跳转；JSDelivr将在April 31st启用HTST，不再提供HTTP，HTTP强制跳转HTTPS；腾讯海外CDN至今仍未提供强制HTTPS服务）。

我们还可以看出，直接提供SRI服务的有75CDN（官网需按照指示开启SRI，复制link或script标签时自动添加）。SRI是浏览器的一种安全策略，防止第三方（中间人？拉光纤的？）篡改CDN文件内容。Github于September 19, 2015已完成Github网页的SRI改造，加强Github的安全性。SRI并非只有官方可以提供，我们可以手动根据CDN静态链接来获取SRI（麻烦一点=.=  ）。

``` text
不要认为SRI多此一举，你可是在国内环境。JSDelivr约半年前，国内CDN被其服务商投毒，后紧急撤回。BootCDN已多次反馈各地CDN被劫持，并要求升级为HTTPS。
```

![链接安全性](https://i.imgur.com/ru73BuV.png)

**国内外IP数和PING的均值**

不要还没看完就认为我歧视那些IP少的CDN，CDN的质量和IP数无直接关联。图中的IP数，绿色为解析IP和其解析地所匹配，红色则为不匹配（国内解析到国外，反之亦然）。后面为对应的均值PING。SM.MS\75CDN\JSDelivr\又拍CDN表现突出，国内外均能正常解析至就近IP，所以其PING值也较低。

![IP数和PING值(均值)](https://i.imgur.com/QSNnewq.png)

**实际文件测试&CDN路径比较&问题**

说明：非单机测试，均为多地服务器测试，均为均值。测试时前5次测试值放弃，保证CDN已取回文件，减少源站的干扰。“-”值为无该文件。除CDNJS取回的文件大小为450KB外，其他测试的CDN取回的文件为element4.5版本的index.js（525.854KB）。新浪CDN未能测试到element的index.js文件，但在查询库时，部分CDN文件存在编码错误（已排除本地问题和引用问题）。

同步CDNJS库的CDN路径相同，开发时便于某些特殊操作。

可以看出，0.5MB的JS，CDNJS最慢，其他表现差异不明显。JSDelivr因压缩方式不同，实际传回文件更小。

![实测数据](https://i.imgur.com/iBAszoe.png)

**总结**

==CDN无好坏之分，分析只是为了寻找更合适的CDN服务。每一个CDN的提供商都不容易。我们也可以从中看到某些大厂，对于公共CDN的服务态度。==

