# Camera-WaterMark PWA 部署与 iOS 使用说明

PWA（渐进式网页应用）= 不用 Mac、不用开发者账号、不用上架审核，把网页"添加到主屏幕"后像原生 App 一样全屏运行、有图标、能离线。这是在 iPhone 上最快用上本软件的方式。

---

## 一、交付目录

`E:\codex\camera-watermark-pwa\`（共 45 个文件，约 9.7MB）就是**完整站点**，整体传到任意 HTTPS 静态托管即可：

```
camera-watermark-pwa/
├─ index.html        # 应用内核（与 Windows/Android 同源）
├─ manifest.json     # PWA 清单：名称/图标/全屏模式
├─ sw.js             # Service Worker：离线缓存（页面网络优先，静态缓存优先）
├─ icons/            # 192 / 512 / 180 / maskable 图标
├─ presets/          # 品牌 logo 与动图首帧预设（离线也要用，故一并打包）
├─ cwm-logo.png / cwm.ico
```

> 所有路径均为相对路径，部署在**子目录**（如 GitHub 项目页 `xxx.github.io/仓库名/`）也能正常工作。

---

## 二、部署到 GitHub Pages（免费 + 自带 HTTPS，推荐）

iPhone 安装 PWA 必须走 **HTTPS**（本地 http 不行），GitHub Pages 自带 https，最合适。

### 方式 A：新建独立仓库（推荐，干净，不与旧 Python 仓库混）
1. 在 GitHub 新建仓库，例如 `camera-watermark-pwa`（public）；
2. 在本机 PowerShell 执行（把 `camera-watermark-pwa` 目录推上去）：
```powershell
cd "E:\codex\camera-watermark-pwa"
git init
git add .
git commit -m "Camera-WaterMark PWA v3.0"
git branch -M main
git remote add origin https://github.com/shiraijikuu/camera-watermark-pwa.git
git push -u origin main
```
3. 仓库 **Settings → Pages → Build and deployment → Source 选 Deploy from a branch**，分支选 `main / (root)`，保存；
4. 约 1 分钟后得到地址：`https://shiraijikuu.github.io/camera-watermark-pwa/`。

### 方式 B：放进现有仓库
把本目录内容放到仓库的 `docs/` 文件夹，Settings → Pages 分支选 main、目录选 `/docs`。

> 其它同样可用的托管：Cloudflare Pages、Vercel、Netlify（均免费、自带 https），把该目录拖进去即可。

---

## 三、iPhone / iPad 安装步骤（务必用 Safari）

1. 用 **Safari**（不是 Chrome/微信内置浏览器，iOS 只有 Safari 支持"添加到主屏幕"）打开上面的 https 地址；
2. 点底部**分享按钮**（方框向上箭头）→ 下滑选**「添加到主屏幕」**→ 右上角「添加」；
3. 桌面出现 **CWM 图标**，点开即**全屏独立运行**（无浏览器地址栏，体验接近 App）；
4. 第一次请在**联网状态**打开一次，Service Worker 会缓存全部资源，之后**断网也能用**。

---

## 四、iOS 上怎么保存成品图（重要差异）

iOS 网页/PWA **不允许静默写入相册**（系统隐私限制，任何网页应用都一样），所以导出流程是：
1. 点「导出当前」；
2. 系统弹出**分享面板** → 选**「存储图像」**，图片即存入相册；
3. 首次会请求访问相册的权限，允许即可。

（Android/桌面浏览器则直接下载文件；原生 Android APK 仍是一键直存相册，不受影响。）

---

## 五、更新机制

- 页面（index.html）采用**网络优先**：用户每次联网打开会拉最新版，拉不到才用离线缓存；一般关闭重开一次即更新；
- 若改动了 `sw.js` 本身或图标，把 `sw.js` 顶部的 `const CACHE='cwm-pwa-v3.0'` 版本号 +1，可强制刷新静态缓存；
- 这与原生 App 的"检查更新"相互独立：PWA 总是最新网页，无需安装包。

---

## 六、PWA 的能力边界（和原生 iOS App 的区别）

| 能力 | PWA（本方案） | 原生 iOS（需 Mac+99 美元账号） |
|---|---|---|
| 免 Mac / 免账号 / 免审核 | ✅ | ❌ |
| 桌面图标 + 全屏 + 离线 | ✅ | ✅ |
| 保存到相册 | 分享面板点「存储图像」（多一步） | 一键直存 |
| 上架 App Store | ❌ | ✅ |
| 推送通知 / 后台 / 深度系统集成 | 受限 | 完整 |
| EXIF / Canvas 水印核心功能 | ✅ 完全一致 | ✅ |

结论：自用、小范围分发、先验证 iOS 需求，PWA 完全够用；将来要正式上 App Store 再做原生版（内核可 100% 复用，只差一个 Swift 存相册插件和签名，见交接文档第 24 节）。

---

## 七、本地桌面自测（可选）
PWA 安装与 Service Worker 需要 https 或 localhost。本机预览：
```powershell
cd "E:\codex\camera-watermark-pwa"
python -m http.server 8080      # 或 npx serve .
# 浏览器开 http://localhost:8080 ，F12 → Application → Manifest/Service Workers 查看安装状态
```
（局域网 IP 的 http 地址在 iPhone 上无法注册 SW，真机安装请以第二节的 https 地址为准。）
