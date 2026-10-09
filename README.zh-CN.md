# react-native-flux-desktop-pro（中文文档）

> 🧩 开箱即用的高阶组件 —— 组合既有原子件，面向中后台业务场景。

![版本](https://img.shields.io/badge/version-0.1.3-blue) ![许可证](https://img.shields.io/badge/license-MIT-green) ![运行时](https://img.shields.io/badge/%E7%BA%AFReact%C2%B7%E5%8E%9F%E7%94%9F%E5%83%8F%E7%B4%A0%C2%B7%E9%9D%9EElectron-ff69b4)

**依赖：** `react-native-flux-desktop`（UI 核心）· `react-native-flux-desktop-chart`（内嵌迷你图）· `react`

---

![高阶表格 ProTable](./assets/pro-table.png)

本包是**组合层**：把原子组件拼装成面向业务的开箱即用组件。`ProTable` 内置查询表单 + 列配置 + 异步 `request` + 分页；配合 `ProForm`、`StatCard`、`CheckCard`、`TrendCard`、`PriceCard` 构成完整的增删改查 / 仪表盘工具箱，全部经 Token 感知主题。

| 高阶表格 ProTable | 轻量表单 ProForm | 指标卡 StatCard |
| :---: | :---: | :---: |
| ![](./assets/pro-table.png) | ![](./assets/pro-form.png) | ![](./assets/stat-card.png) |

## 安装

```bash
npm install react-native-flux-desktop react-native-flux-desktop-chart   # peers
npm install react-native-flux-desktop-pro
```

## 用法

```tsx
import { useState } from 'react';
import { ProTable, type ProColumn } from 'react-native-flux-desktop-pro';

const columns: ProColumn[] = [
  { title: '姓名', dataIndex: 'name', search: true },
  { title: '年龄', dataIndex: 'age', sorter: true },
  { title: '月薪', dataIndex: 'salary', render: (v) => `¥ ${v}` },
];

export default () => {
  const [rows, setRows] = useState<any[]>([]);
  // 受控异步：在 request 回调里拉数据并回填 dataSource（request 本身不返回数据）
  return (
    <ProTable
      columns={columns}
      dataSource={rows}
      request={(params) => { fetchRows(params).then(setRows); }}
    />
  );
};
```

## 组件清单

- `ProTable` 高阶表格 — 搜索表单 / 列配置 / 异步 request / 分页
- `ProForm` 轻量表单 — 声明式字段、校验规则、`actions` 受控
- `ProDescriptions` 描述列表 — 键值详情展示
- `ProCard` 高阶卡片 — 可折叠面板容器
- `StatCard` / `StatisticGroup` 指标卡 / 统计组 — 数值 + 趋势
- `CheckCard` / `CheckCardGroup` 可选卡片 — 单选 / 多选
- `TrendCard` 趋势卡 · `PriceCard` / `PriceTable` 价格卡 / 定价表
- `Highlight` 文本高亮 — 关键词命中着色

## 说明

- 组合层内部消费原子组件（及图表包的 `SparklineChart`），你只需从本包根入口导入。
- `ProTable` 的 `request` 支持同步数据源与异步分页两种模式，列上 `search:true` 自动生成查询项。

## 许可证

MIT

> English 版见 [README.md](./README.md)。
