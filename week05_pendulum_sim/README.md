# Week 05 Pendulum Simulation

- 实验者姓名：徐文豪
- 学号：5702126152
- 无菌工作区状态：就绪。当前目录仅包含本实验 README.md 与原生单文件 index.html，未引入外部库或依赖。
实验报告：人机协同三反思
1. 意图清晰度反思
答： 在让AI编写单摆模拟器MVP时，首轮结果不符合预期。我当时输入的提示词是“写一个单摆动画”，结果AI使用了外部库（如Three.js），且摆球运动速度极快，直接飞出了屏幕。
回看提示词，我缺少了【技术约束】和【验收标准】。
后来我按照“黄金三角”补齐了约束：明确要求“单文件index.html，纯原生HTML5 Canvas绘制，不引用外部库”，并补充了初始参数（摆长L=200px，g=9.8，初始角度45度）和物理方程（引入阻尼系数k），同时明确了“双击浏览器打开即可流畅摆动”的验收标准。补齐后，AI一次生成了符合预期的MVP。

2. 闭环控制反思
答： 当遇到“重置”按钮无响应且动画停滞时，我没有盲目让AI重写，而是采用了证据驱动排错（Evidence-Based Debugging）。
我按F12调出控制台，复现错误，提取了完整的红字堆栈：Uncaught ReferenceError: resetAnimation is not defined at HTMLButtonElement.onclick (index.html:68:15)，并将这段堆栈直接喂给AI。
AI进行了ReAct反思，诊断根因是：resetAnimation 函数被定义在了 DOMContentLoaded 的局部作用域内，而HTML的 onclick 属性只能访问全局作用域。我看懂了AI的修复方案：它没有修改物理公式，而是通过调整JavaScript的作用域边界条件（将函数提升到全局作用域或改用 addEventListener 进行事件绑定），从而精准地修复了Bug。

3. 主体地位确认
答： 作为HOTL（人在回路之上）的产品总设计师，核心决策由我决定：包括产品的视觉方向（深灰科技色#1a1a24、摆球发光光效）、交互边界（摆长100~350px、重力1~25、阻尼0.000~0.010的滑块范围设定）、物理模型的选择（单摆简谐振动微分方程），以及排错时的反馈质量（提取控制台完整堆栈而非情绪化抱怨）。
重复劳动由AI完成：例如HTML/CSS的样板代码编写、Canvas API的绘图细节、利用 requestAnimationFrame 驱动的动画循环、微分方程的数值积分代码实现，以及繁琐的DOM事件监听绑定。我负责“提需求、设边界、看效果、给反馈”，AI负责底层的语法实现。

---

## 基线锁定

- 锁定日期：2026-10-12
- 锁定方式：`feat(week05): init pendulum experiment workspace`
- 工作区就绪状态：无菌（仅 README.md + index.html，无外部依赖）

