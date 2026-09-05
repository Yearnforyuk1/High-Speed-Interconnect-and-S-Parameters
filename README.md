# High-Speed Interconnect and S-Parameters

面向高速芯片与 SerDes RX 的传输线、S 参数与阻抗匹配学习记录。

## 学习重点
传输线模型、Z0/传播延迟、反射与端接、差分100Ω/奇偶模、S11/S21、mixed-mode S参数、TDR/Smith Chart、renormalization、passivity/causality、PEX+S参数联合仿真，以及从波形畸变定位不连续点。

## 场景
差分时钟、clock buffer、芯片内/封装/PCB互连、电RX和光接收机接口。

## 学习原则
- 新练习先与仓库现有记录和已完成问答对比，避免重复考已经掌握的基础题。
- 题目按“必要原理 → 计算/判断 → Cadence/Spectre/S参数实操 → 递进追问”推进。
- 已掌握的基础内容作为后续题目的工具使用，不再反复单独训练。
- **默认同步规则：本学习线之后的新题、用户作答、讲评、关键结论与阶段总结都同步到本仓库；除非用户明确要求暂停同步。**

## 当前进度
已完成/讨论：
- Z0、传播延迟与何时需要 transmission-line model
- 开路/短路与正负反射
- round-trip delay 定位反射点
- 1→2 junction、功率分配与约 -3 dB 问题
- 高阻 clock buffer、AC coupling 与反射
- 严重确定性反射为何不一定带来很大的 clock jitter

当前阶段：S11/S21、return loss、insertion loss 与时域 clock waveform 的联系。

## 记录
- [传播、反射与阻抗](notes/01-transmission-line-reflection.md)
- [S参数与SerDes互连](notes/02-sparameters-serdes.md)
- [E型1→2时钟网络](notes/03-e-network-clock.md)
- [严重反射为什么不一定带来很大的Clock Jitter](notes/04-clock-reflection-vs-jitter.md)
- [练习与作答记录](exercises/01-exercise-log.md)
- [练习02：Clock反射、S11/S21、Return Loss与波形质量](exercises/02-s11-s21-return-loss-and-clock-jitter.md)

## 后续路线
1. S11/S21、return loss、insertion loss
2. 50 Ω single-ended reference 与 100 Ω differential 的关系
3. mixed-mode S 参数：Sdd11/Sdd21/Sdc21 等
4. odd/even mode、Zdiff/Zcm
5. reference impedance 与 renormalization
6. TDR 与阻抗不连续定位
7. Smith Chart
8. S 参数级联、passivity/causality
9. PEX + S 参数联合 Spectre 仿真
10. 从真实 E 型时钟波形反推 discontinuity
