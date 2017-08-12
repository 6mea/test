# 简介

一个 Cytoid 关卡实际就是将所有自制元素（音乐、背景、关卡信息...）打包成一个 `.cytoidlevel` 文件。`.cytoidlevel` 格式的文件可以直接在 Cytoid 中打开和导入，有点像 [osu!](https://osu.ppy.sh/help/wiki/osu!_File_Formats) 里的 `.osz` 曲包文件。

一个 Cytoid 关卡至少由以下四项组成：
- **音乐文件**

    目前仅支持 `.mp3` 格式。如果在 Cytoid 里无法正常播放，请用格式转换工具将文件转换成 `MPEG` 格式。

    建议文件小于 3 MB，否则加载时间会明显变长。并且**强烈建议**剪一段 30 秒，大小压缩在 500 KB 以内的音乐试听文件。

- **背景文件**

    目前支持 `.jpg` 和 `.png` 格式。

    建议选择小于 2 MB 的 `.jpg` 文件。分辨率在 1920px * 1080px 以上为佳。

- **谱面文件**

    目前仅支持 Cytus 格式，或 [Rayark v2 改](https://github.com/TigerHix/Cytoid/wiki/Chart-formats) 格式。**现有的自制谱面无需任何修改即可被 Cytoid 读取。**

- **`level.json` 关卡信息文件**

    此 [JSON](https://json.org) 文件声明必要的关卡信息。

# level.json

以下详细分析一个示例 `level.json` 文件。别担心，超简单。

```
{
  
  "version": 1, // 谱面的版本。必须为整数。
  
  "id": "decnoe.hopes_and_dreams", // 关卡的唯一标识符。详情请见下文。
  "title": "Hopes and Dreams", // 关卡的标题。一般来说，应该是音乐的标题。
  "artist": "Toby Fox", // 曲师的名字。
  "illustrator": "masyu_0331", // 画师的名字。
  "charter": "Decnoe", // 谱师的名字。
  
  "music": {
    "path": "Hopes and Dreams.mp3" // 音乐文件的相对路径。
  },
  "music_preview": {
    "path": "preview.mp3" // 音乐试听文件的相对路径。
  },
  "background": {
    "path": "background.jpg" // 背景文件的相对路径。
  },
  "charts": [ // 在此最多可以定义三个谱面。
    {
      "type": "easy", // 谱面的类型："easy"，"hard" 或者 "extreme"，注意全部为小写。
      "difficulty": 8, // 如果将谱面放到 Cytus 里，你觉得它是哪个等级？填 9 以上也是可以哒。
      "path": "chart.easy.txt" // 谱面文件的相对路径。
    },
    {
      "type": "hard",
      "difficulty": 9,
      "path": "chart.hard.txt",
      "music_override" : {
        "path": "Hopes and Dreams (Alt).mp3" // 你可以覆盖掉某个难度的音乐文件，隐藏曲什么的。
      }
    }
  ]
  
}
```

目录结构：

```
.
├── background.jpg
├── chart.easy.txt
├── chart.hard.txt
├── Hopes and Dreams.mp3
├── Hopes and Dreams (Alt).mp3
└── level.json
```

虽然应该很明显，不过文件名并不需要参照 `background.jpg` 和 `chart.xxx.txt` 这样的格式。只要 `level.json` 里相对路径指向正确的文件就可以了。

# 唯一标识符

`level.json` 中的 `id` 参数在本地测试时无需填写，除非你想上传到 [CytoidDB](http://cytoid.io/browse/)（顺带一提，强烈鼓励上传分享喔 ヽ(●^∀^●)ﾉ）。`id` 相当于关卡的唯一标识符，毕竟总不能用音乐标题作为辨认——想象一下十个谱师都做同一首曲子的情况。（有编程经验的同学，`id` 实际上就是 Java 里的 `package` 或 C++ 里的 `namespace`。）

`id` 必须仅由 `a~z`、`0~9`、`.` 和 `_` 组成。这些 `id` 是合法的：

- io.cytoid.tutorial
- john_doe.freedom_dive
- decnoe.undertale.hopes_and_dreams

# 创建你的第一个关卡

解释了这么多，试试创建一个关卡并导进 Cytoid 吧：

1. 将音乐、背景、谱面文件全部塞一个文件夹里。建议文件夹名称为关卡的唯一标识符。
2. 创建 `level.json` 文件，不妨下载一份[模板](http://cytoid.io/level.json)，填填空，小修小补，就OK了。

最后只需要复制到设备里就大功告成：

- Android：将关卡文件夹拖到外部存储空间（通常是 `sdcard`）的 `Cytoid` 文件夹里。
- iOS：连接设备，打开 iTunes，然后 `应用 -> iTunes 文件分享 -> Cytoid`，将关卡文件夹拖到右边的文件目录里。

打开 Cytoid，你就可以见到你的关卡优雅地出现在关卡选择菜单了。👍

# 上传到 CytoidDB

[CytoidDB](http://cytoid.io/browse) 是一个分享自制关卡的地方。谱面信息会[自动从关卡文件中读取展示](http://cytoid.io/browse/io.cytoid.glow_dance)，并且不像普通网盘全是广告（。

步骤也很简单：

1. 将所有关卡文件压缩成 `.zip`。确保压缩关卡文件本身而不是关卡文件夹，因为 `level.json` 应该在压缩包的根目录下。
2. 创建一个 CytoidDB 账户。
3. 开始上传吧。上传页面会告诉你你的关卡文件出了什么问题（如果有的话）。

然后将页面地址分享出去即可。CytoidDB 会修改你的 `.zip` 后缀名为 `.cytoidlevel`，这样别人下载的时候就可以直接打开导入到 Cytoid 了。方便吧？