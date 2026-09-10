# Camera-WaterMark — PWA（v3.0）

> **官网 Website**：https://itangxs.top/camera-watermark/ （EXIF 相机水印 · 跨平台落地页）
> **在线试用 Try Online**：https://shiraijikuu.github.io/camera-watermark-pwa/
> **PWA 仓库 PWA Repository**：https://github.com/shiraijikuu/camera-watermark-pwa

[![官网 Website](https://img.shields.io/badge/官网-Website-blue?style=for-the-badge&logo=googlechrome&logoColor=white)](https://itangxs.top/camera-watermark/)
[![在线试用 Try Online](https://img.shields.io/badge/在线试用-Try%20Online-green?style=for-the-badge)](https://shiraijikuu.github.io/camera-watermark-pwa/)
[![GitHub](https://img.shields.io/badge/GitHub-源码-black?style=for-the-badge&logo=github&logoColor=white)](https://github.com/shiraijikuu/camera-watermark)

> 相机照片水印工具的网页版（渐进式网页应用）：无需 Mac / 开发者账号 / 上架，浏览器"添加到主屏幕"即像原生 App 一样全屏、带图标、可离线使用。
> 作者：**shiraijikuu**　|　协议：MIT

**Live / 在线地址：** https://shiraijikuu.github.io/camera-watermark-pwa/

**EN:** Installable PWA build of Camera-WaterMark v3.0 (single-file HTML5 Canvas kernel). Reads EXIF (brand / model / focal / shutter / aperture / ISO / date), adds text / image / blur-card watermarks + photo-frame templates, brand-logo & parameter-badge presets, 8 themes. Network-first Service Worker → the page is always the latest; static assets cached for offline use. Best for iPhone/iPad: Safari → Share → "Add to Home Screen".

**中文：** Camera-WaterMark v3.0 的可安装网页版（单文件 HTML5 Canvas 内核）。读取 EXIF（品牌 / 型号 / 焦距 / 快门 / 光圈 / ISO / 日期），支持文字 / 图片 / 模糊卡片水印 + 画框模板、品牌标与参数框预设、8 套主题。Service Worker 网络优先 → 页面始终最新；静态资源缓存可离线。iPhone/iPad 用 Safari「添加到主屏幕」即可全屏使用。

## 跨平台仓库 / Cross-platform repositories
- **主仓库 / Main:** [shiraijikuu/camera-watermark](https://github.com/shiraijikuu/camera-watermark)
- **Android 版 / Android:** [shiraijikuu/camera-watermark-android](https://github.com/shiraijikuu/camera-watermark-android)
- **Windows 版 / Windows:** [shiraijikuu/camera-watermark-windows](https://github.com/shiraijikuu/camera-watermark-windows)

## 使用 / Usage
1. 浏览器打开上面的 https 地址（iPhone 请用 **Safari**）；
2. iPhone：分享按钮 → **添加到主屏幕** → 桌面图标全屏运行；
3. 首次联网打开一次（Service Worker 缓存全部资源），之后断网也能用；
4. 导出：桌面/安卓浏览器直接下载；**iOS 走系统分享面板 →「存储图像」**存相册（iOS 限制网页静默写相册）。

## 站点结构与维护 / Structure & maintenance
- `index.html` — 应用内核（与桌面/移动端同源，改一处需同步各端）
- `manifest.json` / `sw.js` / `icons/` — PWA 清单、Service Worker、图标
- `presets/` — 品牌 logo 等离线素材
- 更新站点 = 改动后 push `main`（GitHub Pages 自动部署，约 1 分钟）；改了静态资源记得把 `sw.js` 顶部 `CACHE` 版本号 +1 强制刷新离线缓存
- 详细部署与 iOS 说明见仓库内 `PWA部署与iOS使用说明.md`

## 许可 / License
MIT
