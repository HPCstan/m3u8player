# m3u8player

基于 HTML + 腾讯云播放器 SDK（TCPlayer）的 m3u8 在线播放器，实现 m3u8 / HLS 与 MP4 格式视频的在线播放。

[English version](./Readme-en.md)

## 线上预览

- Cloudflare Pages：https://m3u8player-be3.pages.dev
- 自定义域名：https://m3u8player.ajwkptc.uk

## 特点

- **免 License**：使用 TCPlayer **v4.9.0**（腾讯云自 v5.0.0 起才要求 License 授权），无需注册腾讯云账号、无需申请 licenseUrl
- 支持 m3u8 / HLS 与 MP4
- 纯静态页面：无需后端、无需构建、无需依赖安装
- 支持 iframe 内嵌播放

## 文件结构

```
.
├── index.html      # 首页：播放器 + 使用说明
├── about.html      # 关于页面
├── player.html     # 可嵌入的纯播放器页面（读取 ?url= 参数）
├── images/         # 图标
└── js/             # TCPlayer 中文语言包
```

## 使用方法

1. 打开首页
2. 在输入框中填入 m3u8 或 mp4 播放地址
3. 点击输入框右侧的播放按钮即可播放

### 内嵌播放

```html
<iframe src="https://m3u8player.ajwkptc.uk/player.html?url=https://example.com/index.m3u8"></iframe>
```

`player.html` 为纯播放器页面，只读取 `url` 参数，适合直接嵌入到其他网站。

## 部署

### Cloudflare Pages（本项目使用的方式）

```bash
npx wrangler pages deploy . --project-name=m3u8player --branch=main
```

### 任意静态服务器

将目录下所有文件复制到服务器即可，访问入口为 `index.html`。

## 自定义域名

在 Cloudflare Pages 项目 → Custom domains 中添加域名，并在该域名的 DNS 中添加记录：

| Type  | Name        | Target                    | Proxy    |
| ----- | ----------- | ------------------------- | -------- |
| CNAME | m3u8player  | m3u8player-be3.pages.dev   | Proxied  |

## 关于 License

腾讯云播放器 SDK（TCPlayer）自 **v5.0.0** 起需要 License 授权才能使用，缺少 `licenseUrl` 会报错（错误码 55「缺少 License url」）。

本项目改用 **v4.9.0** —— 5.0.0 之前不需要 License 的版本，因此：

- 代码中**没有** `licenseUrl` 参数
- 播放功能完全正常，无任何授权校验

若你需要 v5.x 的新增功能（VR 播放、Web 安全插件等），可自行到
[腾讯云视立方控制台](https://console.cloud.tencent.com/vcube/web?tab=player) 申请：
基础版免费、有效期 1 年、可免费续期，以精准域名为单位授权（1 个 License 最多关联 10 个域名）。

## 出处

Fork 自 [geeeeeeeek/m3u8player](https://github.com/geeeeeeeek/m3u8player)。

## 免责声明

本项目仅提供视频播放技术，不存放、不储存任何视频内容。所有视频来源均来自互联网，
本项目不对其内容负责。若任何内容侵犯您的权益，请联系删除。
