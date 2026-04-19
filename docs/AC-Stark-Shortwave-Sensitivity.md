# 基于 AC-Stark 效应的 Cs Rydberg 原子短波电场测量灵敏度分析

本文对基于 **Cs 原子 70D₅/₂ Rydberg 能级** 的短波（HF）电场测量方案进行灵敏度估算。
方案采用 **Rydberg-EIT + 本地场（LO）外差增强** 的工作方式：通过引入一个与待测
短波频率接近的本地振荡电场 $E_\mathrm{LO}$，将原本对小信号二次响应的 AC-Stark 效应
线性化，从而大幅提升对弱场的分辨能力。

---

## 1. 物理原理

### 1.1 AC-Stark 频移

Rydberg 能级在射频/微波电场下的 AC-Stark 频移为

$$
\Delta\nu \;=\; \tfrac{1}{2}\,\alpha\,E^{2}
$$

其中 $\alpha$ 为该 Rydberg 能级的极化率。题目给定

$$
\alpha_{70D_{5/2}} \approx -1.4507\times 10^{4}\ \mathrm{MHz/(V/cm)^2}
      = -1.4507\times 10^{10}\ \mathrm{Hz/(V/cm)^2}.
$$

### 1.2 本地场 LO 外差增强

当本地场 $E_\mathrm{LO}$ 与待测信号 $E_\mathrm{sig}$ 同向且频率接近时，

$$
E(t)=E_\mathrm{LO}\cos\omega_\mathrm{LO}t+E_\mathrm{sig}\cos(\omega_\mathrm{LO}+\delta\omega)t
$$

其平方项给出一个随时间以拍频 $\delta\omega$ 变化的分量，对应的 AC-Stark 频率调制为

$$
\boxed{\;\delta\nu(t)\;=\;\alpha\,E_\mathrm{LO}\,E_\mathrm{sig}\cos\delta\omega t\;}
$$

响应由**二次**变为**线性**，斜率为

$$
k \;\equiv\; \left|\frac{d\nu}{dE_\mathrm{sig}}\right| \;=\; |\alpha|\,E_\mathrm{LO}.
$$

本地场越大响应越灵敏，但其直流 AC-Stark 项 $\tfrac12|\alpha|E_\mathrm{LO}^{2}$
会把 EIT 谱线推出谐振点，因此存在 **最佳 $E_\mathrm{LO}$** —— 令直流频移等于
EIT 线宽 $\Delta\nu_\mathrm{EIT}$：

$$
\boxed{\;E_\mathrm{LO}^{\mathrm{opt}}=\sqrt{\dfrac{2\,\Delta\nu_\mathrm{EIT}}{|\alpha|}}\;}
$$

---

## 2. EIT 线宽估算

EIT 线宽由若干独立机制决定，总线宽近似为各项方均和：

$$
\Delta\nu_\mathrm{EIT}^{2} \approx \Delta\nu_\mathrm{laser}^{2}
  +\Delta\nu_\mathrm{tt}^{2}+\Delta\nu_\mathrm{pow}^{2}+\Delta\nu_\mathrm{nat}^{2}.
$$

### 2.1 激光线宽

探测光（852 nm，6S₁/₂ → 6P₃/₂）与耦合光（509 nm，6P₃/₂ → 70D₅/₂）均为 5 kHz。
对不相关双光子 EIT

$$
\Delta\nu_\mathrm{laser}=\sqrt{\Delta\nu_{852}^{2}+\Delta\nu_{509}^{2}}
=\sqrt{5^{2}+5^{2}}\ \mathrm{kHz}\approx 7\ \mathrm{kHz}.
$$

### 2.2 渡越时间展宽

室温 Cs（$T=300$ K，$m=2.207\times 10^{-25}$ kg）的平均速率

$$
\bar v=\sqrt{\dfrac{8k_{B}T}{\pi m}}\approx 219\ \mathrm{m/s}.
$$

光束直径 $d=0.7$ mm，渡越时间 $\tau=d/\bar v\approx 3.2\ \mu$s。
对高斯光束取 $\Delta\nu_\mathrm{tt}\approx 0.4\,\bar v/d$：

$$
\Delta\nu_\mathrm{tt}\approx\dfrac{0.4\times 219}{0.7\times 10^{-3}}\approx
1.25\times 10^{5}\ \mathrm{Hz}=125\ \mathrm{kHz}.
$$

### 2.3 自然线宽

- 中间态 6P₃/₂：$\Gamma_e/2\pi=5.22$ MHz（用于计算功率展宽，不直接进入双光子线宽）。
- Rydberg 态 70D₅/₂ 寿命约 $\sim 150\ \mu$s，自然线宽 $\sim 1$ kHz，**可忽略**。

### 2.4 耦合光功率展宽

光斑面积

$$
A=\pi(d/2)^2=\pi(0.35\,\mathrm{mm})^2=3.85\times 10^{-3}\ \mathrm{cm^{2}}
=3.85\times 10^{-7}\ \mathrm{m^{2}}.
$$

峰值强度

$$
I=\dfrac{P}{A}=\dfrac{0.5\ \mathrm{W}}{3.85\times 10^{-7}\ \mathrm{m^{2}}}
\approx 1.30\times 10^{6}\ \mathrm{W/m^{2}}\;(=130\ \mathrm{W/cm^{2}}).
$$

对应电场

$$
E_c=\sqrt{2\eta_0 I}=\sqrt{2\times 377\times 1.30\times 10^{6}}
\approx 3.13\times 10^{4}\ \mathrm{V/m}.
$$

取 6P₃/₂ → 70D₅/₂ 有效偶极矩 $d_c\approx 0.01\,ea_0=8.48\times 10^{-32}\ \mathrm{C\cdot m}$
（高主量子数，按 $n^{*-3/2}$ 比例估算），耦合拉比频率

$$
\Omega_c=\dfrac{d_c E_c}{\hbar}\approx 2.5\times 10^{7}\ \mathrm{rad/s},\quad
\Omega_c/2\pi\approx 4.0\ \mathrm{MHz}.
$$

由于 $\Omega_c<\Gamma_e$，阶梯型 EIT 透明窗口 FWHM（功率展宽项）

$$
\Delta\nu_\mathrm{pow}\approx\dfrac{\Omega_c^{2}}{2\pi\,\Gamma_e}
=\dfrac{(4.0\ \mathrm{MHz})^{2}}{5.22\ \mathrm{MHz}}\approx 3.1\ \mathrm{MHz}.
$$

### 2.5 EIT 总线宽

| 贡献 | 数值 |
|---|---|
| 激光线宽 | 7 kHz |
| 渡越时间 | 125 kHz |
| 耦合光功率展宽（主导） | 3.1 MHz |
| Rydberg 自然线宽 | ~1 kHz |

$$
\boxed{\;\Delta\nu_\mathrm{EIT}\approx 3\ \mathrm{MHz}\;}
$$

**功率展宽占绝对主导**。若需进一步压窄，可减小 509 nm 功率或扩束（以代价换取信噪比）。

---

## 3. 本地场选取与响应斜率

### 3.1 最佳本地场

由 $E_\mathrm{LO}^{\mathrm{opt}}=\sqrt{2\Delta\nu_\mathrm{EIT}/|\alpha|}$：

$$
E_\mathrm{LO}^{\mathrm{opt}}=
\sqrt{\dfrac{2\times 3\times 10^{6}\ \mathrm{Hz}}
{1.4507\times 10^{10}\ \mathrm{Hz/(V/cm)^{2}}}}
\approx 2.03\times 10^{-2}\ \mathrm{V/cm}
\approx 20\ \mathrm{mV/cm}.
$$

### 3.2 响应斜率

$$
k=|\alpha|E_\mathrm{LO}^{\mathrm{opt}}
=1.4507\times 10^{10}\times 2.03\times 10^{-2}
\approx 2.95\times 10^{8}\ \mathrm{Hz/(V/cm)}
\approx 295\ \mathrm{kHz/(mV/cm)}.
$$

---

## 4. 灵敏度估算

### 4.1 最小可测频率（鉴频极限）

假设光子散粒噪声下 EIT 鉴频分辨率

$$
\delta\nu_\mathrm{min}\approx\dfrac{\Delta\nu_\mathrm{EIT}}{\mathrm{SNR}\sqrt{\Delta f}}
$$

典型实验参数下 $\delta\nu_\mathrm{min}\sim 1\ \mathrm{kHz}/\sqrt{\mathrm{Hz}}$ 是可达到的。

### 4.2 外差灵敏度

$$
\delta E_\mathrm{min}=\dfrac{\delta\nu_\mathrm{min}}{k}
=\dfrac{10^{3}\ \mathrm{Hz}/\sqrt{\mathrm{Hz}}}{2.95\times 10^{8}\ \mathrm{Hz/(V/cm)}}
\approx 3.4\times 10^{-6}\ \mathrm{V/cm}/\sqrt{\mathrm{Hz}}.
$$

$$
\boxed{\;\delta E_\mathrm{min}\approx 3.4\ \mathrm{\mu V/cm}/\sqrt{\mathrm{Hz}}
\;\;(\approx 340\ \mathrm{\mu V/m}/\sqrt{\mathrm{Hz}})\;}
$$

### 4.3 无 LO 直接测量对比

直接 AC-Stark 法 $\Delta\nu=\tfrac12|\alpha|E^{2}$，

$$
\delta E^{\text{no-LO}}_\mathrm{min}
=\sqrt{\dfrac{2\delta\nu_\mathrm{min}}{|\alpha|}}
=\sqrt{\dfrac{2\times 10^{3}}{1.4507\times 10^{10}}}
\approx 3.7\times 10^{-4}\ \mathrm{V/cm}/\sqrt{\mathrm{Hz}}.
$$

| 方式 | 灵敏度 |
|---|---|
| 纯 AC-Stark（无 LO） | ≈ 0.37 mV/cm/√Hz |
| LO 外差增强 | ≈ **3.4 μV/cm/√Hz** |
| **增益** | **~100 倍** |

---

## 5. 参数与结果汇总

| 项目 | 数值 |
|---|---|
| 原子 / 能级 | Cs，70D₅/₂ |
| 极化率 $\alpha$ | −14 507 MHz/(V/cm)² |
| 探测光波长 / 线宽 | 852 nm / 5 kHz |
| 耦合光波长 / 功率 / 线宽 | 509 nm / 500 mW / 5 kHz |
| 光束直径 × 长度 | 0.7 mm × 70 mm |
| 耦合光强度 | 130 W/cm² |
| 耦合光拉比频率 $\Omega_c/2\pi$ | ≈ 4 MHz |
| 激光线宽贡献 | ≈ 7 kHz |
| 渡越时间展宽 | ≈ 125 kHz |
| 功率展宽（主导） | ≈ 3 MHz |
| **EIT 总线宽 $\Delta\nu_\mathrm{EIT}$** | **≈ 3 MHz** |
| **最佳本地场 $E_\mathrm{LO}^\mathrm{opt}$** | **≈ 20 mV/cm** |
| 响应斜率 $k$ | ≈ 295 kHz/(mV/cm) |
| 鉴频分辨 $\delta\nu_\mathrm{min}$（假设） | 1 kHz/√Hz |
| **短波电场灵敏度 $\delta E_\mathrm{min}$** | **≈ 3.4 μV/cm/√Hz** |

---

## 6. 结论与优化方向

1. 当前参数下 EIT 线宽约 **3 MHz**，被 509 nm 耦合光的功率展宽主导。
2. 与此线宽匹配的最佳本地场 **$E_\mathrm{LO}\approx 20$ mV/cm**，在此偏置下
   AC-Stark 响应线性化，斜率 $\approx 295$ kHz/(mV/cm)。
3. 外差方案灵敏度达 **3.4 μV/cm/√Hz**，相比无 LO 方案提升约两个量级。
4. 进一步提升方向：
   - **降低耦合光功率或扩束**，把 $\Omega_c$ 降到接近 $\Gamma_e$ 以下，可使
     $\Delta\nu_\mathrm{EIT}$ 降至 ~100 kHz 量级；此时
     $E_\mathrm{LO}^\mathrm{opt}\to\sim 4$ mV/cm，$k$ 反而减小，但
     $\delta E_\mathrm{min}\propto\sqrt{\Delta\nu_\mathrm{EIT}}$ 整体下降，
     灵敏度可再提升 ~5 倍。
   - 提高探测光子数（增大光斑长度 70 mm 有利）以压低散粒噪声极限。
   - 使用频率锁定更窄的激光或冷原子样品以消除渡越时间展宽。
   - 采用共振腔增强探测或平衡零拍检测。

> 注：文中 6P₃/₂ → 70D₅/₂ 偶极矩采用 $\sim 0.01\,ea_0$ 的近似，实际值可由
> Cs 原子结构计算器（如 ARC）精确给出；若偶极矩偏差 2 倍，则 $\Omega_c^2$ 相应
> 变化 4 倍，功率展宽与结论数值需按此缩放，但分析框架不变。
