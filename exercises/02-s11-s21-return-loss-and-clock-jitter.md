# 练习 02：Clock 反射、S11/S21、Return Loss 与波形质量

日期：2026-09-05

## 学习位置
基础反射系数、开路/短路、往返延迟、1→2 junction、基础 dB 关系已做过，不再作为独立入门题重复。当前开始进入 S 参数指标如何对应 SerDes RX 实际 clock waveform。

---

## Part A：回顾题——严重反射为什么不一定带来大 jitter

场景：

16 GHz differential clock → S-parameter interconnect → high-Z clock buffer

仿真观察：
- line input：约 300 mVpp
- clock buffer input：约 550 mVpp
- 存在明显反射台阶
- 连续测很多 clock cycle，恢复后的 RMS jitter 仍很小

### A1 判断题
哪些解释合理？可多选。

A. 反射是确定性的，每周期基本重复，因此可能造成固定波形畸变而不造成很大的 cycle-to-cycle jitter。

B. 只要有反射，jitter 一定很大。

C. 只要 threshold crossing 附近的 slew rate 仍然很大，buffer 的时间噪声可能依然很小。

D. 只看 clock amplitude 足够判断 clock quality。

### A2 分析题
解释为什么周期性 1010... clock 比 PRBS data 更不容易因为固定反射产生 data-dependent jitter。

### A3 Cadence/Spectre 分析题
保持 S 参数网络和反射幅度基本不变，只改变 transmission-line delay，使主要 reflection echo 相对 threshold crossing 的到达时间发生移动。

记录：
- buffer 输入 differential crossing slew
- output RMS jitter
- multiple crossing 是否出现
- reflection arrival time 相对 crossing 的位置

目标：验证“反射幅度相近，但反射落在 crossing 附近时 jitter 可能显著恶化”。

---

## Part B：S11、S21 与 Return Loss

### 必要原理
S11=b1/a1，表示 Port 1 入射波中有多少以反射波返回。

S21=b2/a1，表示从 Port 1 入射后有多少波到达 Port 2。

S 参数幅度用 dB 表示：

S11(dB)=20log10|S11|

Return Loss 定义：

RL=-20log10|S11|

因此：
- S11(dB) 越负，匹配越好；
- Return Loss 越大，匹配越好。

注意 reflection、insertion loss、waveform distortion、jitter 是相关但不同的指标。

### Q1：从 S11 dB 还原反射幅度
某差分 clock interconnect 在 16 GHz：

Sdd11=-10 dB

计算：

|S11|=10^(-10/20)

并判断这个反射幅度是否还能忽略。

### Q2：匹配和传输损耗不要混为一谈
Channel A：
- Sdd11=-6 dB
- Sdd21=-0.5 dB

Channel B：
- Sdd11=-20 dB
- Sdd21=-3 dB

回答：
1. 哪个匹配更好？
2. 哪个 transmission loss 更小？
3. 能否只凭这两个频点数字断言哪一个时域 clock waveform 一定更好？为什么？

### Q3：AC coupling 的低频 S11
设 AC coupling capacitor C=250 fF。

分别估算：
- 1 GHz 时 |ZC|=1/(2πfC)
- 16 GHz 时 |ZC|=1/(2πfC)

解释：为什么 AC-coupled clock network 的 S11 在低频接近 0 dB，并不能直接说明 16 GHz clock transmission 很差？

### Q4：基波和三次谐波
如果：

Sdd21(16 GHz)=-0.5 dB

Sdd21(48 GHz)=-8 dB

哪项最合理？

A. 16 GHz 基波几乎传不过去

B. clock amplitude 一定接近 0

C. clock 还能传，但边沿会明显变慢/变圆

D. 一定产生很大 random jitter

---

## Part C：Cadence / S 参数实操

对真实高速差分时钟网络至少观察三个频点：
- 1 GHz
- 16 GHz
- 48 GHz（三次谐波）

优先画 mixed-mode 指标：
- Sdd11
- Sdd21

若当前仍只有 single-ended 4-port/6-port S 参数，则先保留物理端口定义，后续单独进入 mixed-mode conversion。

记录：
- 目标频率的 return loss
- 目标频率 insertion loss
- 三次谐波 attenuation
- 时域 rise/fall time
- differential crossing slew
- overshoot / ringing / step

## 本轮回答格式
Q1：...
Q2.1：...；Q2.2：...；Q2.3：...
Q3：1 GHz=...，16 GHz=...；解释：...
Q4：...

## 下一阶段
完成本轮后进入：
“为什么 100 Ω differential interconnect 的 multi-port S 参数通常仍使用 50 Ω single-ended reference ports？”
随后进入 mixed-mode S 参数、Sdd11/Sdd21/Sdc21、odd/even mode 与 renormalization。
