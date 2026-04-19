# 指标分析计算一：NEP ≤100 fW/√Hz 可行性分析（NA=0.06 修正版）

本文档对原始 NEP 可行性分析进行审核校正，并以 **NA = 0.06** 重新计算全部链路参数。

---

## 一、原始计算审核意见

对照原始文档，发现以下问题：

### 1. NA 取值前后不一致（主要问题）

| 位置 | 使用的 NA | 对应 η_collect |
| --- | --- | --- |
| 正文推导（arcsin 部分） | 写 arcsin(0.06) 但结果 4.01° 对应 NA≈0.07 | 0.12% |
| 汇总表标题 | 0.25 | — |
| 汇总表中光子率（步骤⑤⑥） | 0.25（隐含） | 1.59% |
| 灵敏度裕度分析基准值 | 0.25 | 1.59% |

**结论**：正文推导过程与汇总表/裕度分析使用了不同的 NA 值，导致 NEP 结果矛盾。

### 2. arcsin 参数笔误

正文写 $\theta = \arcsin(0.06) = 4.01°$，但 $\arcsin(0.06) = 3.44°$。实际 $\arcsin(0.07) = 4.01°$，说明原文实际 NA=0.07，书写时误写为 0.06。

### 3. 汇总表光子率不自洽

汇总表中步骤④标注 $\eta_{\text{collect}} = 0.12\%$（对应 NA≈0.07），但步骤⑤⑥光子率 $1.779 \times 10^6$ 和 $1.281 \times 10^6$ 对应的是 $\eta_{\text{collect}} = 1.59\%$（NA=0.25）。表内效率列与光子率列使用了不同的 NA。

### 4. 最差情况组合因子计算有误

原文给出全部最差叠加因子为 ×2.20，但逐项乘积：

$$
\sqrt{2} \times 1.18 \times 1.25 \times 1.07 \times 1.10 = 1.414 \times 1.18 \times 1.25 \times 1.07 \times 1.10 \approx 2.45
$$

正确的组合因子应为 **×2.45**，而非 ×2.20。

### 5. 其余计算验证

除上述问题外，三光子激发效率、THz 吸收截面、光学厚度、散粒噪声 NEP 公式等基本物理推导均合理。

---

## 二、以 NA = 0.06 重新计算

以下保持原文其他参数不变，仅将荧光收集 NA 统一为 **0.06**。

### 2.1 三光子里德堡态激发效率（不变）

**第一步** $6S_{1/2} \to 6P_{3/2}$（852 nm, 5 mW）：

$$
s_1 = \frac{I_{852}}{I_{\text{sat}}} = 579, \quad \rho_{6P} = \frac{s_1/2}{1 + s_1} = \frac{289.5}{580} \approx 50\%
$$

**第二步** $6P_{3/2} \to 7S_{1/2}$（1470 nm, 50 mW）：

$$
\Omega_{1470} = 2\pi \times 48\ \text{MHz}, \quad \Gamma_{7S} = 2\pi \times 1.81\ \text{MHz}
$$

$$
\eta_2 = \frac{\Omega_{1470}^2}{\Omega_{1470}^2 + \Gamma_{6P}\Gamma_{7S}} = \frac{2304}{2304 + 9.4} \approx 99.6\%
$$

**第三步** $7S_{1/2} \to 16P_{3/2}$（822 nm, 500 mW）：

$$
\Omega_{822} = 2\pi \times 14.5\ \text{MHz}, \quad \Gamma_{16P} = 2\pi \times 1.3\ \text{kHz}
$$

$$
\eta_3 \approx \frac{\Omega_{822}^2 / \Gamma_{16P}}{\Omega_{822}^2 / \Gamma_{16P} + \Gamma_{7S}} \approx 99.99\%
$$

**总里德堡态激发效率**（含多体效应、失谐等经验修正 $f_c \approx 0.002$）：

$$
\eta_{\text{Ryd}} = \rho_{6P} \times \eta_2 \times \eta_3 \times f_c \approx 0.5 \times 0.996 \times 0.9999 \times 0.002 = 1.0 \times 10^{-3}
$$

### 2.2 激发区里德堡原子数（单像素，不变）

单像素体积 $V = 1\ \text{mm} \times 1\ \text{mm} \times 1\ \text{mm} = 10^{-3}\ \text{cm}^3$：

$$
N_{\text{atom}} = n_{\text{Cs}} \times V = 10^{10} \times 10^{-3} = 10^7
$$

$$
N_{\text{Ryd}} = N_{\text{atom}} \times \eta_{\text{Ryd}} = 10^7 \times 10^{-3} = 10^4
$$

### 2.3 THz 与里德堡原子耦合（不变）

跃迁偶极矩 $16P_{3/2} \to 16D_{5/2}$：

$$
d = n^2 \cdot e a_0 = 256 \times 8.478 \times 10^{-30}\ \text{C·m} = 2.17 \times 10^{-27}\ \text{C·m} \approx 650\ \text{Debye}
$$

THz 吸收截面（$\nu = 0.32\ \text{THz}$，$\lambda = 937\ \mu\text{m} = 9.37 \times 10^{-4}\ \text{m}$）：

$$
\sigma_0 = \frac{3\lambda_{\text{THz}}^2}{2\pi} = \frac{3 \times (9.37 \times 10^{-4})^2}{2\pi} = \frac{3 \times 8.78 \times 10^{-7}}{6.283} = 4.19 \times 10^{-7}\ \text{m}^2
$$

$16D$ 态自然线宽：

$$
\Gamma_{16D} = \frac{\Gamma_0}{n_{\text{eff}}^3} \approx \frac{3.3 \times 10^7}{14.6^3} \approx 1.06 \times 10^4\ \text{s}^{-1} \approx 1.7\ \text{kHz}
$$

加上功率展宽及渡越展宽，有效吸收线宽 $\Delta\nu_{\text{atom}} \approx 100\ \text{kHz}$。

THz 信号线宽 $\Delta\nu_{\text{THz}} = 2\ \text{MHz}$，有效吸收比例：

$$
f_{\text{BW}} = \frac{\Delta\nu_{\text{atom}}}{\Delta\nu_{\text{THz}}} = \frac{100\ \text{kHz}}{2\ \text{MHz}} = 0.05
$$

里德堡原子面密度（沿 THz 传播方向，穿过 1 mm 激发区）：

$$
n_{\text{Ryd}}^{\text{col}} = n_{\text{Cs}} \times \eta_{\text{Ryd}} \times L = 10^{16} \times 10^{-3} \times 10^{-3} = 10^{10}\ \text{m}^{-2}
$$

共振光学厚度：

$$
OD_0 = n_{\text{Ryd}}^{\text{col}} \times \sigma_0 = 10^{10} \times 4.19 \times 10^{-7} = 4{,}190 \gg 1
$$

有效吸收率：

$$
\eta_{\text{abs}} = f_{\text{BW}} \times \min(OD_0,\, 1) = 0.05 \times 1 = 5\%
$$

### 2.4 THz 光子 → 527 nm 光子 → CCD 光电子（NA=0.06 更新）

**THz 光子能量与光子率**（不变）：

$$
E_{\text{THz}} = h\nu = 6.626 \times 10^{-34} \times 3.2 \times 10^{11} = 2.12 \times 10^{-22}\ \text{J}
$$

设入射 $P_{\text{THz}} = 1\ \text{pW} = 10^{-12}\ \text{W}$：

$$
\Phi_{\text{THz}} = \frac{P_{\text{THz}}}{E_{\text{THz}}} = \frac{10^{-12}}{2.12 \times 10^{-22}} = 4.72 \times 10^9\ \text{photons/s}
$$

**被吸收的 THz 光子率**（不变）：

$$
\dot{N}_{\text{abs}} = \Phi_{\text{THz}} \times \eta_{\text{abs}} = 4.72 \times 10^9 \times 0.05 = 2.36 \times 10^8\ \text{photons/s}
$$

**527 nm 荧光光子产生率**（分支比 55.7%，不变）：

$$
\dot{N}_{527} = \dot{N}_{\text{abs}} \times \eta_{\text{branch}} = 2.36 \times 10^8 \times 0.557 = 1.315 \times 10^8\ \text{photons/s}
$$

**荧光收集效率（NA = 0.06）** 🔄 更新：

$$
\theta = \arcsin(0.06) = 3.44°
$$

$$
\Omega = 2\pi(1 - \cos\theta) = 2\pi(1 - 0.99820) = 2\pi \times 0.00180 = 0.01131\ \text{sr}
$$

$$
\eta_{\text{collect}} = \frac{\Omega}{4\pi} = \frac{0.01131}{12.566} = 9.00 \times 10^{-4} = 0.090\%
$$

**光学系统透射率**（4 片透镜、8 个面，每面 $T=0.98$，不变）：

$$
T_{\text{optics}} = 0.98^8 = 0.851
$$

> 注：实际透镜片数待荧光收集光路设计完成后更新。此处按 4 片透镜（8 个面）保守估计。

**到达 CCD 的光子率** 🔄 更新：

$$
\dot{N}_{\text{CCD}} = \dot{N}_{527} \times \eta_{\text{collect}} \times T_{\text{optics}} = 1.315 \times 10^8 \times 9.00 \times 10^{-4} \times 0.851 = 1.007 \times 10^5\ \text{photons/s}
$$

**CCD 光电子产生率**（QE = 72%）🔄 更新：

$$
\dot{N}_{e^-} = \dot{N}_{\text{CCD}} \times QE = 1.007 \times 10^5 \times 0.72 = 7.25 \times 10^4\ e^-/\text{s}
$$

### 2.5 散粒噪声极限 NEP（NA=0.06 更新）

散粒噪声主导时，$1\ \text{Hz}$ 带宽内信噪比：

$$
SNR_{1\text{Hz}} = \sqrt{\dot{N}_{e^-}} = \sqrt{7.25 \times 10^4} = 269.3
$$

NEP：

$$
\boxed{NEP = \frac{P_{\text{THz}}}{SNR_{1\text{Hz}}} = \frac{1 \times 10^{-12}}{269.3} = 3.71 \times 10^{-15}\ \text{W/}\sqrt{\text{Hz}} = 3.71\ \text{fW/}\sqrt{\text{Hz}}}
$$

$$
NEP = 3.71\ \text{fW/}\sqrt{\text{Hz}} \ll 100\ \text{fW/}\sqrt{\text{Hz}} \quad \checkmark
$$

### 2.6 转换效率汇总（NA=0.06）

| 步骤 | 环节 | 效率 | 光子/电子率 (per pixel) |
| --- | --- | --- | --- |
| ① | THz 入射（$P=1\ \text{pW}$） | — | $4.72 \times 10^9\ /\text{s}$ |
| ② | 里德堡原子吸收 | $\eta_{\text{abs}} = 5\%$ | $2.36 \times 10^8\ /\text{s}$ |
| ③ | 527 nm 荧光分支比 | $\eta_{\text{branch}} = 55.7\%$ | $1.315 \times 10^8\ /\text{s}$ |
| ④ | 荧光收集（NA=0.06） | $\eta_{\text{collect}} = 0.090\%$ | $1.184 \times 10^5\ /\text{s}$ |
| ⑤ | 光学透射 | $T_{\text{optics}} = 85.1\%$ | $1.007 \times 10^5\ /\text{s}$ |
| ⑥ | CCD QE @527 nm | $QE = 72\%$ | $7.25 \times 10^4\ e^-/\text{s}$ |

**总系统效率**（THz 光子 → CCD 光电子）：

$$
\eta_{\text{total}} = \eta_{\text{abs}} \times \eta_{\text{branch}} \times \eta_{\text{collect}} \times T_{\text{optics}} \times QE
$$

$$
= 0.05 \times 0.557 \times 9.00 \times 10^{-4} \times 0.851 \times 0.72 = 1.536 \times 10^{-5}
$$

即每约 **65,100** 个 THz 光子产生 1 个 CCD 光电子。

### 2.7 灵敏度裕度分析（NA=0.06）

| 参数 | 基准值 | 最差估计 | NEP 变化因子 |
| --- | --- | --- | --- |
| 里德堡激发效率 $\eta_{\text{Ryd}}$ | $10^{-3}$ | $5 \times 10^{-4}$ | OD 仍 $\gg 1$，$\eta_{\text{abs}}$ 不变 |
| 原子吸收线宽 $\Delta\nu_{\text{atom}}$ | 100 kHz | 50 kHz | $\times\sqrt{2} = \times 1.41$ |
| 分支比 $\eta_{\text{branch}}$ | 55.7% | 40% | $\times\sqrt{55.7/40} = \times 1.18$ |
| 收集 NA | 0.06 | 0.05 | $\times\sqrt{0.090/0.0625} = \times 1.20$ |
| 光学透射率 | 85.1% | 75% | $\times\sqrt{85.1/75} = \times 1.07$ |
| QE @527 nm | 72% | 60% | $\times\sqrt{72/60} = \times 1.10$ |
| **全部最差叠加** | — | — | **$\times 2.36$** |

> NA=0.05 对应 $\theta = \arcsin(0.05) = 2.87°$，$\Omega = 2\pi(1 - \cos 2.87°) = 2\pi \times 0.00125 = 0.00785\ \text{sr}$，$\eta_{\text{collect}} = 0.00785/12.566 = 0.0625\%$。

**最差情况 NEP**：

$$
3.71 \times 2.36 = 8.76\ \text{fW/}\sqrt{\text{Hz}} \ll 100\ \text{fW/}\sqrt{\text{Hz}}
$$

---

## 三、与原始计算及 NA=0.6 版本对比

| 对比项 | 原文 (NA≈0.07) | 原文表 (NA=0.25) | NA=0.06 (本文) | NA=0.6 |
| --- | --- | --- | --- | --- |
| 收集半角 $\theta$ | 4.01° | 14.48° | 3.44° | 36.87° |
| 立体角 $\Omega$ | 0.0154 sr | 0.200 sr | 0.0113 sr | 1.257 sr |
| 收集效率 $\eta_{\text{collect}}$ | 0.12% | 1.59% | 0.090% | 10.0% |
| CCD 光电子率 | $9.65 \times 10^4\ e^-/\text{s}$ | $1.28 \times 10^6\ e^-/\text{s}$ | $7.25 \times 10^4\ e^-/\text{s}$ | $8.06 \times 10^6\ e^-/\text{s}$ |
| NEP | $3.2\ \text{fW/}\sqrt{\text{Hz}}$ | $0.883\ \text{fW/}\sqrt{\text{Hz}}$ | $3.71\ \text{fW/}\sqrt{\text{Hz}}$ | $0.352\ \text{fW/}\sqrt{\text{Hz}}$ |
| 最差情况 NEP | — | — | $8.76\ \text{fW/}\sqrt{\text{Hz}}$ | $0.841\ \text{fW/}\sqrt{\text{Hz}}$ |
| 对 100 fW/√Hz 裕度 | ~31× | ~113× | **~27×（最差 ~11×）** | ~284× |

---

## 四、结论

1. **原始计算物理框架合理**，三光子激发效率、THz 吸收截面、光学厚度、散粒噪声 NEP 推导均正确。
2. **原文主要问题是 NA 取值前后不一致**：正文推导用 NA≈0.07（误写为 0.06），汇总表和灵敏度分析用 NA=0.25，导致 NEP 结果自相矛盾。
3. **以 NA=0.06 重新计算后**：
   - 收集半角 $\theta = 3.44°$，立体角 $\Omega = 0.0113\ \text{sr}$；
   - 收集效率 $\eta_{\text{collect}} = 0.090\%$；
   - 系统总效率 $\eta_{\text{total}} = 1.54 \times 10^{-5}$，每约 65,100 个 THz 光子产生 1 个 CCD 光电子；
   - **NEP = 3.71 fW/√Hz**，远低于 100 fW/√Hz 指标；
   - 即使全部参数取最差值，NEP = 8.76 fW/√Hz，仍有 **超过 11 倍裕度**，指标 $\leq 100\ \text{fW/}\sqrt{\text{Hz}}$ 可靠满足。
4. **NA=0.06 是所有讨论中最保守的参数**，即便如此仍有充足裕度，证明系统设计方案鲁棒性良好。
