# S 参数与 SerDes 互连

## 延迟如何进入 .sp
S21(f)=exp(-γL)=exp(-αL)exp(-jβL)。幅度体现损耗，相位包含传播延迟；近似无色散时 phase(S21)=-2πf·td，group delay τg=-dφ/dω。频域复数 S 参数转到时域后自然出现 delayed echo、台阶和振铃。

## S11 与 clock buffer
S11 大表示相对 reference impedance 失配，不等于接收端电压一定小。高阻 CMOS clock buffer 可有正反射并增大端点电压，但可能改变 threshold crossing，产生 deterministic jitter。

## AC coupling
交流能通过 ≠ 阻抗匹配。ZC=1/(j2πfC)。250 fF 在 16 GHz 的 |ZC| 约 40 Ω。增大耦合电容只能减小其串联电抗，不能把后级高阻/容性 CMOS 输入自动变成 100 Ω differential termination。

## PEX vs S参数
不是“PEX低精度、S参数高精度”。短、电长度小的局部互连，正确 PEX RLC 与 EM/S 参数应趋近；长线、复杂耦合、多端口和传播明显时，EM/S参数更自然。
