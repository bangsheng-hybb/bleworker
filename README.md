# 🛀 蓝牙水控 bleworker

深圳市常工电子“蓝牙水控器”控制程序的本地 Web 实现，面向国内高校宿舍热水器。  
基于小程序 `pages/index` 的 `buildCmdString` / `sendCommandAndWait` 协议逆向还原，支持**免费用水（isFreeWater）**一键开闸。

本项目参考 [celesWuff/waterctl](https://github.com/celesWuff/waterctl) 的使用体验与文档结构，面向浏览器 Web Bluetooth 场景提供单页离线可用的控制界面。

## 🏃 使用

- 🌎 开始使用（GitHub Pages）： https://bangsheng-hybb.github.io/bleworker/
- 不能用？请先看看「疑难解答」： [FAQ.md](./FAQ.md)
- 仓库地址： https://github.com/bangsheng-hybb/bleworker

> Web Bluetooth 需要 **HTTPS** 或 `localhost`。手机端推荐 Chrome / Edge 打开。

## ✨ 特性

- 🌐 真正离线可用：单页 `index.html`，部署后不依赖后端
- 🖕 完全脱离“微信”小程序，浏览器直连蓝牙水表
- 🆓 支持**免费用水模式**（对齐小程序 `isFreeWater`，不走云余额 / `rateOrder`）
- ⚡ 一键开启：选设备 → `23/00` 同步查询 → `85/00` 开闸
- 🔒 关闭流程对齐小程序：用水中先 `86/00` 结束用水，再 `87/00` 仅关闭
- 🧪 内置高级面板：UUID / 命令字 / 写特征方式 / 诊断日志可调
- 📱 支持 Windows / Linux / macOS / Android（iOS 需 Bluefy）
- 👍 开放源代码

## 🧭 操作说明

1. 用支持 Web Bluetooth 的浏览器打开页面
2. 确认已勾选「免费用水模式」（默认开启）
3. 点击 **开启**，在系统弹窗中选择附近水表
4. 连接成功后自动同步并开闸；界面显示「已开启 · 请立即开龙头」
5. 用完后点击 **关闭**：先结束用水，再关闭阀门

### 协议要点

帧格式：`FE + LEN + payload + CS`，其中 `CS` 为 payload 字节和校验。

| 命令 | 含义 | 说明 |
| --- | --- | --- |
| `23 / 00` | 查询 / 同步 | 连接后自动发送 |
| `85 / 00` | 开始用水 | 默认开闸命令 |
| `86 / 00` | 结束用水 | 用水中关闭时先发 |
| `87 / 00` | 仅关闭 | 最终关阀 |

## 🧰 本地打开

```bash
# 克隆仓库
git clone https://github.com/bangsheng-hybb/bleworker.git
cd bleworker

# 任意静态服务器即可，例如：
python -m http.server 8080
# 然后打开 http://localhost:8080
```

也可直接用支持本地文件或 Live Server 的方式打开 `index.html`（蓝牙权限仍建议走 HTTPS / localhost）。

## ♿ 相关项目

- [celesWuff/waterctl](https://github.com/celesWuff/waterctl) 蓝牙水控器 FOSS（参考实现）
- [celesWuff/wateremu](https://github.com/celesWuff/wateremu) 蓝牙水控器模拟器
- [celesWuff/drinkctl](https://github.com/celesWuff/drinkctl) “点点”扫码饮水开源实现

## 📜 开源许可

基于 [GNU Affero General Public License v3.0](./LICENSE) 许可进行开源。

文档结构参考 [celesWuff/waterctl](https://github.com/celesWuff/waterctl)。
