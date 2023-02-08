# KOSP 进展

## 目前存在的问题（Build 0.1）

- 显示驱动方面

  1.Eink刷新模式不可控，目前为全局GC16_Fast刷新（刷不出灰度），需要改成GL16_Fast刷新并加上控制功能
  
  2.切换activity时大概率会卡5-15秒不等，目前查不出问题根源（问题估计和2.3一样，epdc刷新动作阻塞了安装进程）
  
  【如果app是首次打开则不会出现卡顿，如果是从后台调出则会出现卡顿】
  
  3.Surfacecontrol.configDisplay已经正常工作，可以把参数从Java层传递到FslHwcomposer内，但是没有办法传入Gralloc内使其响应刷新模式切换的需求
  
  4.手动全刷触发为configDisplay（1001，1），触发后要给gralloc传递一个用GC16_fast全刷的信号
  
  5.加入点击/滑动事件的检测，参考徐

- 系统方面

  1.导航栏全刷，翻页按钮图标需要缩小到正常大小
  
  2.状态栏有一块还是白色的，需要想办法改成黑色
  
  3.软件包安装器安装APK速度奇慢，在某些情况下还会安装失败（见1.2）

## To-Do List

- [ ] 修复上述Bug

- [ ] 加入翻指定页数之后全刷的功能

- [ ] 加入用户修改Eink刷新模式功能

- [ ] 加入手动全刷功能

- [ ] 加入休眠屏保，且用户可自定义壁纸

- [ ] 把这套安卓移植到Wario Platform

- [ ] 显示驱动加上帧合并，避免残影的出现

- [x] 修改分区表，为以后的双系统做准备

  Number  Start   End     Size    File system  Name      Flags
   1      32.0MB  46.7MB  14.7MB               boot      msftdata
   2      47.2MB  64.0MB  16.8MB               recovery  msftdata
   3      64.0MB  70.3MB  6291kB               config    msftdata
   4      70.3MB  71.3MB  1049kB               misc      msftdata
   5      71.3MB  591MB   520MB   ext4         system
   6      591MB   600MB   8389kB  ext4         cache
   7      600MB   3909MB  3309MB  ext4         userdata

  （eMMC前端留32M放原系统Kernel，Diags Kernel等）

## 目前存在的难点

1. 1.2与2.3的奇怪卡顿问题难debug
2. 不知道怎么让HWcomposer和Gralloc之间相互传递参数
3. 最近没什么进展，基本属于半弃坑状态，希望有人接着研究
