# 轮回指数 · 官方介绍页 设计文档

> 四问评审：2026-11-22（增量修订免重复触发；架构级变更须再评审并更新此行）

## 项目概述

为量化数据平台「狩诸待To」（正式站 https://www.szdto.xyz/ ）制作官方产品介绍页，
以产品功能展示为主、引流到正式站为辅。纯静态单页，部署于 GitHub Pages：
https://cycleindex-szdto.github.io/ （用户主页仓库 `cycleindex-szdto.github.io`）。

## 品牌命名（已确认）

```
眉题：SZD CYCLE INDEX · QUANT TERMINAL
主标题：轮回指数
副标题：狩诸待To —— 市场情绪量化终端
站点 <title>：轮回指数 · 狩诸待To — 市场情绪量化终端
```

## 技术形态（已确认）

- 手写单文件静态站：`index.html` 内嵌全部 CSS/JS，截图放 `images/`
- 零构建、零依赖；git push → GitHub Pages（Deploy from a branch: main / root）
- 视觉风格：现代金融终端风——深色底 + 数据可视化元素 + 渐变光效
  （TradingView / Bloomberg 官网质感），与正式站深色主题一致

## 页面结构（自上而下）

1. **顶部导航**（sticky）：轮回指数字标 + 「进入平台」按钮
2. **Hero 首屏**：眉题 + 主标题「轮回指数」+ 副标题 + 双 CTA（进入平台 / 浏览功能）
   + 纯 CSS/SVG 渐变光效、网格与蜡烛图装饰
3. **数据亮点条**：多市场覆盖 / 贪恐指数实时追踪 / 行业板块 / 策略回测 等静态亮点
4. **功能画廊**（核心区）：每组 = 小标题 + 一句话说明 + 截图卡片；
   hover 浮起，点击灯箱放大（参考趋势动物Pro 交互）
5. **CTA 收尾**：「立即体验」→ https://www.szdto.xyz/
6. **页脚**：© 轮回指数 · 狩诸待To · szdto.xyz · GitHub 仓库链接

## 功能画廊内容分组（截图来自正式站真实页面）

| # | 分组 | 截图来源路由 |
|---|---|---|
| 1 | 恐惧贪婪指数 | /home |
| 2 | 股票筛选列表 | /stocks |
| 3 | 股票 K 线终端 | /stock/kline/600519 |
| 4 | 加密货币 K 线 | /crypto/kline/BTCUSDT |
| 5 | 行业板块 | /markets/sectors |
| 6 | 主线板块 | /markets/mainline |
| 7 | 市场宽度 | /markets/breadth |
| 8 | 市场温度 | /markets/temperature |
| 9 | 策略回测 | /backtest-history（若跳登录则跳过） |

## 工程硬性项（验收标准）

- [ ] 移动端适配：390px 窄视口实测截图验收（移动 UA + 窄视口，不靠猜）
- [ ] 图片：统一压缩，`loading="lazy"`，整站图片 ≤ 15MB
- [ ] SEO：title / description / OG 标签完整（分享有卡片预览）
- [ ] 安全红线：页面与截图中不出现服务器 IP、内网地址、个人信息
- [ ] 截图质量：每张截图等待数据加载完成，无空态/加载中/报错画面
- [ ] 部署后线上验证：`curl -I` 200 + 线上截图 + Lighthouse 审计
- [ ] 灯箱交互：点击放大 / ESC / 点击遮罩关闭 / 背景 scroll 锁定

## 部署（需用户配合）

- 本地仓库 remote → `git@github.com:cycleindex-szdto/cycleindex-szdto.github.io.git`
- 建仓与 push 需 cycleindex-szdto 账号凭证（本机 gh 登录的是 wuchun4，
  部署时需用户 `gh auth login` 切换/添加账号，或用 SSH key）
- GitHub 仓库 Settings → Pages → Deploy from a branch → main / (root)

## 实现步骤

1. ✅ 项目骨架 + 本设计文档
2. 截图采集（无头浏览器逐页实截正式站）
3. index.html 主实现（结构/样式/交互/SEO）
4. 多维评审（workflow：视觉/文案/SEO/安全红线/移动端）
5. 修复 + 本地多视口验收
6. 部署 + 线上验证
