# PYGLET–在播放器中获取当前媒体纹理

> 原文:[https://www . geesforgeks . org/pyglet-get-current-media-texture-in-player/](https://www.geeksforgeeks.org/pyglet-get-current-media-texture-in-player/)

在本文中，我们将看到如何在 python 中获取 PYGLET 模块的播放器的当前媒体纹理。Pyglet 是一个易于使用但功能强大的库，用于开发视觉丰富的图形用户界面应用程序，如游戏、多媒体等。窗口是占用操作系统资源的“重量级”对象。窗口可能显示为浮动区域，或者可以设置为充满整个屏幕(全屏)。该模块允许应用程序指定资源的搜索路径。Pyglet 可以播放 WAV 文件，如果安装了 FFmpeg，还可以播放许多其他音频和视频格式。播放由 Player 类处理，该类从 Source 对象读取原始数据，并提供暂停、查找、调整音量等方法。获取当前视频帧的纹理应该在我们每次显示一帧视频时调用，因为可能会使用多个纹理。如果当前源中没有视频，返回值将为无。

我们可以借助下面给出的命令创建一个窗口和播放器对象

```py
# creating a window
window = pyglet.window.Window(width, height, title)

# creating a player for media
player = pyglet.media.Player() 
```

> 为此，我们对玩家对象
> **使用 get_texture play 方法语法:** player.get_texture()
> **参数:**它不需要参数
> **返回:**它返回 pyglet.image.Texture 对象

下面是实现

## 蟒蛇 3

```py
# importing pyglet module
import pyglet

# width of window
width = 800

# height of window
height = 500

# caption i.e title of the window
title = "Geeksforgeeks"

# creating a window
window = pyglet.window.Window(width, height, title)

# video path
vidPath ="gfg.mp4"

# creating a media player object
player = pyglet.media.Player()

# creating a source object
source = pyglet.media.StreamingSource()

# load the media from the source
MediaLoad = pyglet.media.load(vidPath)

# add this media in the queue
player.queue(MediaLoad)

# play the video
player.play()

# on draw event
@window.event
def on_draw():

    # clear the window
    window.clear()

    # if player source exist
    # and video format exist
    if player.source and player.source.video_format:

        # get the texture of video and
        # make surface to display on the screen
        player.get_texture().blit(0, 0)

# key press event    
@window.event
def on_key_press(symbol, modifier):

    # key "p" get press
    if symbol == pyglet.window.key.P:

        # pause the video
        player.pause()

        # printing message
        print("Video is paused")

    # key "r" get press
    if symbol == pyglet.window.key.R:

        # resume the video
        player.play()

        # printing message
        print("Video is resumed")

# seek video at time stamp = 4
# and pause the video
player.seek(4)
player.pause()

# getting texture of the video
value = player.get_texture()

# printing value of texture
print("Texture : " + str(value))

# run the pyglet application
pyglet.app.run()
```

![](img/ef4bf67a028f1627d00fa5846db20f45.png)

```py
Texture : 
```