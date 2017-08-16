## 模拟按键/输入

在 `adb shell` 里有个很实用的命令叫 `input`，通过它可以做一些有趣的事情。

`input` 命令的完整 help 信息如下：

```sh
Usage: input [<source>] <command> [<arg>...]

The sources are:
      mouse
      keyboard
      joystick
      touchnavigation
      touchpad
      trackball
      stylus
      dpad
      gesture
      touchscreen
      gamepad

The commands and default sources are:
      text <string> (Default: touchscreen)
      keyevent [--longpress] <key code number or name> ... (Default: keyboard)
      tap <x> <y> (Default: touchscreen)
      swipe <x1> <y1> <x2> <y2> [duration(ms)] (Default: touchscreen)
      press (Default: trackball)
      roll <dx> <dy> (Default: trackball)
```

比如使用 `adb shell input keyevent <keycode>` 命令，不同的 keycode 能实现不同的功能，完整的 keycode 列表详见 [KeyEvent](https://developer.android.com/reference/android/view/KeyEvent.html)，摘引部分我觉得有意思的如下：

|keyname             | keycode | 含义                     |
|--------------------|---------|-------------------------|
|KEYCODE_UNKNOWN     | 0       |                         |
|KEYCODE_MENU        | 1       |                         |
|KEYCODE_SOFT_RIGHT  | 2       |                         |
|KEYCODE_HOME        | 3       | HOME 键                  |
|KEYCODE_BACK        | 4       | 返回键                   |
|KEYCODE_CALL        | 5       | 打开拨号应用              |
|KEYCODE_ENDCALL     | 6       | 挂断电话                  |
|KEYCODE_0           | 7       | 0                        |
|KEYCODE_1           | 8       | 1                        |
|KEYCODE_2           | 9       | 2                        |
|KEYCODE_3           | 10      | 3                        |
|KEYCODE_4           | 11      | 4                        |
|KEYCODE_5           | 12      | 5                        |
|KEYCODE_6           | 13      | 6                        |
|KEYCODE_7           | 14      | 7                        |
|KEYCODE_8           | 15      | 8                        |
|KEYCODE_9           | 16      | 9                        |
|KEYCODE_STAR        | 17      | 按键'*'                  |
|KEYCODE_POUND       | 18      | 按键'#'                  |
|KEYCODE_DPAD_UP     | 19      | 导航键 向上               |
|KEYCODE_DPAD_DOWN   | 20      | 导航键 向下               |
|KEYCODE_DPAD_LEFT   | 21      | 导航键 向左               |
|KEYCODE_DPAD_RIGHT  | 22      | 导航键 向右               |
|KEYCODE_DPAD_CENTER | 23      | 导航键 确定键              |
|KEYCODE_VOLUME_UP   | 24      | 增加音量                  |
|KEYCODE_VOLUME_DOWN | 25      | 降低音量                  |
|KEYCODE_POWER       | 26      | 电源键                    |
|KEYCODE_CAMERA      | 27      | 拍照（需要在相机应用里）    |
|KEYCODE_CLEAR       | 28      |                          |
|KEYCODE_A           | 29      |                          |
|KEYCODE_B           | 30      |                          |
|KEYCODE_C           | 31      |                          |
|KEYCODE_D           | 32      |                          |
|KEYCODE_E           | 33      |                          |
|KEYCODE_F           | 34      |                          |
|KEYCODE_G           | 35      |                          |
|KEYCODE_H           | 36      |                          |
|KEYCODE_I           | 37      |                          |
|KEYCODE_J           | 38      |                          |
|KEYCODE_K           | 39      |                          |
|KEYCODE_L           | 40      |                          |
|KEYCODE_M           | 41      |                          |
|KEYCODE_N           | 42      |                          |
|KEYCODE_O           | 43      |                          |
|KEYCODE_P           | 44      |                          |
|KEYCODE_Q           | 45      |                          |
|KEYCODE_R           | 46      |                          |
|KEYCODE_S           | 47      |                          |
|KEYCODE_T           | 48      |                          |
|KEYCODE_U           | 49      |                          |
|KEYCODE_V           | 50      |                          |
|KEYCODE_W           | 51      |                          |
|KEYCODE_X           | 52      |                          |
|KEYCODE_Y           | 53      |                          |
|KEYCODE_Z           | 54      |                          |
|KEYCODE_COMMA       | 55      | ,                        |
|KEYCODE_PERIOD      | 56      | .                        |
|KEYCODE_ALT_LEFT    | 57      |                          |
|KEYCODE_ALT_RIGHT   | 58      |                          |
|KEYCODE_SHIFT_LEFT  | 59      |                          |
|KEYCODE_SHIFT_RIGHT | 60      |                          |
|KEYCODE_TAB         | 61      | Tab键                    |
|KEYCODE_SPACE       | 62      | 空格键                    |
|KEYCODE_SYM         | 63      |                          |
|KEYCODE_EXPLORER    | 64      | 打开浏览器                |
|KEYCODE_ENVELOPE    | 65      | 打开邮件                  |
|KEYCODE_ENTER       | 66      | 回车键                    |
|KEYCODE_DEL         | 67      | 向前删除键                |
|KEYCODE_GRAVE       | 68      | `                        |
|KEYCODE_MINUS       | 69      | -                        |
|KEYCODE_EQUALS      | 70      | =                        |
|KEYCODE_LEFT_BRACKET | 71     | [                        |
|KEYCODE_RIGHT_BRACKET| 72     | ]                        |
|KEYCODE_BACKSLASH   | 73      | \                        |
|KEYCODE_SEMICOLON   | 74      | ;                        |
|KEYCODE_APOSTROPHE  | 75      | '                        |
|KEYCODE_SLASH       | 76      | /                        |
|KEYCODE_AT          | 77      | @                        |
|KEYCODE_NUM         | 78      |                          |
|KEYCODE_HEADSETHOOK | 79      |                          |
|KEYCODE_FOCUS       | 80      | 对焦键                    |
|KEYCODE_PLUS        | 81      | +                        |
|KEYCODE_MENU        | 82      | 菜单键                    |
|KEYCODE_NOTIFICATION| 83      | 通知键                    |
|KEYCODE_SEARCH      | 84      | 搜索键                    |
|KEYCODE_MEDIA_PLAY_PAUSE  | 85  | 播放/暂停               |
|KEYCODE_MEDIA_STOP        | 86  | 停止播放                |
|KEYCODE_MEDIA_NEXT        | 87  | 播放下一首               |
|KEYCODE_MEDIA_PREVIOUS    | 88  | 播放上一首               |
|KEYCODE_MEDIA_REWIND      | 89  | 快退                    |
|KEYCODE_MEDIA_FAST_FORWARD| 90  | 快进                    |
|KEYCODE_MUTE        | 91      | 话筒静音键                 |
|KEYCODE_PAGE_UP     | 92      | 向上翻页键                 |
|KEYCODE_PAGE_DOWN   | 93      | 向下翻页键                 |
|KEYCODE_ESCAPE      | 111     | ESC键                     |
|KEYCODE_FORWARD_DEL | 122     | 移动光标到行首或列表顶部     |
|KEYCODE_CAPS_LOCK   | 115     | 大写锁定键                 |
|KEYCODE_SCROLL_LOCK | 116     | 滚动锁定键                 |
|KEYCODE_BREAK       | 121     | Break / Pause键           |
|KEYCODE_MOVE_HOME   | 122     | 光标移动到开始键            |
|KEYCODE_MOVE_END    | 123     | 移动光标到行末或列表底部     |
|KEYCODE_INSERT      | 124     | 插入键                     |
|KEYCODE_MEDIA_PLAY  | 126     | 恢复播放                   |
|KEYCODE_MEDIA_PAUSE | 127     | 暂停播放                   |
|KEYCODE_MEDIA_CLOSE | 128     | 多媒体键 >> 关闭            |
|KEYCODE_MEDIA_EJECT | 129     | 多媒体键 >> 弹出            |
|KEYCODE_MEDIA_RECORD| 130     | 多媒体键 >> 录音            |
|KEYCODE_NUM_LOCK    | 143     | 小键盘锁                    |
|KEYCODE_VOLUME_MUTE | 164     | 扬声器静音键                |
|KEYCODE_ZOOM_IN     | 168     | 放大键                      |
|KEYCODE_ZOOM_OUT    | 169     | 缩小键                      |
|KEYCODE_SETTINGS    | 176     | 打开系统设置                 |
|KEYCODE_APP_SWITCH  | 187     | 切换应用                    |
|KEYCODE_CONTACTS    | 207     | 打开联系人                   |
|KEYCODE_CALENDAR    | 208     | 打开日历                     |
|KEYCODE_MUSIC       | 209     | 打开音乐                     |
|KEYCODE_CALCULATOR  | 210     | 打开计算器                   |
|KEYCODE_BRIGHTNESS_DOWN | 220 | 降低屏幕亮度                 |
|KEYCODE_BRIGHTNESS_UP   | 221 | 提高屏幕亮度                 |
|KEYCODE_SLEEP       | 223     | 系统休眠                     |
|KEYCODE_WAKEUP      | 224     | 点亮屏幕                     |
|KEYCODE_VOICE_ASSIST| 231     | 打开语音助手                  |
|KEYCODE_SOFT_SLEEP  | 276     | 如果没有 wakelock 则让系统休眠 |


下面是 `input` 命令的一些用法举例。

### 电源键

命令：

```sh
adb shell input keyevent 26
```

执行效果相当于按电源键。

### 菜单键

命令：

```sh
adb shell input keyevent 82
```

### HOME 键

命令：

```sh
adb shell input keyevent 3
```

### 返回键

命令：

```sh
adb shell input keyevent 4
```

### 音量控制

增加音量：

```sh
adb shell input keyevent 24
```

降低音量：

```sh
adb shell input keyevent 25
```

静音：

```sh
adb shell input keyevent 164
```

### 媒体控制

播放/暂停：

```sh
adb shell input keyevent 85
```

停止播放：

```sh
adb shell input keyevent 86
```

播放下一首：

```sh
adb shell input keyevent 87
```

播放上一首：

```sh
adb shell input keyevent 88
```

恢复播放：

```sh
adb shell input keyevent 126
```

暂停播放：

```sh
adb shell input keyevent 127
```

### 点亮/熄灭屏幕

可以通过上文讲述过的模拟电源键来切换点亮和熄灭屏幕，但如果明确地想要点亮或者熄灭屏幕，那可以使用如下方法。

点亮屏幕：

```sh
adb shell input keyevent 224
```

熄灭屏幕：

```sh
adb shell input keyevent 223
```

### 滑动解锁

如果锁屏没有密码，是通过滑动手势解锁，那么可以通过 `input swipe` 来解锁。

命令（参数以机型 Nexus 5，向上滑动手势解锁举例）：

```sh
adb shell input swipe 300 1000 300 500
```

参数 `300 1000 300 500` 分别表示`起始点x坐标 起始点y坐标 结束点x坐标 结束点y坐标`。

### 输入文本

在焦点处于某文本框时，可以通过 `input` 命令来输入文本。

命令：

```sh
adb shell input text hello
```

现在 `hello` 出现在文本框了。
