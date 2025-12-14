# 🎵 Luxury Vinyl Player | 奢华黑胶唱片播放器

<p align="center">
  <img src="https://img.shields.io/badge/Web_Audio_API-FF6B6B?style=for-the-badge" alt="Web Audio API"/>
  <img src="https://img.shields.io/badge/Canvas-2D-orange?style=for-the-badge" alt="Canvas 2D"/>
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5"/>
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3"/>
  <img src="https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge" alt="MIT License"/>
</p>

<p align="center">
  <strong>🎧 一个具有黑金奢华美学的 Web 音乐可视化播放器</strong><br/>
  3D 黑胶唱片 · 实时频谱 · 唱臂动画 · 动态光晕 · 粒子特效
</p>

<p align="center">
  ✨ <strong>纯前端实现 | 零依赖 | Hi-Fi 视觉体验</strong>
</p>


## ✨ 效果预览

### 🎬 视觉元素

| 元素 | 描述 |
|------|------|
| 💿 **3D 黑胶唱片** | 带纹路、反射、透视效果的旋转唱片 |
| 🎚️ **唱臂系统** | 播放时自动摆动的拟真唱臂 |
| 📊 **环形频谱** | 120 条金色音频频谱柱，围绕唱片旋转 |
| ✨ **粒子特效** | 低音触发的金色粒子爆发 |
| 🔆 **动态光晕** | 随音乐节拍呼吸的氛围背景 |
| 🏷️ **黑金标签** | 奢华风格的唱片中心标签设计 |
| 🎛️ **毛玻璃控件** | Glassmorphism 风格的控制面板 |

### 🎮 交互功能

| 操作 | 效果 |
|------|------|
| 📂 **加载音乐** | 点击文件夹图标选择本地音频文件 |
| ▶️ **播放/暂停** | 金色主按钮控制播放状态 |
| 🔊 **音量控制** | 滑块调节音量大小 |
| 🖱️ **鼠标移动** | 唱片 3D 透视视差效果 |
| 👆 **按住唱片** | 模拟"搓盘"效果，静音并暂停旋转 |

## 🎨 设计亮点

### 黑金奢华配色

```css
--bg-dark: #050505;           /* 深邃背景 */
--bg-light: #242426;          /* 层次渐变 */
--primary-gold: #c5a059;      /* 主金色 */
--highlight-gold: #fddb92;    /* 高光金 */
--glass-bg: rgba(20, 20, 20, 0.7);  /* 毛玻璃 */
```

### 视觉层次

```
┌─────────────────────────────────────┐
│         噪点纹理叠加层               │ ← 质感增强
├─────────────────────────────────────┤
│         动态氛围光晕层               │ ← 随音乐呼吸
├─────────────────────────────────────┤
│         径向渐变背景层               │ ← 立体空间感
├─────────────────────────────────────┤
│                                     │
│     ┌─────────┐                     │
│     │ 频谱环  │  ← Canvas 绑定到中心 │
│     │ ┌─────┐ │                     │
│     │ │唱片 │ │  ← 3D 透视旋转      │
│     │ └─────┘ │                     │
│     └─────────┘                     │
│                    🎚️ 唱臂          │ ← 播放时摆动
│                                     │
│     ┌─────────────────────┐         │
│     │   毛玻璃控制面板     │         │ ← 底部悬浮
│     └─────────────────────┘         │
└─────────────────────────────────────┘
```

## 🚀 快速开始

### 方式一：直接打开
```bash
# 下载后直接用浏览器打开
open index.html
```

### 方式二：在线体验
```bash
本项目右边栏处有在线体验链接
```

### 使用步骤
1. 点击 📂 按钮加载本地音频文件
2. 点击 ▶ 按钮开始播放
3. 享受视听盛宴 🎶

## 🛠️ 技术实现

### 核心技术栈

- **Web Audio API** - 音频分析与处理
- **Canvas 2D** - 频谱可视化绘制
- **CSS3** - 3D 变换、毛玻璃、动画
- **Vanilla JavaScript** - 零依赖实现

### 系统架构

```
┌─────────────────────────────────────────────────┐
│                 音频处理管线                     │
├─────────────────────────────────────────────────┤
│                                                 │
│  Audio File → MediaElementSource                │
│                      │                          │
│                      ▼                          │
│              ┌──────────────┐                   │
│              │   Analyser   │ ← FFT 频谱分析    │
│              │  fftSize:512 │                   │
│              └──────────────┘                   │
│                      │                          │
│                      ▼                          │
│              ┌──────────────┐                   │
│              │   GainNode   │ ← 音量控制        │
│              └──────────────┘                   │
│                      │                          │
│                      ▼                          │
│              ┌──────────────┐                   │
│              │ Destination  │ → 扬声器输出      │
│              └──────────────┘                   │
│                                                 │
└─────────────────────────────────────────────────┘
```

### 关键算法

#### 1. 环形频谱绘制
```javascript
const bars = 120;
for (let i = 0; i < bars; i++) {
    const value = dataArray[i * step];
    const percent = value / 255;
    const barLen = percent * 100;
    const rad = (Math.PI * 2 / bars) * i;
    
    // 极坐标转笛卡尔坐标
    const x1 = cx + Math.cos(rad) * radius;
    const y1 = cy + Math.sin(rad) * radius;
    const x2 = cx + Math.cos(rad) * (radius + barLen);
    const y2 = cy + Math.sin(rad) * (radius + barLen);
    
    ctx.moveTo(x1, y1);
    ctx.lineTo(x2, y2);
}
```

#### 2. 低音能量检测
```javascript
// 提取低频能量（前 10 个频段）
let bassEnergy = 0;
for(let i = 0; i < 10; i++) {
    bassEnergy += dataArray[i];
}
bassEnergy = bassEnergy / 10;

// 触发唱片缩放呼吸
const scale = 1 + (bassEnergy / 255) * 0.08;
```

#### 3. 3D 透视视差
```javascript
document.addEventListener('mousemove', (e) => {
    const x = (window.innerWidth / 2 - e.clientX) / 45;
    const y = (window.innerHeight / 2 - e.clientY) / 45;
    vinylWrapper.style.transform = `rotateY(${x}deg) rotateX(${y}deg)`;
});
```

#### 4. 搓盘效果
```javascript
vinylWrapper.addEventListener('mousedown', () => {
    isDragging = true;
    // 平滑静音
    gainNode.gain.setTargetAtTime(0, audioCtx.currentTime, 0.1);
});

document.addEventListener('mouseup', () => {
    // 平滑恢复音量
    gainNode.gain.setTargetAtTime(volume, audioCtx.currentTime, 0.1);
});
```

## 🎨 视觉定制

### 修改配色方案

```css
:root {
    /* 主背景 */
    --bg-dark: #050505;
    --bg-light: #242426;
    
    /* 金色主题 → 可改为其他颜色 */
    --primary-gold: #c5a059;      /* 尝试: #ff6b6b (红) / #6bff6b (绿) */
    --highlight-gold: #fddb92;
    
    /* 毛玻璃 */
    --glass-bg: rgba(20, 20, 20, 0.7);
    --glass-border: rgba(197, 160, 89, 0.3);
}
```

### 修改唱片标签

```html
<div class="vinyl-label">
    <div class="label-logo">Premium Sound</div>      <!-- 品牌名 -->
    <div class="label-text top">High Fidelity</div>  <!-- 顶部文字 -->
    <div class="label-text bottom">33 ⅓ RPM</div>   <!-- 底部文字 -->
</div>
```

### 调整频谱参数

```javascript
// 频谱条数量（越多越密集）
const bars = 120;

// 频谱最大长度
const barLen = percent * 100;  // 修改 100 调整长度

// 频谱起始半径
let radius = 200;
```

### 调整动画速度

```javascript
// 唱片旋转速度（度/帧）
let rotationSpeed = 1.8;

// 唱臂摆动过渡时间
transition: transform 0.8s cubic-bezier(0.4, 0.0, 0.2, 1);
```

## 📱 浏览器兼容性

| 浏览器 | 版本要求 | 支持情况 |
|--------|---------|---------|
| Chrome | 66+ | ✅ 完美支持 |
| Firefox | 60+ | ✅ 完美支持 |
| Safari | 14+ | ✅ 支持 |
| Edge | 79+ | ✅ 完美支持 |
| iOS Safari | 14+ | ⚠️ 需用户交互触发音频 |

> ⚠️ 需要支持 Web Audio API、CSS backdrop-filter

## 🎵 支持的音频格式

| 格式 | 支持情况 |
|------|---------|
| MP3 | ✅ |
| WAV | ✅ |
| OGG | ✅ |
| FLAC | ✅ (Chrome/Edge) |
| AAC | ✅ |
| M4A | ✅ |

## 🌈 扩展想法

- [ ] 添加播放列表功能
- [ ] 支持在线音乐 URL 加载
- [ ] 添加均衡器控制
- [ ] 添加更多可视化模式（波形、粒子场）
- [ ] 支持歌词显示 (LRC)
- [ ] 添加键盘快捷键
- [ ] 支持全屏模式
- [ ] 添加音乐元数据显示（专辑封面）
- [ ] PWA 离线支持

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

### 贡献流程
1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/NewFeature`)
3. 提交更改 (`git commit -m 'Add NewFeature'`)
4. 推送到分支 (`git push origin feature/NewFeature`)
5. 提交 Pull Request


## 🙏 致谢

- [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) - 音频处理能力
- 黑胶唱片美学 - 复古与现代的完美融合
- Glassmorphism 设计趋势 - 毛玻璃视觉风格

## 说明
- 代码和README皆由AI生成
- 更多作品：https://ai.feishu.cn/docx/Rnn0dQbnWo576dxc3qecgjsAnpf

---

<p align="center">
  Made with 🎵 and ☕
</p>

<p align="center">
  如果觉得项目不错，请给个 ⭐ Star 支持一下！
</p>

<p align="center">
  <strong>🎧 HIFI AUDIO SYSTEM - PREMIUM SOUND 🎧</strong>
</p>
