# talAudio

小型，轻量vue播放器

## 1.1参数

+ src
作用： 音频资源路径
类型：String
默认值：\'\'

+ show

作用：是否展示audio原生控制面板
类型：Boolean
默认值：true

## 1.2 事件

+ readyToPlay
作用：相当于audio的canplay事件
参数类型：Object
参数示例：{duration: audio.duraion, canPlay: true}

+ playStateChanged

作用：audio播放状态变更时触发,播放时返回false
参数类型：Object
参数示例：{isPaused: true/ false}

+ currentTimeUpdated

作用：audio播放进度发生变更时触发
参数类型：Number
参数示例：100 （单位：s）

## 1.3 方法

+ play

作用：播放当前音频
参数：选填，可传递一个整数，以指定从某一时刻播放。实现快进、快退

+ pause

作用：暂停播放
参数：无

+ stop
作用：停止播放，play方法的语法糖
参数：无