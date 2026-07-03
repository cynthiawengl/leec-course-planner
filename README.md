# LEEC 课程规划工具

一个纯前端的单页网页，帮助在 **MEEC（电气与计算机工程硕士）** 和 **MEIC-A（信息与计算机工程硕士）** 两个 Técnico Lisboa 硕士课程之间选课、规划学分，并安排每周上课时间表。

在线预览：直接打开 [`planner/index.html`](planner/index.html) 即可使用，无需安装依赖、无需服务器。

## 功能

### 1. 学分规划
- 两年四学期（Y1S1 / Y1S2 / Y2S1 / Y2S2），每学期上限 **36 ECTS**
- 第二年第一学期自动锁定 **12 ECTS PIC**（二级项目），第二年第二学期自动锁定 **30 ECTS 论文**（Dissertação），均计入学分上限
- 每个学期按 period 拆分显示：贯穿整学期（Semestral）的课程单独展示，半学期课程按 P1/P2 或 P3/P4 归入对应栏目
- 右侧课程目录支持按院系（MEEC / MEIC-A）、学期、专业方向筛选，支持搜索课程名称/缩写
- **方案保存与对比**：可将当前选课保存为具名方案，反复保存多份；勾选任意两个方案可弹窗对比每学期的课程差异与学分小计
- 所有数据保存在浏览器 `localStorage`，刷新不丢失

### 2. 每周课表
- 与学分规划共享同一份已选课程数据，按学期切换
- 周一至周五、08:00–21:00 的网格视图，操作方式类似苹果日历：
  - 按住空白处拖拽即可新建时间块，选择课程 + 类型（Teórica / Prática / Lab）
  - 点击已有时间块可编辑或删除
  - 拖动块体可整体移动（含跨天），拖动底边可调整时长（15 分钟为最小单位）
  - 同一天时间重叠的时间块会自动标红提示冲突
- 在学分规划里移除某门课时，该课程在课表中已排的时间块会自动清除

## 数据来源

课程数据从两份官方资料解析整理而来（均保存在仓库根目录）：

- `Currículo · Mestrado Bolonha em Engenharia Eletrotécnica e de Computadores.pdf` — MEEC 官方课程大纲（86 门课）
- `A3ES MEIC2026 Plano curricular.xlsx` — MEIC-A 学分结构表（56 门课）

解析结果整理为 [`planner/courses.json`](planner/courses.json)，供网页直接读取（已内嵌进 `index.html`，无需额外请求）。

## 目录结构

```
.
├── planner/
│   ├── index.html      # 单页应用（学分规划 + 每周课表）
│   └── courses.json    # 解析后的课程数据
├── A3ES MEIC2026 Plano curricular.xlsx
├── Currículo · Mestrado Bolonha em Engenharia Eletrotécnica e de Computadores.pdf
```

## 本地运行

直接双击 `planner/index.html` 用浏览器打开即可（数据已内嵌，不依赖网络请求）。

如果想用本地服务器预览：

```bash
cd planner
python3 -m http.server 8743
# 然后访问 http://localhost:8743
```

## 版本历史

提交记录按功能迭代顺序保留，可用 `git log --oneline` 查看：

1. 添加原始课程大纲资料
2. 提取整理课程数据为 JSON
3. v1：学分规划网页初版（深色主题）
4. v2：改为浅色主题，新增方案保存与对比功能
5. v3：按 period 拆分学期显示
6. v4：新增独立的每周课表拖拽页面
7. v5：合并为单页应用（学分规划 + 每周课表）
