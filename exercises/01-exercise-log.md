# 练习与作答记录

## 已完成
- 开路/短路：Γopen=+1，Γshort=-1；能判断高阻正反射、低阻负反射。
- 往返延迟定位：30 ps 往返、vp=1.5×10^8 m/s，得到 2.25 mm。
- 开路端：入射 0.4 V、Γ=+1，第一次端点电压 0.8 V；进一步讨论多次反射与源端边界。
- Clock buffer：V+=300 mV、ΓL=0.8，作答 VL=540 mV；正确指出反射可能改变时钟边沿/crossing，因此大正反射不一定优于匹配。
- 1→2 junction：100 Ω 主线→两条100 Ω支路，Zeq=50 Ω、Γ=-1/3；入射600 mV，作答 VJ=400 mV，并指出并联导致失配。
- 分支功率：Γ=-1/3，作答反射功率1/9、每支路4/9，正确。
- 匹配 junction 的直观尝试：两个相同支路并联为100 Ω时，每支路 characteristic impedance 为200 Ω；已澄清不是“线电阻翻倍”，也不能简单按线宽减半得到精确2×Z0。

## 后续
source termination + high-Z receiver；差分阻抗/奇偶模；S11/S21、return/insertion loss；mixed-mode；reference impedance/renormalization；TDR/Smith Chart；passivity/causality；PEX+S参数联合仿真；从真实E型波形反推 discontinuity。
