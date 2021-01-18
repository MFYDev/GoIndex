# GoIndex-theme-acrou

结合 [Cloudflare Workers](https://workers.cloudflare.com/) 和 [Google Drive](https://www.google.com/drive/) 的力量，你可以在Cloudflare Workers的浏览器上建立你的文件索引。

[go2index/index.js](https://github.com/MFYDev/GoIndex/go2index) 是Workers脚本的内容。

这个主题的goindex目前是基于 [Achrou/goindex-theme-acrou](https://github.com/Achrou/goindex-theme-acrou)

**删除了原仓库中的百度统计相关代码，让仓库更干净。**

[README](README.md) | [中文文档](README_zh.md)

## 预览  

MFY.GD: [https://mfy.gd/](https://mfy.gd/) 

## 特色

- [x] 👑 页面级缓存，浏览器前进后退不刷新秒加载（mac用户使用触控板体验更佳）
- [x] 🗂 多盘切换
- [x] 🔐 Http Basic Auth
- [x] 🎨 网格视图模式（文件预览）
- [x] 🎯 分页加载
- [x] 🌐 I18n（多国语言）
- [x] 🛠 Markdown/Html渲染（也许它可以成为你的博客）
- [x] 🖥 视频在线播放（支持外挂字幕vtt）
- [x] 🕹 支持自定义视频播放器（API）
- [x] 🎧 音频在线播放
- [x] 🚀 拥有更快的速度

## TODO

- [ ] 更多文件格式预览
- [ ] 让Goindex不只是一个目录索引

## 快速部署

1. 打开以下任意网址（哪个快用哪个） 

   - https://goindex-quick-install.glitch.me
   - https://goindex-install.herokuapp.com

2. 授权并获取授权码

3. 将代码部署到 [Cloudflare Workers](https://www.cloudflare.com/)

## 部署

1. 开启[Google Drive API](https://console.developers.google.com/apis/api/drive.googleapis.com/overview)
2. 创建一个 [OAuth client ID](https://console.developers.google.com/apis/credentials/oauthclient)
3. 本地安装[rclone](https://rclone.org/downloads/)
4. 使用`rclone`获取`refresh_token`
5. 下载`index.js` (https://github.com/Aicirou/goindex-theme-acrou/tree/master/go2index) 然后替换`client_id`,`client_secret`,`refresh_token` 为你刚刚获取到的
6. 把代码部署到[Cloudflare Workers](https://www.cloudflare.com/)

> 如果你写了一篇不错的文章，想分享给大家，请提交Issues，我会把链接贴在这里。

## 选项

### Video

| Option     | Type                       | Default                                                      | Description                                                  |
| ---------- | -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `api`      | String                     | `''`                                                         | 外部视频播放器api。当这个值不为空时，以下所有选项都不起作用。 |
| `autoplay` | Boolean                    | `true`                                                       | 当设置为`true`时，视频会自动播放，不过这取决于浏览器是否支持。 |
| `controls` | Array, Function or Element | `['play-large', 'restart', 'play', 'progress', 'current-time', 'duration', 'mute', 'volume', 'captions', 'settings', 'pip', 'airplay', 'download', 'fullscreen']` | 控制栏中显示哪些按钮。详细查看[CONTROLS.md](https://github.com/sampotts/plyr/blob/master/CONTROLS.md#using-default-controls) |
| `settings` | Array                      | `['quality', 'speed', 'loop']`                               | 菜单中显示哪些设置                                           |

更多选项查看 plyr [options](https://github.com/sampotts/plyr#options)

### Audio

| Option      | Type    | Default    | Description                                                  |
| ----------- | ------- | ---------- | ------------------------------------------------------------ |
| `container` | String  | `.aplayer` | 不支持修改                                                   |
| `fixed`     | Boolean | `true`     | 不支持修改                                                   |
| `autoplay`  | Boolean | `false`    | 当设置为`true`时，音频会自动播放，不过这取决于浏览器是否支持。 |
| `loop`      | String  | `'all'`    | 音频循环播放, 可选值: 'all', 'one', 'none'                   |
| `order`     | String  | `'list'`   | 音频循环顺序, 可选值: 'list', 'random'                       |
| `preload`   | String  | `'auto'`   | 预加载，可选值: 'none', 'metadata', 'auto'                   |
| `volume`    | Number  | `0.7`      | 默认音量，请注意播放器会记忆用户设置，用户手动设置音量后默认音量即失效 |
| `audios`    | Array   | `[]`       | 预设播放列表。详情查看 [FAQ](#FAQ)                           |

更多选项查看 APlayer [options](https://aplayer.js.org/#/home?id=options)

## 常见问题

> 怎么修改列表的排序方式？

修改第636行或者在代码中搜索`params.orderBy`

```javascript
－ params.orderBy = "folder,name,modifiedTime desc";
＋ params.orderBy = "modifiedTime desc";
```

> 怎么预设音频播放列表？

音频选项中添加 `audios`

```
audio: {
  audios: [
    {
      name: "Mojito",
      artist: "周杰伦",
      url: "https://xx.mp3",
      lrc: "https://xx.lrc",
      cover: "https://xx.jpg"
    }
  ]
}
```

## Lisense

[MIT](LICENSE)
