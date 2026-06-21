# 2025-2026学年春季学期《游戏音频设计》期末作品说明
## 一、项目概述

选题为项目二：Unreal & Wwise 音频设计实践。基于 Unreal Engine 5 与 Wwise 音频中间件，完成空间音频（Room & Portal）、环境声、篝火物件音效及角色脚步声四大模块的设计实现，构建具备室内外声学差异的动态音频场景。

---

## 二、模块开发过程

### 模块一：空间音频 — Room & Portal

室内外各放置 AkSpatialAudioVolume，勾选 Enable Room 和 Enable Late Reverb；室内 Volume 的 Aux Bus 属性关联 Wwise 中挂载 RoomVerb 效果器的 Aux Bus。门口放置 AkAcousticPortal，启用 Fit To Geometry，Initial State 设为 Enabled。测试时室内外声音混响呈平滑过渡。

 
 
---

### 模块二：基础环境声 — Ambience

Wwise 中创建 Sound SFX，启用 Looping 并设循环区间；开启 3D Spatialization，Attenuation 曲线设为 0 dB（0–5 m）至 -60 dB（100 m）线性衰减。创建 Play Event，在 Unreal 场景 Actor 上调用触发。

 
---

### 模块三：篝火物件 — 3D Object

使用白色立方体代替篝火模型，创建 Random Container 容纳多组燃烧素材，Pitch/Volume 开启 Randomizer 增加变化。设置 3D 定位及衰减。创建 Play Event，在 Unreal 中将 AkComponent 挂载到篝火 Mesh 上，摆放于室内，验证混响效果。

 
 
---

### 模块四：角色脚步声 — Footstep

Wwise 侧：创建 Switch Group Footstep_Material，含 Dirt、Rock、Wood、Grass 四个 Switch。Switch Container 下为每种材质建 Random Container 存放脚步声采样，完成映射。

Unreal 侧：Project Settings 中新增四种 Surface Type，分别创建 Physical Material 并赋给场景中对应材质的地面。在跑步动画脚掌触地处添加 AkEvent Notify，对 Notify 进行改造，通过射线检测获取 Hit.PhysMaterial 的 Surface Type，匹配后调用 SetSwitch 再播放 Event。

 
 

 
## 三、GitHub 仓库

项目工程、Wwise 工程及说明文档已上传至个人 GitHub 公开仓库：
