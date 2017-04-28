# 控件

这是渲染`Plyr`控件的标记语言。你可以使用默认控件或根据需要提供自定义的标记语言版本。

## 国际标准使用的默认控件

在初始化控件时，可以提供一个`i18n`对象作为你的选项之一，它会在渲染控件时起作用。

### 例子

```javascript
i18n: {
    restart:            "Restart",
    rewind:             "Rewind {seektime} secs",
    play:               "Play",
    pause:              "Pause",
    forward:            "Forward {seektime} secs",
    buffered:           "buffered",
    currentTime:        "Current time",
    duration:           "Duration",
    volume:             "Volume",
    toggleMute:         "Toggle Mute",
    toggleCaptions:     "Toggle Captions",
    toggleFullscreen:   "Toggle Fullscreen"
}
```

**注意**：`{seektime}`会被你配置的搜索时间或者默认搜索时间替换。举个例子，"Forward {seektime} secs"会被渲染为"Forward 10 secs"。

## 使用自定义HTML

您可以使用`html`选项指定控件的HTML内容。

模板中使用的类和数据属性应与选择器选项匹配。

你需要在你的HTML模板中添加几个占位符，这些占位符在渲染时被替换：

- `{id}` - 动态生成的播放器ID（用于表单控件）
- `{seektime}` - 在快进和快退选项中指定的寻道时间

指定自定义html时，你只能包含所需的控件。

### 例子

这是一个具有所有控件`html`选项的示例。

```javascript
var controls = ["<div class='plyr__controls'>",
    "<button type='button' data-plyr='restart'>",
        "<svg><use xlink:href='#plyr-restart'></use></svg>",
        "<span class='plyr__sr-only'>Restart</span>",
    "</button>",
    "<button type='button' data-plyr='rewind'>",
        "<svg><use xlink:href='#plyr-rewind'></use></svg>",
        "<span class='plyr__sr-only'>Rewind {seektime} secs</span>",
    "</button>",
    "<button type='button' data-plyr='play'>",
        "<svg><use xlink:href='#plyr-play'></use></svg>",
        "<span class='plyr__sr-only'>Play</span>",
    "</button>",
    "<button type='button' data-plyr='pause'>",
        "<svg><use xlink:href='#plyr-pause'></use></svg>",
        "<span class='plyr__sr-only'>Pause</span>",
    "</button>",
    "<button type='button' data-plyr='fast-forward'>",
        "<svg><use xlink:href='#plyr-fast-forward'></use></svg>",
        "<span class='plyr__sr-only'>Forward {seektime} secs</span>",
    "</button>",
    "<span class='plyr__progress'>",
        "<label for='seek{id}' class='plyr__sr-only'>Seek</label>",
        "<input id='seek{id}' class='plyr__progress--seek' type='range' min='0' max='100' step='0.1' value='0' data-plyr='seek'>",
        "<progress class='plyr__progress--played' max='100' value='0' role='presentation'></progress>",
        "<progress class='plyr__progress--buffer' max='100' value='0'>",
            "<span>0</span>% buffered",
        "</progress>",
        "<span class='plyr__tooltip'>00:00</span>",
    "</span>",
    "<span class='plyr__time'>",
        "<span class='plyr__sr-only'>Current time</span>",
        "<span class='plyr__time--current'>00:00</span>",
    "</span>",
    "<span class='plyr__time'>",
        "<span class='plyr__sr-only'>Duration</span>",
        "<span class='plyr__time--duration'>00:00</span>",
    "</span>",
    "<button type='button' data-plyr='mute'>",
        "<svg class='icon--muted'><use xlink:href='#plyr-muted'></use></svg>",
        "<svg><use xlink:href='#plyr-volume'></use></svg>",
        "<span class='plyr__sr-only'>Toggle Mute</span>",
    "</button>",
    "<span class='plyr__volume'>",
        "<label for='volume{id}' class='plyr__sr-only'>Volume</label>",
        "<input id='volume{id}' class='plyr__volume--input' type='range' min='0' max='10' value='5' data-plyr='volume'>",
        "<progress class='plyr__volume--display' max='10' value='0' role='presentation'></progress>",
    "</span>",
    "<button type='button' data-plyr='captions'>",
        "<svg class='icon--captions-on'><use xlink:href='#plyr-captions-on'></use></svg>",
        "<svg><use xlink:href='#plyr-captions-off'></use></svg>",
        "<span class='plyr__sr-only'>Toggle Captions</span>",
    "</button>",
    "<button type='button' data-plyr='fullscreen'>",
        "<svg class='icon--exit-fullscreen'><use xlink:href='#plyr-exit-fullscreen'></use></svg>",
        "<svg><use xlink:href='#plyr-enter-fullscreen'></use></svg>",
        "<span class='plyr__sr-only'>Toggle Fullscreen</span>",
    "</button>",
"</div>"].join("");

// Setup the player
plyr.setup('.js-player', {
    html: controls
});
```
