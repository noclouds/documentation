## CDNBye :id=head
> 基于WebRTC技术的视频网站省流量&加速引擎，无需安装任何浏览器插件，与高昂的CDN流量费Say Goodbye!

## 面向未来的P2P流媒体技术
P2P技术使观看相同内容的用户之间可以相互分享数据，不仅能效降低视频/直播网站的带宽成本，还可以提升用户的播放体验，降低卡顿、二次缓存的发生率。
<br>另外，随着H5的普及，flash逐渐被淘汰已成为不可逆转的趋势。而在H5采用的视频传输格式中，hls由于兼容ios和android、可以穿过任何允许HTTP数据通过的防火墙、容易使用内容分发网络来传输媒体流和码率自适应等众多优势而在业界得到广泛使用。通过使用[hls.js](https://github.com/video-dev/hls.js)这个第三方库，几乎所有现代浏览器都可以播放hls视频。hls天生分片传输的优势，使其可以采用p2p的方式进行传输，从而减小服务器的负担。
<br>在Web端，无插件化实现p2p传输能力的最好选择就是[WebRTC](https://zh.wikipedia.org/wiki/WebRTC)技术，与hls.js类似，WebRTC也支持几乎所有现代浏览器。本项目是一个hls.js的插件，通过WebRTC datachannel技术，在不影响用户体验的前提下，最大化p2p率，是面向未来的Web P2P技术。

## 特性
- 浏览器原生支持，不需要安装任何插件，采用仿BT算法，在线人数越多效果越好
- 支持基于HLS流媒体协议(m3u8)的直播和点播场景
- 不改动hls.js源码，并且可以与其无缝衔接，几行代码集成，便于在现有项目中快速集成
- 浏览器不支持WebRTC时无缝切换到HTTP下载模式
- 高可配置化，用户可以根据特定的使用环境调整各个参数
- 支持video.js、Clappr、Flowplayer等第三方播放器
- 通过有效的调度策略来保证用户的播放体验以及p2p率
- Tracker服务器根据访问IP的ISP、地域等进行智能调度
- API已经固化，新版本完全兼容旧版本代码

## 演示Demo
打开2个相同的网页：[demo](https://demo.cdnbye.com/)

## 浏览器支持情况
由于WebRTC已成为HTML5标准，目前大部分主流浏览器都已经支持。CDNBye的浏览器兼容性取决于WebRTC和hls.js。需要注意的是iOS版Safari由于不支持MediaSource API，因此也不支持hls.js(不过Safari原生支持HLS播放)。

 兼容性|Chrome | Firefox | Mac Safari| 安卓微信/QQ | Opera | IE | Edge| iOS Safari | 
:-: | :-: | :-: | :-: | :-: | :-: | :-:| :-:| :-:
WebRTC | ✔ | ✔ | ✔ | ✔ | ✔ | ❌ | ❌ | ✔ |
Hls.js | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ❌ |
CDNBye | ✔ | ✔ | ✔ | ✔ | ✔ | ❌ | ❌ | ❌ |

## 后台管理系统
在接入P2P插件后，访问`https://oms.cdnbye.com`，注册并绑定域名，即可查看该域名的P2P流量、在线人数、用户地理分布等信息。

## 客户案例
[<img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1531253035445&di=7af6cc9ad4abe3d06ba376af22d85131&imgtype=0&src=http%3A%2F%2Fimg.kuai8.com%2Fattaches%2Fintro%2F1213%2F201612131436417407.png" width="120">](https://egame.qq.com/?hls=1&p2p=1&_debug=1)

## 联系我们
邮箱：service@cdnbye.com

## 技术交流
QQ群：746163014

## Github Star数趋势图

[![Stargazers over time](https://starcharts.herokuapp.com/cdnbye/hlsjs-p2p-engine.svg)](https://starcharts.herokuapp.com/cdnbye/hlsjs-p2p-engine)
      
**[👉 快速开始](/usage.md)**