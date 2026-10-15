# tasks.md — deep-cave UI 轮

- **文档状态**: approved
- **最后更新**: 2026-10-13
- 标记：`[spec]` 规范/契约 · `[ui]` 界面实现 · `[verify]` 验证

## 已完成

- [spec] 建立 `spec.md`（玩法→UI 规则映射、平台、验收标准）
- [spec] 建立 `research.md`（7 项实测缺陷 D1–D7，含测量数据）
- [spec] 建立 `contracts/style-contract.yaml`（原始值 / 语义别名 / 组件契约 / 交互反馈）
- [spec] 建立 `contracts/screen-contract.yaml`（12 屏审计 + 缺口）
- [ui] D3 · Canvas 字体统一为 `UI` 常量（4 档字号 + 1 套含中文回退的字体栈），硬编码 `ctx.font` 归零
- [ui] D1 · Boss 血条迁到 DOM `#bossBar`，并删除死代码 `drawBossBar()`
- [ui] D1 · 顶部 HUD 改 flex 行 `#hudTop`，血条结构上不可能与左右 HUD 重叠
- [ui] D2 · 绳索文案数字优先、去掉与右 HUD 重复的层号，条形内不再贴边
- [ui] D4 · `label()` 边缘夹紧 8px；建筑离屏 >30px 不再画标签
- [ui] D5 · 新增 `settings` 屏（主音量 / 屏幕震动 / 减少动态效果 / 触屏按键 / 操作说明）
- [ui] D5 · 无障碍：减少动效 → 震屏归零 + 粒子减半；设置存独立 key `deepcave_ui`
- [ui] D6 · 新增 `tutorial-overlay`（3 步，只出现一次，**不改 state**，不阻断游戏）
- [ui] D7 · HUD 底色 `.72→.80`、描边 `.35→.50`，暗场景边界可辨
- [ui] 层级契约落地：hud 10 < bossbar 12 < toast 13 < touch 15 < fade 18 < modal 20
- [verify] `suite4.mjs` 48 项断言：Token 落地 / 血条 DOM / 数字优先 / 设置持久化 / 引导一次性 /
      字体统一 / 标签像素级夹紧 / 离屏剔除 / 窄视口 900×600 适配
- [verify] 全量回归 169 项断言全过、控制台 0 错误

## 待办

- [ ] `[ui]` codex 图鉴屏（`optional`）：矿物 7 种 / 怪物 5 种 / 精英词缀 5 种 / 武器挡位 6 档
      入口建议并入 `menu`，不新占地表建筑位
- [ ] `[ui]` 设置面板压缩高度：把「操作」区从 4 张卡片改为紧凑行，避免需要滚动
- [ ] `[verify]` 触屏真机走查：`#hudTop` 在手机横屏（如 844×390）下的密度与安全区
- [ ] `[ui]` 若将来加入多语言，`UI.FAMILY` 与 DOM `--font` 需抽出同一份字体表
