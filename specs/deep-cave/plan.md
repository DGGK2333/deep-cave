# plan.md — 屏幕路线与批次

- **文档状态**: approved
- **最后更新**: 2026-10-13

## 屏幕路线（按玩家旅程，不按名称排序）

```
[首次进入] start-menu
   ├─(无存档)→ fresh() → tutorial-overlay（只出现一次，不阻断游戏）
   └─(有存档)→ cont()
        ↓
[核心循环] hud（地表形态）
   ├─ 走到 POI → shop / casino / upgrade / relics / portal / stats
   ├─ 洞口按 S → hud（地下形态）+ 绳索紧张态
   └─ 每 5 层 → boss-bar 出现 → 第 15 层 victory
        ↓
[返程] settlement ──→ 回 hud（地表）继续升级
[死亡] death ──→ 回 hud（地表），背包减半
[任意时刻] Esc → menu（暂停）→ settings
```

## 批次

| 批次 | 内容 | 依赖 | 状态 |
|---|---|---|---|
| B1 | Token 化 + 组件规则统一（颜色/圆角/字号/层级） | 无 | ✅ 完成 |
| B2 | Boss 血条从 Canvas 迁到 DOM；顶部 HUD 改 flex 行 | B1 | ✅ 完成 |
| B3 | HUD 文案数字优先；地表标签夹紧 + 离屏剔除 | B1 | ✅ 完成 |
| B4 | settings 屏（音量/震动/减少动效/触屏） | B1 | ✅ 完成 |
| B5 | tutorial-overlay 屏（3 步，不阻断，可跳过） | B1 | ✅ 完成 |
| B6 | codex 图鉴屏 | B1 | ⏸ 未做（optional，见 tasks.md） |

## 为什么是这个顺序

1. **先 Token 化再做具体界面**：否则每改一个界面都要重新发明颜色与圆角，且后续必然打架。
2. **Boss 血条优先于其它界面**：它是当前唯一"会压住玩家正在看的信息"的缺陷（与 toast 几何重叠），属于功能性阻断。
3. **设置屏排在引导前**：引导只影响新玩家一次，而设置影响所有人；且"减少动态效果"是无障碍项，优先级高于教学。
4. **图鉴最后**：它只增加留存，不闭合任何循环。

## 生成批次说明（本项目不适用图片链路）

`game-ui-workflow` 的 B 之后阶段（page-generator → component-breakdown → sprite-sheet-splitter → asset-pipeline）
在本项目**不执行**，原因写入 `research.md`：本项目零图片依赖、UI 全部程序化绘制；
引入 PNG/Atlas 会破坏"单文件、双击即玩"这一核心交付属性。

## 遗留与风险

- 设置面板内容略高于可视区，需要滚动才能看到底部按钮（`.card{overflow:auto}` 已兜住，不阻断操作）。
- `hudR` 用 `max-width:36%` 限制宽度；若将来武器名更长，靠 `text-overflow:ellipsis` 截断，属可接受降级。
- 触屏下 `#hudTop` 仍是 flex 行，未针对竖屏单独适配（项目本身只支持横屏）。
