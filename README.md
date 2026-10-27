# 冲床图纸图床（GitHub Pages / raw 直链）

本仓库仅存放冲床规格参数小程序的图纸 PNG，供 `<image>` 通过 https 直链加载。

## 目录

- `drawings/*.png` —— 127 张图纸（下工作台 / 上工作台 / 外形图 / 基础图）
- `drawings.json` —— 文件名索引（供索引页或脚本核对）
- `index.html` —— 图纸索引页（可按仓库名切换 `raw` 与 `pages` 两种直链）

## 直链规则

```
https://raw.githubusercontent.com/<owner>/<repo>/main/drawings/<文件名>.png
```

或（GitHub Pages，需在仓库 Settings → Pages 里开启，Source 选 main / root）：

```
https://<owner>.github.io/<repo>/drawings/<文件名>.png
```

小程序侧只需要改 `punch-press-miniprogram/utils/image-host.js` 的 `base` 与 `dir`：

```js
base: "https://raw.githubusercontent.com/<owner>/<repo>/main",
dir:  "drawings",
query: "",
wechatBlocked: false,
```

改完务必自检：`node tools/check-host.mjs --ua`（必须看到「✔ 微信 UA 可正常取到 PNG」）。

## 注意

- 仓库必须是 **public**，否则 raw 直链返回 404。
- raw.githubusercontent.com 在国内偶有波动，若小程序端出现零星加载失败，可改用 jsDelivr：
  `https://cdn.jsdelivr.net/gh/<owner>/<repo>@main/drawings/<文件名>.png`（实测不按 UA 拦截，且国内通常更快）。
- 新增/替换图纸：把 PNG 放进 `drawings/`，同步更新 `drawings.json`，提交推送即可。
