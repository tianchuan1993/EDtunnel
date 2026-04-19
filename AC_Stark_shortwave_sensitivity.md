# 基于 AC‑Stark 效应的短波天线（Cs 70D₅/₂）灵敏度估算

> 通过 852 nm 探测光 + 509 nm 耦合光在 Cs 蒸气中建立 Rydberg‑EIT，利用 AC‑Stark 效应测量短波电场。
> 核心思路：**引入本地场 (Local Oscillator, LO) 做外差式放大，将未知短波场的灵敏度由 EIT 线宽主导的频率分辨率决定。**

---

## 1. 已知参数

| 量 | 数值 |
|---|---|
| 原子 | ¹³³Cs，300 K 蒸气 |
| 探测光波长 | 852 nm (6S₁/₂ → 6P₃/₂) |
| 耦合光波长 | 509 nm (6P₃/₂ → 70D₅/₂)，最大可用功率 500 mW |
| 激光线宽 (852/509) | 各 5 kHz |
| 束腰几何 | 直径 0.7 mm、长度 70 mm（可调） |
| 6P₃/₂ 自然线宽 Γₑ | 2π × 5.22 MHz |
| 70D₅/₂ 极化率 α | **−14 507 MHz / (V/cm)²** |
| 6P₃/₂ → 70D₅/₂ 偶极矩 μ_c | ≈ 0.0072 e·a₀ (≈ 6.1 × 10⁻³² C·m) |

---

## 2. 灵敏度的物理图像

短波频率 f_RF ≪ Rydberg 共振频率 → 场对能级的作用属 **AC‑Stark 频移 (非共振二阶响应)**：

$$
\Delta f \;=\; \tfrac12\,\alpha\,E_{\rm RF}^{2}
$$

若仅有待测弱场 E_sig，则 Δf ∝ E_sig²，灵敏度随 E_sig→0 **迅速变差**。

引入同频或邻频的本地场 E_LO：

$$
E_{\rm RF}(t) = E_{\rm LO}\cos(\omega_{\rm LO}t) + E_{\rm sig}\cos(\omega_{\rm sig}t+\phi)
$$

代入后交叉项：

$$
\Delta f(t) \supset \alpha\,E_{\rm LO}\,E_{\rm sig}\cos(\Delta\omega\,t+\phi)
$$

这是一支 **正比于 E_sig 的拍频信号**。响应度

$$
\boxed{\;R \equiv \dfrac{\partial(\Delta f)}{\partial E_{\rm sig}} = \alpha\,E_{\rm LO}\;}
$$

越大灵敏度越高，而频率分辨率由 **EIT 线宽 Γ_EIT** 及光子散粒噪声共同决定：

$$
E_{\rm sig}^{\min}\big/\sqrt{\rm Hz}\;=\;\dfrac{\Gamma_{\rm EIT}}{2\,\alpha\,E_{\rm LO}\,(\mathrm{SNR}/\sqrt{\rm Hz})}
$$

因此 **Γ_EIT 越窄、E_LO 越大，灵敏度越高**；但 E_LO 不能太大，否则其自身 AC‑Stark 频移超过 EIT 特征而饱和 ——
最佳工作点约为 $|\alpha|E_{\rm LO}^2 \approx \tfrac12 \Gamma_{\rm EIT}$。

---

## 3. EIT 线宽的三大贡献

$$
\Gamma_{\rm EIT} \;\approx\; \underbrace{\dfrac{\Omega_c^{2}}{\Gamma_e}}_{\text{功率展宽}} \;+\; \underbrace{\dfrac{v_{\rm th}}{d}}_{\text{渡越展宽}} \;+\; \underbrace{\Delta\nu_{\rm laser}}_{\text{激光线宽}\;\approx\;10\text{ kHz}}
$$

- **耦合 Rabi 频率**：Ω_c = μ_c · E₅₀₉ / ℏ，其中 E₅₀₉ = √(4P /(π ε₀ c w₀²))，w₀ = d/2。
- Cs 室温平均热速度 v_th = √(8k_BT/πm) ≈ **218.6 m/s**。

### 3.1 功率‑光斑扫描（核心结果）

| P (mW) | d (mm) | Ω_c/2π (MHz) | Δν_pow (kHz) | Δν_transit (kHz) | **Γ_EIT (kHz)** |
|---:|---:|---:|---:|---:|---:|
| 500 | 0.7 | 4.08 | 3 183 | 49.7 | **3 243** |
| 200 | 1.0 | 1.81 | 624 | 34.8 | **669** |
| 100 | 2.0 | 0.64 | 78.0 | 17.4 | **105** |
|  50 | 2.0 | 0.45 | 39.0 | 17.4 | **66** |
|  50 | 3.0 | 0.30 | 17.3 | 11.6 | **38.9** ✅ |
|  30 | 3.0 | 0.23 | 10.4 | 11.6 | **32** |
|  20 | 3.0 | 0.19 |  6.9 | 11.6 | **28** |

> **结论**：500 mW × 0.7 mm 的默认参数功率展宽高达 ~3 MHz，**严重不利**。
> 把光斑扩大到 **d ≈ 3 mm** 并把 509 nm 功率降到 **~ 50 mW**，
> 三项贡献相互平衡（Δν_pow ≈ Δν_transit ≈ Δν_laser ≈ 10–20 kHz），
> Γ_EIT 降到 **≈ 40 kHz**，同时仍保留 Ω_c/2π ≈ 0.3 MHz 的可观 EIT 对比度。
> 进一步降功率收益有限，且 EIT 对比度会过低。

---

## 4. 选取的最优工作点

| 参数 | 取值 |
|---|---|
| 509 nm 功率 | **P = 50 mW**（总 500 mW 的 10 %） |
| 光斑直径 (1/e²) | **d = 3.0 mm** |
| 光斑长度 | 70 mm（不变） |
| Ω_c/2π | 0.30 MHz |
| 功率展宽 | 17.3 kHz |
| 渡越展宽 | 11.6 kHz |
| 激光贡献 | 10 kHz |
| **Γ_EIT (FWHM)** | **≈ 39 kHz** |

---

## 5. 本地场 (LO) 的选取

要求 LO 自身 AC‑Stark 频移不超过 EIT 特征的一半：

$$
|\alpha|\,E_{\rm LO}^{2} = \tfrac12 \Gamma_{\rm EIT}
\;\Longrightarrow\;
E_{\rm LO} = \sqrt{\dfrac{\Gamma_{\rm EIT}}{2|\alpha|}}
= \sqrt{\dfrac{39\,\text{kHz}}{2 \times 14.507\,\text{GHz/(V/cm)}^{2}}}
\approx \mathbf{1.16\;mV/cm}
$$

对应响应度：

$$
R = 2\,|\alpha|\,E_{\rm LO}
   = 2 \times 14.507\,\text{GHz/(V/cm)}^2 \times 1.16\times 10^{-3}\,\text{V/cm}
   \approx \mathbf{3.4\times 10^{7}\,Hz/(V/cm)}
$$

---

## 6. 灵敏度

散粒噪声极限下，EIT 线型频率读出噪声
Γ_EIT / (2·SNR/√Hz)；取典型 EIT 对比度 C ≈ 0.15，
探测光子率 Ṅ ≈ 10⁹ s⁻¹、总效率 η ≈ 0.5 → SNR/√Hz ≈ C √(ηṄ) ≈ **5 × 10³**。

$$
\delta f_{\min} \;=\; \dfrac{\Gamma_{\rm EIT}}{2\,(\mathrm{SNR}/\sqrt{\rm Hz})}
\;=\; \dfrac{39\,\text{kHz}}{10^{4}}
\;\approx\; \mathbf{3.9\;mHz/\sqrt{Hz}}
$$

再经 LO 放大，得到短波场灵敏度：

$$
\boxed{\;
E_{\rm sig}^{\min} \;=\; \dfrac{\delta f_{\min}}{R}
\;\approx\; \mathbf{1.2\times 10^{-7}\;V/cm/\sqrt{Hz}}
\;=\; \mathbf{116\;nV/cm/\sqrt{Hz}}
\;}
$$

对应功率通量谱密度：

$$
S_{\min} = \tfrac12\varepsilon_0 c\,E_{\rm sig}^{\min\,2}
\;\approx\; 1.8\times 10^{-17}\,\text{W/m}^{2}/\text{Hz}
\;\approx\; -137.5\;\text{dBm/m}^{2}/\text{Hz}
$$

---

## 7. 参数对照与结论

| 方案 | 509 nm 功率 | 光斑 d | Γ_EIT | E_LO | **灵敏度** |
|---|---:|---:|---:|---:|---:|
| 题目默认 | 500 mW | 0.7 mm | 3.2 MHz | 10.5 mV/cm | ~ 1 µV/cm/√Hz |
| **本文最优** | **50 mW** | **3.0 mm** | **39 kHz** | **1.16 mV/cm** | **≈ 116 nV/cm/√Hz** |

把 509 nm 功率从 500 mW 降到 50 mW、把光束从 0.7 mm 扩到 3 mm，可使
**EIT 线宽缩小近两个数量级，短波探测灵敏度提升约一个数量级**，达到 **~ 10²
nV cm⁻¹ Hz⁻¹/²** 量级，与国际上 Rydberg 外差电场计的实验值（几十 nV/cm/√Hz）相符。

---

### 符号速查
- α = −14 507 MHz/(V/cm)²：70D₅/₂ 标量极化率
- Ω_c：509 nm 耦合光 Rabi 频率
- Γₑ：6P₃/₂ 自发辐射速率
- v_th：Cs 热速度
- d：激光束 1/e² 直径（即渡越特征长度）
- R = ∂(Δf)/∂E_sig = α E_LO：外差响应度
- SNR/√Hz：每 √Hz 积分带宽内的信噪比（散粒噪声极限）
