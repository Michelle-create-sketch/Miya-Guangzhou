# 咪呀广州 🐾 智能路线规划系统

广州全区美食 + City Walk 路线智能规划页面，基于高德地图 JS API 构建。

## 🚀 部署到 GitHub Pages（最简单，零成本）

1. 在 GitHub 新建一个仓库，例如 `miya-guangzhou`。
2. 把本目录下的 `index.html` 上传到仓库根目录（直接拖拽到 GitHub 网页上传即可，文件名必须是 `index.html`）。
3. 进入仓库 **Settings → Pages**。
4. 在 "Build and deployment" 中，Source 选择 **Deploy from a branch**，Branch 选择 `main`（或 `master`），目录选择 `/ (root)`，点击 Save。
5. 等待 1-2 分钟，页面会发布在：
   `https://你的GitHub用户名.github.io/仓库名/`

也可以用命令行一次性推送：

```bash
git init
git add index.html README.md
git commit -m "init: 咪呀广州路线规划页面"
git branch -M main
git remote add origin https://github.com/你的用户名/miya-guangzhou.git
git push -u origin main
```

然后按上面第 3-4 步在仓库设置里开启 Pages 即可。

## ⚠️ 部署前必须做的一件事：高德地图 Key 安全设置

页面里使用的高德 JS API Key 是写死在前端代码里的，任何人查看网页源码都能看到。**高德地图本身就是这样设计的（Key 必须暴露在前端才能调用 JS API）**，但你需要在高德开放平台后台给这个 Key **绑定白名单域名**，否则别人盗用你的 Key 会消耗你的调用额度：

1. 登录 [高德开放平台控制台](https://console.amap.com/)。
2. 找到本项目使用的 Key（代码里 `key=eba0d43a4a695f875393985a52d0d8bc` 对应的应用）。
3. 进入该应用的「设置」，在「Web端(JS API)」的 **白名单** 中添加你的 GitHub Pages 域名，例如：
   - `你的用户名.github.io`
4. 保存后即可生效，未在白名单内的域名访问会被高德拒绝调用。

> 如果这个 Key 不是你自己申请的，建议去 [高德开放平台](https://lbs.amap.com/) 免费申请一个属于你自己的 Key 和安全密钥（`securityJsCode`），替换掉 `index.html` 头部 `<script>` 中的：
> ```js
> window._AMapSecurityConfig = { securityJsCode: '你的安全密钥' }
> ```
> 以及 `<script src="https://webapi.amap.com/maps?v=2.0&key=你的Key&plugin=...">` 中的 `key` 参数。

## 📂 项目结构

```
miya-guangzhou-site/
├── index.html   # 唯一页面文件，包含全部 HTML/CSS/JS，无需构建工具
└── README.md    # 本说明文档
```

纯静态单文件页面，不依赖任何打包工具（无需 npm / webpack），上传即可直接访问，天然适合 GitHub Pages、Vercel、Netlify、Cloudflare Pages 等任意静态托管平台。

## ✅ 功能一览

- 城区覆盖广州全部 11 区（荔湾/越秀/天河/海珠/白云/黄埔/番禺/花都/南沙/增城/从化），每区餐厅与景点严格对应所选区域
- 8 种偏好口味 + 10 种出行场景（晴空漫步、夜幕观光、情侣约会、黄昏落日、亲子周末、闺蜜聚会、人少出片、雨天室内、遛宠漫游、一人毕业旅）
- 高德地图实时天气、步行路线规划、卫星图层 / 实时路况切换
- 地图站点名称点击 3D 翻转查看实拍图，路线列表点击弹出图文翻转卡片
- 一键调起高德地图 App 导航
- 自动生成的旅途手账本，支持手写心情随笔与照片上传（浏览器本地保存）
- 移动端响应式适配

## 🔧 本地预览

无需任何依赖，直接双击 `index.html` 用浏览器打开即可预览（部分浏览器对本地 file:// 协议下的 AMap 接口可能有跨域限制，建议用本地静态服务器预览，例如）：

```bash
# 任选一种方式在本目录下启动本地服务器
python3 -m http.server 8080
# 或
npx serve .
```

然后浏览器打开 `http://localhost:8080` 即可。
