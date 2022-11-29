# ParamountHelper

Paramount+ iOS App 外挂字幕和强制1080p插件

**本插件与DualSubs字幕插件可能存在冲突，请按需启用。**
**我使用的Essential套餐没发现广告，所以暂时不更新去广告功能。请发现广告的朋友向我反馈。**

## 外挂字幕

- ### QuanX配置
```
hostname = pubads.g.doubleclick.net, link.theplatform.com, vod*.cbsaavideo.com

# 外挂srt字幕 pubads.g.doubleclick.net, link.theplatform.com, vod*.cbsaavideo.com
^https:\/\/link\.theplatform\.com\/s\/\w+\/\w+\?format=SMIL url script-response-body https://raw.githubusercontent.com/liunice/ParamountHelper/master/paramount_helper.js
^https:\/\/pubads\.g\.doubleclick\.net\/ondemand\/hls\/content\/.*?\/\d+\-\d+\.vtt$ url script-response-body https://raw.githubusercontent.com/liunice/ParamountHelper/master/paramount_helper.js
^https:\/\/vod\-.*?\.cbsaavideo\.com\/intl_vms\/.*?\/seg_\d+\.vtt$ url script-response-body https://raw.githubusercontent.com/liunice/ParamountHelper/master/paramount_helper.js
```

- ### 字幕文件的放置
  **【前置步骤】**  
  在 ``iCloud云盘/Quantumult X/Data``目录下新建``Subtitles``目录，如果没有``Data``目录请先新建, 注意字母大小写。  
  **【文件放置】**  
  我们以Paramount+上的剧集 ``Tulsa King``为例。  
    1. 在Paramount+上播放``Tulsa King``第一集，等待顶部出现``正在播放剧集``的通知，注意观察通知框上的剧集名称，应为``Tulsa King``
    2. 在``iCloud云盘/Quantumult X/Data/Subtitles``目录下新建文件夹``Tulsa King``
    3. 如果你观看的是第1季，请在``Tulsa King``下新建文件夹``S01``。**注意字母S为大写，且后面的数字固定为两位数。**
    4. 如果你观看的是第1季第1集，请将srt字幕文件复制到``Tulsa King/S01``目录下，并重命名为``S01E01.srt``，**注意字母S和E均为大写，且后面的数字固定为两位数。**  
    **如果你在Mac上复制文件，请在iPhone上打开``文件``App并确认修改已云同步。**

- ### 字幕时间轴的微调
  同样以上面的``Tulsa King``为例。如果你觉得字幕滞后了，想将所有字幕往前调3秒，步骤如下：  
    1. 在``Tulsa King/S01``文件夹下新建文件``subtitle.conf``
    2. 在``subtitle.conf``中添加设置项：``offset=-3000``  
       **注意这里的offset值的单位为毫秒**

  类似的，如果你只想将S01E01往后调3秒，步骤如下：
    1. 在``Tulsa King/S01``文件夹下新建文件``subtitle.conf``
    2. 在``subtitle.conf``中添加设置项：``S01E01:offset=3000``  
       **注意offset前的符号为英文冒号，此设置可以与前面的设置项共存**
  
  部分网友反馈下载的字幕在观看时发现时快时慢，即便添加了时间轴的配置还是对不上。这种情况一般不是插件问题，而是**你下载的字幕和Paramount+的片源不匹配，建议换一个字幕组的再试试。**
  比如Tulsa King的字幕可以从SubHD网站下载，字幕文件名格式为``tulsa.king.s01e01.2160p.web.h265-glhf``，该字幕的时间轴完美匹配Paramount+片源。如果下载到的是ASS格式，可通过第三方工具将ASS转成SRT格式再使用。

## 强制1080p
本功能适用于网络不佳且不希望app在缓冲时频繁调整到低码率导致画面模糊的用户。启用后画面会保持最高1080p画质，负作用是首次缓冲和每次快进时可能需要多等待两到三秒，具体取决于你的网络状况。
```
hostname = vod*.cbsaavideo.com

# 强制1080p vod*.cbsaavideo.com
^https:\/\/vod.*?\.cbsaavideo\.com\/intl_vms\/.*?\/master\.m3u8\? url script-response-body https://raw.githubusercontent.com/liunice/ParamountHelper/master/paramount_helper.js
```

## 插件通知的禁用

本插件默认开启通知。如需禁用，请按以下步骤操作：  
    1. 在``iCloud云盘/Quantumult X/Data/Subtitles``目录下新建文件``helper.conf``  
    2. 在``helper.conf``中添加设置项：``notify=false``  
**注意**  
    1. 一般不建议禁用通知。禁用通知后插件不会提示正在播放的剧集名称，这样你将不知道如何建立字幕文件夹。  
    2. 如果你在Mac上修改配置，请在iPhone上打开``文件``App并确认修改已云同步。

## 注意
    - 本插件暂只支持QuanX，后续会支持Surge
    - 本插件暂只支持电视剧，不支持电影
    - 仅支持srt格式的字幕
    - 字幕文件建议为utf-8编码，否则可能无法解析
    - 本插件与DualSubs字幕插件可能存在冲突，请按需启用

## 反馈和建议
不建议在github上提交issue，我不一定看得到。欢迎加入官方TG群组：https://t.me/+W6aJJ-p9Ir1hNmY1v