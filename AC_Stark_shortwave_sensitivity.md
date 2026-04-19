# 基于 AC‑Stark 效应的短波天线灵敏度估算（Cs 70D₅/₂ + LO 外差增强）

> 通过 852 nm 探测光 + 509 nm 耦合光在 Cs 蒸气中建立 Rydberg‑EIT，利用 AC‑Stark 效应测量短波电场。
> 核心思路：**引入本地场 (Local Oscillator, LO) 做外差放大，将待测场的响应从 E² 提升到线性 E，并通过优化激光功率使 EIT 线宽与信噪比达到最佳平衡，实现灵敏度最大化。**

---

## 1. 已知参数

| 量 | 数值 |
|---|---|
| 原子 | ¹³³Cs，300 K 蒸气 |
| 探测光波长 | 852 nm（6S₁/₂ → 6P₃/₂） |
| 耦合光波长 | 509 nm（6P₃/₂ → 70D₅/₂），最大可用功率 **500 mW** |
| 激光线宽（852 nm / 509 nm） | 各 **5 kHz** |
| 激光光斑 | 直径 **d = 1.3 mm**（1/e²），长度 **L = 70 mm** |
| 6P₃/₂ 自然线宽 Γₑ | 2π × 5.22 MHz |
| 70D₅/₂ AC‑Stark 极化率 α | **−14 507 MHz/(V/cm)²** |
| 6P₃/₂ → 70D₅/₂ 跃迁偶极矩 μ_c | ≈ 0.0072 e·a₀ ≈ 6.1 × 10⁻³² C·m |

---

## 2. 灵敏度的物理图像

短波频率远低于 Rydberg 共振频率，场对 70D₅/₂ 能级的作用属于 **AC‑Stark 频移（二阶非共振响应）**：

$$
\Delta f = \tfrac{1}{2}\,\alpha\,E_{\rm RF}^{2}
$$

若仅有待测弱场 E_sig，Δf ∝ E_sig²，灵敏度随 E_sig → 0 迅速变差。

### 引入本地场 (LO)

$$
E_{\rm RF}(t) = E_{\rm LO}\cos(\omega_{\rm LO}t) + E_{\rm sig}\cos(\omega_{\rm sig}t+\phi)
$$

展开 AC‑Stark 后得到交叉项：

$$
\Delta f(t) \supset \alpha\,E_{\rm LO}\,E_{\rm sig}\,\cos(\Delta\omega\,t+\phi)
$$

这是一支**正比于 E_sig 的拍频信号**，外差响应度为：

$$
\boxed{R = \frac{\partial(\Delta f)}{\partial E_{\rm sig}} = \alpha\,E_{\rm LO}}
$$

最终的场灵敏度由 **EIT 线宽 Γ_EIT** 和 **EIT 信号的信噪比 (SNR)** 共同决定：

$$
\boxed{E_{\rm sig}^{\min}/\sqrt{\rm Hz} = \frac{\Gamma_{\rm EIT}}{2\,|\alpha|\,E_{\rm LO}\,(\mathrm{SNR}/\sqrt{\rm Hz})}}
$$

关键矛盾：
- **增大 509 nm 功率** → EIT 对比度 C 增大（SNR 提高），但功率展宽使 Γ_EIT 增大
- **减小 509 nm 功率** → Γ_EIT 缩窄，但 C 下降（SNR 降低）
- 需要**找到两者平衡**的最优功率

---

## 3. EIT 线宽的三大贡献

$$
\Gamma_{\rm EIT} \approx \underbrace{\frac{\Omega_c^{2}}{\Gamma_e}}_{\text{功率展宽}} + \underbrace{\frac{v_{\rm th}}{\pi\,w_0}}_{\text{渡越展宽}} + \underbrace{\Delta\nu_{\rm laser}}_{\approx\,10\,\text{kHz}}
$$

各项说明：

**① 功率展宽 Δν_pow = Ω_c² / Γₑ**

耦合光 Rabi 频率：

$$
\Omega_c = \frac{\mu_c \cdot E_{509}}{\hbar}\,,\qquad
E_{509} = \sqrt{\frac{4P}{\pi\varepsilon_0 c\,w_0^2}}
$$

其中 w₀ = d/2 = 0.65 mm 为束腰半径。

**② 渡越展宽 Δν_transit = v_th / (π w₀)**

Cs 室温热速度 v_th = √(8k_BT/πm) ≈ **218.6 m/s**，
原子横穿 Gaussian 光束的有效渡越展宽：

$$
\Delta\nu_{\rm transit} = \frac{v_{\rm th}}{\pi\,w_0} = \frac{218.6}{\pi \times 6.5 \times 10^{-4}} \approx \mathbf{107\;\text{kHz}}
$$

**③ 激光线宽** Δν_laser = 5 kHz + 5 kHz = **10 kHz**

---

## 4. EIT 对比度与信噪比模型

EIT 对比度（透射窗深度）由耦合 Rabi 频率与 Rydberg 退相干速率之比决定：

$$
C = \frac{\Omega_c^2}{\Omega_c^2 + \Gamma_e \cdot \gamma_{\rm deph}}
$$

其中 Rydberg 态退相干速率：

$$
\gamma_{\rm deph} = 2\pi(\Delta\nu_{\rm transit} + \Delta\nu_{\rm laser}) = 2\pi \times 117\;\text{kHz}
$$

探测光散粒噪声极限 SNR（每 √Hz 积分带宽）：

$$
\mathrm{SNR}/\sqrt{\rm Hz} = C \cdot \sqrt{\eta \cdot \dot{N}_{\rm ph}}
$$

取探测光子率 Ṅ ≈ 10⁹ s⁻¹（对应 ~230 nW @ 852 nm），探测效率 η = 0.5。

---

## 5. 功率扫描与最优化（核心结果）

光斑固定 d = 1.3 mm，扫描 509 nm 功率：

| P (mW) | Ω_c/2π (MHz) | Δν_pow (kHz) | Γ_EIT (kHz) | C (%) | SNR/√Hz | **E_min (nV/cm/√Hz)** |
|---:|---:|---:|---:|---:|---:|---:|
| 10 | 0.31 | 18.5 | 136 | 13.6 | 3 046 | 355 |
| 20 | 0.44 | 36.9 | 154 | 24.0 | 5 361 | 215 |
| 30 | 0.54 | 55.4 | 172 | 32.1 | 7 181 | 170 |
| 50 | 0.69 | 92.3 | 209 | 44.1 | 9 858 | 136 |
| 75 | 0.85 | 138 | 256 | 54.2 | 12 116 | 123 |
| 100 | 0.98 | 185 | 302 | 61.2 | 13 684 | 118 |
| **125** | **1.10** | **231** | **348** | **66.3** | **14 835** | **≈ 117** ✅ |
| 150 | 1.20 | 277 | 394 | 70.3 | 15 716 | 117 |
| 200 | 1.39 | 369 | 486 | 75.9 | 16 978 | 121 |
| 300 | 1.70 | 554 | 671 | 82.6 | 18 459 | 130 |
| 500 | 2.20 | 923 | 1 040 | 88.7 | 19 844 | 151 |

> **最优功率 P ≈ 125 mW**（约最大功率的 1/4），此时：
> - 功率展宽（231 kHz）与渡越展宽（107 kHz）为同一量级
> - EIT 对比度 C ≈ 66%，在信噪比和线宽之间取得最佳平衡
> - Γ_EIT ≈ 348 kHz

物理解释：功率过低时虽然线宽窄，但 EIT 信号极弱（C < 20%），SNR 不足导致频率读出噪声大；功率过高时对比度虽好（C > 80%），但功率展宽使 Γ_EIT 过大。灵敏度极小值恰在这两个极端的**折中点**。

---

## 6. 选取的最优工作点

| 参数 | 取值 |
|---|---|
| 509 nm 功率 | **P ≈ 125 mW** |
| 光斑直径 | d = 1.3 mm（固定） |
| 光斑长度 | L = 70 mm（固定） |
| Ω_c/2π | 1.10 MHz |
| 功率展宽 Δν_pow | 231 kHz |
| 渡越展宽 Δν_transit | 107 kHz |
| 激光贡献 Δν_laser | 10 kHz |
| **Γ_EIT (FWHM)** | **≈ 348 kHz** |
| EIT 对比度 C | **66 %** |
| SNR/√Hz（散粒噪声极限） | **≈ 1.5 × 10⁴** |

---

## 7. 本地场 (LO) 的最优选取

LO 自身 AC‑Stark 频移不能超出 EIT 特征线宽，否则拍频信号被 EIT 线型裁剪。最佳条件：

$$
|\alpha|\,E_{\rm LO}^{2} = \tfrac{1}{2}\,\Gamma_{\rm EIT}
$$

代入数值：

$$
E_{\rm LO} = \sqrt{\frac{\Gamma_{\rm EIT}}{2\,|\alpha|}}
= \sqrt{\frac{348\,\text{kHz}}{2 \times 14\,507\,\text{MHz/(V/cm)}^{2}}}
\approx \mathbf{3.5\;\text{mV/cm}}
$$

对应外差响应度：

$$
R = 2\,|\alpha|\,E_{\rm LO}
= 2 \times 14.507\,\text{GHz/(V/cm)}^2 \times 3.5 \times 10^{-3}\,\text{V/cm}
\approx \mathbf{1.0 \times 10^{8}\;\text{Hz/(V/cm)}}
$$

---

## 8. 最终灵敏度

散粒噪声极限下 EIT 频率读出噪底：

$$
\delta f_{\min} = \frac{\Gamma_{\rm EIT}}{2\,(\mathrm{SNR}/\sqrt{\rm Hz})}
= \frac{348\,\text{kHz}}{2 \times 1.5 \times 10^{4}}
\approx 11.8\;\text{mHz}/\sqrt{\rm Hz}
$$

经 LO 外差放大后，短波场灵敏度：

$$
\boxed{
E_{\rm sig}^{\min} = \frac{\delta f_{\min}}{R}
= \frac{11.8\,\text{mHz/}\sqrt{\text{Hz}}}{1.0\times10^{8}\,\text{Hz/(V/cm)}}
\approx \mathbf{117\;\text{nV/cm}/\sqrt{\text{Hz}}}
}
$$

对应最小可探测功率通量谱密度：

$$
S_{\min} = \tfrac{1}{2}\varepsilon_0\,c\,\left(E_{\rm sig}^{\min}\right)^{2}
\approx 1.8 \times 10^{-21}\;\text{W/m}^{2}/\text{Hz}
\approx \mathbf{-177\;\text{dBm/m}^{2}/\text{Hz}}
$$

---

## 9. 方案对照与结论

| 方案 | 509 nm 功率 | 光斑 d | Γ_EIT | EIT C | E_LO | **灵敏度** |
|---|---:|---:|---:|---:|---:|---:|
| 默认参数（未优化） | 500 mW | 1.3 mm | 1 040 kHz | 89 % | 6.0 mV/cm | ~ 151 nV/cm/√Hz |
| **本文最优** | **125 mW** | **1.3 mm** | **348 kHz** | **66 %** | **3.5 mV/cm** | **≈ 117 nV/cm/√Hz** |

### 关键结论

1. **EIT 线宽与信噪比的权衡决定最优功率**：在光斑固定为 d = 1.3 mm 时，渡越展宽约 107 kHz 为不可压缩的下限；509 nm 功率的作用是调节功率展宽和 EIT 对比度之间的平衡。

2. **最优 509 nm 功率约为 125 mW**（最大功率的 1/4）：此时功率展宽 ≈ 231 kHz（与渡越展宽同量级），EIT 对比度 C ≈ 66%（SNR 可观），Γ_EIT ≈ 348 kHz。

3. **最优本地场 E_LO ≈ 3.5 mV/cm**：满足 LO AC‑Stark 频移等于半线宽条件，响应度 R ≈ 10⁸ Hz/(V/cm)。

4. **可达灵敏度约 117 nV/cm/√Hz**（-177 dBm/m²/Hz），比未优化方案提升约 23%，与国际上 Rydberg 外差电场计的实验水平（几十至百余 nV/cm/√Hz）一致。

5. **进一步提升空间**：若增大光斑直径（如 d > 2 mm）可压低渡越展宽至 < 50 kHz，此时最优功率可进一步降低，Γ_EIT 有望降至 ~100 kHz 以下，灵敏度可望提升 2–3 倍。

---

### 符号速查

| 符号 | 含义 |
|---|---|
| α = −14 507 MHz/(V/cm)² | 70D₅/₂ AC‑Stark 标量极化率 |
| Ω_c | 509 nm 耦合光 Rabi 频率 |
| Γₑ = 2π × 5.22 MHz | 6P₃/₂ 自发辐射速率 |
| v_th ≈ 218.6 m/s | Cs 室温热速度 |
| d = 1.3 mm | 激光束 1/e² 直径（渡越特征长度） |
| C | EIT 对比度（透射窗深度） |
| γ_deph | Rydberg 态退相干速率 |
| R = α · E_LO | 外差响应度 |
| SNR/√Hz | 每 √Hz 带宽信噪比（散粒噪声极限） |

