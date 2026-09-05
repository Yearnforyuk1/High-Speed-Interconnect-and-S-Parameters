# 严重反射为什么不一定带来很大的 Clock Jitter

## 结论
对于周期性差分时钟，如果互连/封装/S 参数网络可近似为线性时不变（LTI）系统，且反射路径和边界条件固定，那么反射可以造成明显的幅度畸变、台阶、过冲、固定相移，但不会凭空产生 cycle-to-cycle 随机抖动。

## LTI 数学解释
设通道冲激响应为 h(t)，输入时钟满足 x(t+T)=x(t)。输出

y(t)=x(t)*h(t)。

则

y(t+T)=∫h(τ)x(t+T-τ)dτ=∫h(τ)x(t-τ)dτ=y(t)。

因此稳态输出仍以 T 严格重复。若同类边沿 crossing 为 t_c，则 t_{c,n}=t_c+nT；固定波形畸变或固定延迟不等于 cycle-to-cycle jitter。

## 用反射回波表示
多次反射可写成

h(t)=a0δ(t-τ0)+a1δ(t-τ1)+a2δ(t-τ2)+...

所以

y(t)=a0x(t-τ0)+a1x(t-τ1)+a2x(t-τ2)+...

只要 a_k、τ_k 固定，每个 clock period 的回波图样也固定。

## 为什么 Data 更容易变成 DDJ
PRBS 数据的 bit history 不同，通道 memory/ISI 会让不同边沿前的 residual voltage 不同，从而产生不同 crossing time，即 data-dependent deterministic jitter。周期 1010... clock 的边沿历史固定，因此这一机制明显弱得多。

## Clock buffer 的关键：crossing slew
小信号近似下，阈值附近电压噪声转成时间误差：

Δt≈-ΔV/(dV/dt)，RMS 形式 σ_t≈σ_v/SR。

因此即使完整波形存在台阶，只要 reflection 不压在 threshold crossing 附近，且 crossing slew 很大，恢复后的 clock jitter 仍可很小。高阻端的正反射甚至可能提高局部摆幅/斜率，但不能因此直接认为反射“有益”。

## 什么时候反射会明显恶化 jitter
1. 反射台阶落在 threshold crossing 附近，降低局部 slew。
2. 产生 plateau 或 multiple crossing，小噪声即可切换实际判决时刻。
3. P/N 路径不对称，使 differential crossing 随 PVT/crosstalk/supply 变化。
4. 互连本身随时间变化，或叠加电源噪声、串扰、器件噪声。

## 对 SerDes RX clock network 的判断
不要只看 waveform 是否“像方波”。至少同时检查：
- differential zero crossing；
- crossing slew rate；
- edge-to-edge / period jitter；
- reflection arrival time 相对 crossing 的位置；
- P/N 对称性及 common-mode → differential conversion。

后续建议在 Spectre 中保持反射幅度基本不变，只扫 transmission-line delay，使回波从远离 crossing 移到 crossing 附近，观察 output RMS jitter 与 reflection arrival time 的关系。
