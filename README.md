# NutriNarrative 🥗📊

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/CurSpoon/NutriNarrative/pulls)

**智能饮食记录系统，用数据讲述你的美食故事**

## 功能亮点 ✨
- 🕒 **智能时间识别** - 根据用餐时间自动分类餐型
- 📈 **动态可视化** - 使用 ECharts 实现卡路里趋势分析
- 🔥 **交互式热力图** - 直观展示每日能量分布，支持悬停查看食物明细
- 🤖 **AI 营养师** - 使用 DeepSeek API 生成效果敏捷的饮食分析报告
- 📦 **数据管理** - 一键导入/导出饮食记录，支持 JSON 文件格式

## 项目结构 🗂️
```
.
├── src
│   └── versions
│       ├── health0.1
│       │   └── index.html
│       └── health0.2
│           └── index.html
├── docs
│   └── ai-prompts
│       └── process-records.md
├── LICENSE
└── README.md
```

## 版本更新报告 📄

### 版本 0.1 -> 0.2 更新

**新增功能**
- **卡路里智能计算优化**: 支持手动输入卡路里，并智能标记是否为用户手动输入。
- **热力图交互升级**: 新增鼠标悬停提示框，提供详细的餐次食物信息。
- **数据管理功能增强**: 增加导入导出功能按钮，支持JSON格式的数据保存与读取。
- **AI 分析报告优化**:
  - 引入 DeepSeek API 分析接口，为用户生成更个性化的饮食报告。
  - 提供详细的 HTML 格式分析报告，包括营养概要、饮食性格标签等。

**界面与交互优化**
- 数据录入、分析结果与数据管理布局更加合理。
- 按钮、提示框等组件加入动画与视觉效果。

## 技术栈 🛠️
- **核心框架**: Vanilla JavaScript
- **可视化**: ECharts 5.4.3
- **AI引擎**: DeepSeek API
- **样式**: 纯CSS现代设计
- **存储**: localStorage + JSON 文件管理

## 快速开始 🚀

1. 克隆仓库
    ```bash
    git clone https://github.com/CurSpoon/NutriNarrative.git
    cd NutriNarrative
    ```
2. 打开 `index.html` 文件即可运行

## 使用指南 📚
1. **录入饮食数据**
   - 输入日期、时间、食物名称和份量
   - 系统将智能计算卡路里
2. **数据可视化**
   - 通过图表查看每日卡路里趋势与热力图分布
3. **AI 分析**
   - 点击生成分析按钮，获得生动有趣的饮食报告
4. **数据管理**
   - 导入导出饮食记录，轻松备份与分享

## 许可证 📚
本项目基于 MIT 协议开源。

