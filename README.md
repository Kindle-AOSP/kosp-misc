# KOSP 进展

## 目前存在的问题

- 显示驱动方面
  1. Eink刷新模式不可控，目前为全局GC16刷新
  2. 切换activity时大概率会卡5-15秒不等，目前查不出问题根源

- 系统方面

  1. 导航栏全刷，翻页按钮图标需要修改

  2. 状态栏有一块还是白色的，需要想办法改成黑色

  3. 软件包安装器安装APK速度奇慢，在某些情况下还会安装失败


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

1. 不知道怎么让gralloc与用户层交互（徐用的是SurfaceControl，但我不会）
2. 不知道怎么判断翻了几页（徐给Kobo Aura HD写的判断方案会把那些无效的刷新也算进去，不能用）
3. 最近没什么进展，基本属于半弃坑状态，希望有人接着研究
