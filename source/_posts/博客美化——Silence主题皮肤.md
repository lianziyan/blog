---
title: 博客美化——Silence主题皮肤
tags:
  - 博客园
  - 博客美化
categories:
  - 博客园博文
  - 博客美化
top_img: 'https://cdn.jsdelivr.net/gh/glassy-sky-lisong/StaticFile@master/top-img/3.jpg'
abbrlink: 3ba53770
date: 2020-08-30 20:08:31
---

## 介绍
&emsp;&emsp;一款专注阅读的博客园主题，主要面向于经常混迹 博客园 的朋友。其追求大道至简的终极真理，界面追求简洁、运行追求高效、部署追求简单。
* [博客皮肤源码地址](https://github.com/glassy-sky-lisong/SilenceSkin)
* [预览地址](https://www.cnblogs.com/esofar)
* [如何部署、使用皮肤](https://github.com/esofar/cnblogs-theme-silence/blob/master/docs/deploy.md)
* [Silence作者的友链](https://www.cnblogs.com/esofar/p/cnblogs-theme-silence.html)

## 特点
* 简洁优雅、精致漂亮的 UI 设计
* 提供多种风格主题以便适应各类用户的偏好
* 响应式设计，兼容手机端浏览器
* 提供事无巨细的部署文档
* 源码结构清晰并且注释完整，方便扩展

## 开发
&emsp;&emsp;请先确保您正在使用的机器已经安装 Node.js 和 Git 客户端。

     git clone https://github.com/esofar/cnblogs-theme-silence.git   # 克隆源码
     cd cnblogs-theme-silence                                        # 进入项目
     npm install                                                     # 安装依赖
     npm run build
    
&emsp;&emsp;如果没有安装node。js或者不会使用的童鞋可以在我的GitHub，也就是博客皮肤源码地址中。

## 部署
&emsp;&emsp;重点部署之前使用博客园的cutorm皮肤，具体部署细节请详见'如何部署、使用皮肤'，如果又不会的话可以看一看我的配置作为参考（仅作为参考，找不回来别哭鼻子）
***CSS***

    <!-- 溢出隐藏设置（放置在管理--> 设置--> css模块中） -->
    #topics, #mainContent {
        overflow: visible;
    }
    .cnblogs-markdown .hljs{
	    display:block;
	    color:#333;
	    overflow-x:auto;
	    background:#F2F4F5!important;
	    border:none!important;
	    font-family:Consolas,Monaco,'Andale Mono','Ubuntu Mono',monospace!important;
	    padding:1em!important;
	    font-size:14px!important
	    }

***侧边栏公告***

    <!-- 在管理--> 设置-> 侧边栏公告(支持js代码、支持html代码) -->
    <script src="https://blog-static.cnblogs.com/files/glassysky/silence.min.js"></script>
    <script type="text/javascript">
        $.silence({
            profile: {
                enable: true,
                avatar: 'https://gitee.com/glassyskyforgame/glassysky/blob/master/4c67d1a20cf431ade2873e284836acaf2fdd989e.jpg',
                favicon: 'https://gitee.com/glassyskyforgame/glassysky/raw/master/4c67d1a20cf431ade2873e284836acaf2fdd989e.jpg',
            },
            catalog: {
                enable: true,
                move: true,
                index: true,
                level1: 'h2',
                level2: 'h3',
                level3: 'h4',
            },
            signature: {
                enable: true,
                home: 'https://www.cnblogs.com/glassysky/',
                license: '署名 4.0 国际',
                link: 'https://creativecommons.org/licenses/by/4.0'
            },
            reward: {
                enable: true,
                title: '感谢小可爱投食',
                wechat: 'https://images.cnblogs.com/cnblogs_com/esofar/972540/o_wechat.png',
                alipay: 'https://images.cnblogs.com/cnblogs_com/esofar/972540/o_alipay.png'
            },
            github: {
                enable: true,
                color: '#fff',
                fill: null,
                link: 'https://github.com/glassy-sky-lisong'
            }
        });
    </script>
    <!--外置主题css补丁-->
    <link rel="stylesheet" type="text/css" href="https://blog-static.cnblogs.com/files/glassysky/sli.css"/>

***会动的title***

    <!-- 动态titlejs -->
    <script> var OriginTitle = document.title; var titleTime; document.addEventListener('visibilitychange', function () { if                 
    (document.hidden) { document.title = '╭(°A°`)╮ 页面崩溃啦 ~'; clearTimeout(titleTime); } else { document.title = '(ฅ>ω<*ฅ) 噫又    
    好了~' + OriginTitle; titleTime = setTimeout(function () { document.title = OriginTitle; }, 2000); } }); </script>

***图片放大功能***

    <!--图片放大的zoomcss和js-->
    <link rel="stylesheet" type="text/css" href="https://blog-static.cnblogs.com/files/glassysky/zoom.css"/>
    <script src="https://blog-static.cnblogs.com/files/glassysky/zoom.js"></script>
    <!-- Bootstrap 的 transition.js cdn（过渡动画插件）-->
    <script type="text/javascript">$('#cnblogs_post_body img').attr('data-action', 'zoom');</script>

## 博客的皮肤风格
* 简约·蓝
  ![img1](https://github.com/esofar/cnblogs-theme-silence/raw/master/docs/theme_default.png) 
* 暗黑·绿
  ![img2](https://github.com/esofar/cnblogs-theme-silence/raw/master/docs/theme_dark.png)
* 女神·粉
  ![img3](https://github.com/esofar/cnblogs-theme-silence/raw/master/docs/theme_goddess.png)  
