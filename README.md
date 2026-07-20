# AI时代的前端工程

> Created By [RV](mailto:rodney.vin@gmail.com), and licensed with Creative Commons "[CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)"

![landscape](./assets/landscape.png)

---

## 第一原理：AI Native，AI First

AI 不是前端工具的又一个迭代，而是前端架构的范式切换。

传统前端框架（React、Vue、Angular）是为**人类开发者**设计的——复杂的状态管理、组件树协调、虚拟 DOM diff、手动优化。这些框架的复杂度来源于一个假设：**UI 由人编写、由人维护**。

AI 时代，这个假设不成立了。

如果 UI 由 AI 生成，那么架构应该为 AI 优化，而不是为人类开发者优化。这就是"AI Native，AI First"的含义：

- **AI 是第一路径**：需要 UI → AI 生成。人类不写 UI 代码。
- **人类干预是例外**：当 AI 能力不足时，人类去补充 Catalog（工具箱），而不是绕过 AI 手写 UI。
- **预置式 UI 是 AI 的缓存**：构建时 AI 生成蓝图、冻住、随包发布。运行时 AI 重新生成就是动态 UI。两者同一来源，同一架构。

---

## 架构栈

整个体系由四层构成，每层都为"AI 是蓝图的生成者"这个前提优化：

```
                    ┌──────────────────────────────────┐
     UI 层          │  Schema + Catalog + Renderer   │
                    │  ┌─Blueprint（结构）            │  ← AI 生成
                    │  ├─Catalog（组件注册表）         │  ← 人类维护
                    │  ├─DataModel（数据状态）         │  ← 服务端驱动
                    │  └─Interaction（行为枚举）       │  ← 声明式
                    ├──────────────────────────────────┤
  通信/协作层       │  Kree4X RPC ServiceCall       │  ← 语义调用
                    ├──────────────────────────────────┤
  传输层            │  Kree4js (mTLS + KCP)         │  ← 可靠传输
                    ├──────────────────────────────────┤
  状态层            │  服务端状态管理 + Diff         │  ← 增量更新
                    └──────────────────────────────────┘
```

### UI 层 — Schema + Catalog + Renderer

AI 生成的不是代码，而是**结构化的 UI 描述**（Blueprint）。渲染器拿蓝图 + 数据渲染原生组件。

我们借用了 A2UI 的核心思想——Catalog 组件注册、Blueprint 结构描述、DataModel 数据分离——但不使用 A2UI 本身。A2UI 是 SDUI 面向纯 AI 生成的一种参考实现，我们的实现基于相同的设计原则，但有独立的架构决策。

- **Blueprint**：UI 树结构，AI 生成的输出
- **Catalog**：组件白名单，AI 只能使用 Catalog 内的组件
- **DataModel**：数据状态，与 Blueprint 分离，支持独立更新
- **Interaction**：扁平 Action 枚举，AI 声明用户交互行为

### 通信/协作层 — Kree4X RPC ServiceCall

无消息层，AI 调用 Service 而非发送消息。AI 理解的是语义（"获取用户信息"），而不是协议细节（"发送 GET /users/123"）。

### 传输层 — Kree4js

mTLS 加密传输，KCP 可靠 UDP。AI 不感知这一层。

### 状态层 — 服务端状态管理 + Diff

服务端维护状态完整性，自动计算 diff 下发增量更新。AI 只需下发完整状态，不需要理解"哪些变了"。

---

## 与传统前端栈的对比

| 维度 | 传统前端（React/Vue + REST/Redux） | AI Native 前端（Schema + Catalog + Renderer + Kree4X） |
|------|-----------------------------------|----------------------------------|
| UI 来源 | 人类手写 | AI 生成 |
| 渲染方式 | 虚拟 DOM diff + 协调 | Blueprint 直接映射到原生组件 |
| 状态管理 | 客户端全局 store | DataModel 分离，服务端驱动 |
| 通信模型 | REST/GraphQL，消息语义 | RPC ServiceCall，调用语义 |
| 增量更新 | 手动优化 | 服务端自动 diff |
| 离线策略 | 复杂（SWR、缓存策略） | Blueprint 本地缓存 = 预置 UI |
| 人类角色 | 写 UI 代码 | 维护 Catalog、定义 Schema |

---

## 本书结构

第一章从问题出发，逐步推演出这套架构的各个侧面；后续章节展开各个层次的具体设计与实现。

全书目录见 [SUMMARY.md](./SUMMARY.md)。
