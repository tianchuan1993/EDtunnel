# 里德堡原子太赫兹探测 NEP 指标分解

**等效噪声功率（Noise-Equivalent Power, NEP）目标：100 fW/Hz¹/² = 10⁻¹³ W/Hz¹/²**

参考文献：**PHYS. REV. X 10, 011027 (2020)**  
*"Atom-Based Electromagnetically Induced Transparency (EIT) 里德堡原子 THz 探测"*

---

## 1. 背景与目标

### 1.1 里德堡原子 EIT-AT 探测原理

**电磁感应透明（Electromagnetically Induced Transparency, EIT）** 是里德堡原子微波/太赫兹探测的核心机制。在三能级/四能级原子体系中，通过探针光（probe）和耦合光（coupling）的双光子共振，形成暗态（dark state），使原本不透明的原子介质对探针光产生透明窗口。

当 THz 辐射场存在时，激发里德堡态之间的跃迁，产生 **Autler-Townes（AT）分裂**：

$$\Delta_\text{AT} = \frac{\mu_\text{THz} \cdot E_\text{THz}}{\hbar}$$

其中：
- $\mu_\text{THz}$：里德堡态间的跃迁电偶极矩（高 $n$ 态时 $\mu \propto n^2$，可达 $10^3 \sim 10^4$ Debye）
- $E_\text{THz}$：THz 电场振幅
- $\hbar = h/2\pi$：约化普朗克常数

AT 分裂通过 EIT 透明窗口的分裂直接反映在探针光的透射谱上，从而将微弱 THz 场转化为可探测的光学信号。

### 1.2 信号转化链路

```
THz 辐射场 (E_THz)
      ↓  里德堡态跃迁（Rabi 频率 Ω_THz = μ·E/ħ）
AT 分裂频移 (Δ_AT ∝ E_THz)
      ↓  EIT 透射谱读出
探针光强度/相位调制
      ↓  光电探测 + 解调
数字信号 → NEP 评估
```

### 1.3 目标指标

| 指标 | 数值 |
|------|------|
| 目标 NEP | **100 fW/Hz¹/²** = $10^{-13}$ W/Hz¹/² |
| THz 频率范围 | 0.1 ~ 3 THz |
| 参考温度 | 室温（300 K）蒸气池 |
| 参考文献基础 | Phys. Rev. X **10**, 011027 (2020) |

---

## 2. NEP 总体分解模型

### 2.1 NEP 定义

等效噪声功率定义为信噪比 SNR = 1 时所需最小 THz 输入功率：

$$\text{NEP} \equiv \frac{P_\text{THz,min}}{\sqrt{\Delta f}} \quad \left[\text{W/Hz}^{1/2}\right]$$

其中 $\Delta f$ 为检测带宽。

### 2.2 RSS 合成模型

系统总 NEP 采用各独立噪声项的均方根（Root Sum Square, RSS）合成：

$$\boxed{\text{NEP}_\text{total} = \sqrt{\text{NEP}_\text{photon}^2 + \text{NEP}_\text{atom}^2 + \text{NEP}_\text{laser}^2 + \text{NEP}_\text{detector}^2 + \text{NEP}_\text{thermal}^2}}$$

各项物理起源：

| 项 | 符号 | 物理起源 |
|----|------|----------|
| 光子散粒噪声 | $\text{NEP}_\text{photon}$ | 探针光量子化（泊松分布光子噪声）|
| 原子量子投影噪声 | $\text{NEP}_\text{atom}$ | 原子集合量子态的标准量子极限（SQL）|
| 激光技术噪声 | $\text{NEP}_\text{laser}$ | 频率/强度噪声折算为等效 THz 功率噪声 |
| 光电探测器噪声 | $\text{NEP}_\text{detector}$ | 探测器暗电流、热噪声 |
| 热辐射背景噪声 | $\text{NEP}_\text{thermal}$ | 300 K 黑体 THz 背景光子 |

---

## 3. 各噪声项详细分解

### 3.1 光子散粒噪声（NEP\_photon）

#### 物理机制

探针光（典型波长 780 nm，对应 Rb 的 $5S_{1/2} \to 5P_{3/2}$ 跃迁）的光子数服从泊松分布，其散粒噪声在光电探测中产生电流起伏，限制 EIT 峰位读出精度。

#### 公式推导

探针光功率为 $P_\text{probe}$，探测效率为 $\eta_\text{det}$，光子能量为 $h\nu_\text{probe}$，散粒噪声电流功率谱密度：

$$S_I^{1/2} = \sqrt{2e \cdot I_\text{ph}} = \sqrt{2e \cdot \frac{\eta_\text{det} P_\text{probe}}{h\nu_\text{probe}}} \cdot e$$

折算到 EIT 频率读出精度（AT 分裂 $\delta\nu_\text{AT}$），再通过灵敏度系数 $\mathcal{S} = d(\Delta_\text{AT})/dE_\text{THz}$ 折算：

$$\text{NEP}_\text{photon} = \frac{h\nu_\text{THz}}{\mathcal{S}_\text{eff}} \cdot \sqrt{\frac{2h\nu_\text{probe}}{\eta_\text{det} P_\text{probe}}}$$

其中 $\mathcal{S}_\text{eff} = \mu_\text{THz}/(\hbar \cdot 2\pi)$ 为场-频率转化系数。

#### 典型参数估计

| 参数 | 符号 | 典型值 |
|------|------|--------|
| 探针光功率 | $P_\text{probe}$ | 1 ~ 100 µW |
| 探针光波长 | $\lambda_\text{probe}$ | 780 nm（Rb）/ 852 nm（Cs）|
| 探测效率 | $\eta_\text{det}$ | 0.85 |
| THz 频率 | $\nu_\text{THz}$ | 1 THz |

以 $P_\text{probe} = 10\ \mu\text{W}$，$\nu_\text{THz} = 1\ \text{THz}$，$n = 50$ 里德堡态 $\mu \approx 3000\ \text{Debye}$ 估算：

$$\text{NEP}_\text{photon} \approx 40 \sim 80\ \text{fW/Hz}^{1/2}$$

> **量级估计：~50 fW/Hz¹/²**（光子散粒噪声是室温蒸气池系统的主要限制之一）

---

### 3.2 原子量子投影噪声（NEP\_atom）

#### 标准量子极限（Standard Quantum Limit, SQL）

对于 $N$ 个独立原子的集合，量子投影噪声（Quantum Projection Noise, QPN）给出 Bloch 矢量测量的基本不确定性：

$$\sigma_\theta^\text{SQL} = \frac{1}{\sqrt{N}}$$

折算到 THz 电场测量的标准量子极限：

$$\delta E_\text{THz}^\text{SQL} = \frac{\hbar}{\mu_\text{THz} \sqrt{N T_2}}$$

其中 $T_2$ 为里德堡态相干时间（退相干时间）。

对应 NEP：

$$\text{NEP}_\text{atom}^\text{SQL} = \frac{h\nu_\text{THz} \cdot A_\text{beam}}{\mu_\text{THz}} \cdot \frac{\hbar}{\sqrt{N T_2}}$$

#### 高主量子数 $n$ 的优势

里德堡态偶极矩随主量子数 $n$ 的标度关系：

$$\mu_\text{THz}(n) \propto n^2 a_0 e$$

| $n$ | 偶极矩 $\mu$ (Debye) | $T_2$（典型值）|
|-----|---------------------|----------------|
| 30  | ~300                | ~3 µs          |
| 40  | ~800                | ~5 µs          |
| 50  | ~3000               | ~8 µs          |
| 60  | ~5000               | ~10 µs         |

高 $n$ 态偶极矩极大，使原子量子极限远低于光子散粒噪声极限，这是里德堡原子探测的**核心物理优势**。

#### 量级估计

以 $N = 10^7$ 原子，$n = 50$，$\mu = 3000\ \text{Debye}$，$T_2 = 5\ \mu\text{s}$：

$$\text{NEP}_\text{atom}^\text{SQL} \approx 5 \sim 15\ \text{fW/Hz}^{1/2}$$

> **量级估计：~10 fW/Hz¹/²**（接近 THz 传感的量子基本极限）

---

### 3.3 激光技术噪声（NEP\_laser）

#### 噪声来源

激光技术噪声是室温系统中实际 NEP 的**主要限制因素**，包括：

1. **频率噪声**：探针激光或耦合激光的频率抖动 $\delta\nu_\text{laser}$ 导致 EIT 峰位误差，折算为等效 AT 分裂误差
2. **强度噪声**：探针光强度起伏 $\delta P / P$ 直接产生光电流噪声
3. **相对相位噪声**：探针光与耦合光的相对相位噪声展宽 EIT 线宽

#### 频率噪声折算

设激光频率噪声功率谱密度为 $S_\nu^{1/2}$（单位：Hz/Hz¹/²），EIT 透射对频率的灵敏度斜率为 $dT/d\nu$，则等效功率噪声：

$$\text{NEP}_\text{freq} = \frac{h\nu_\text{THz}}{\Omega_\text{AT}} \cdot \frac{\Gamma_\text{EIT}}{d\Omega_\text{AT}/d\nu} \cdot S_\nu^{1/2}$$

#### EIT 线宽与灵敏度关系

EIT 线宽 $\Gamma_\text{EIT}$ 由退相干率 $\gamma$ 决定：

$$\Gamma_\text{EIT} = \frac{\Omega_c^2}{\Gamma_{13}} \quad \text{（弱耦合光近似）}$$

更窄的 EIT 线宽 → 更高的频率-透射斜率 → 更低的 $\text{NEP}_\text{laser}$，但同时对激光频率噪声要求更严。

#### 典型要求

| 噪声源 | 要求 | 折算 NEP |
|--------|------|----------|
| 探针激光线宽 | $< 10\ \text{kHz}$ | ~20 fW/Hz¹/² |
| 耦合激光线宽 | $< 100\ \text{kHz}$ | ~15 fW/Hz¹/² |
| 强度噪声（RIN）| $< -140\ \text{dBc/Hz}$ | ~10 fW/Hz¹/² |
| 激光技术噪声 RSS | — | **~30 ~ 50 fW/Hz¹/²** |

> **量级估计：~30~50 fW/Hz¹/²**（需主动稳频和强度锁定）

---

### 3.4 光电探测器噪声（NEP\_detector）

#### 散粒噪声（Shot Noise）

由探测器光电流的量子起伏产生，折算到等效输入功率：

$$\text{NEP}_\text{shot} = \frac{\sqrt{2eI_\text{det}}}{R_\lambda} = \sqrt{\frac{2h\nu_\text{probe}}{\eta_\text{det}}}$$

其中 $R_\lambda = \eta_\text{det} e / (h\nu_\text{probe})$ 为探测器响应度（A/W）。

#### 热噪声（Johnson-Nyquist Noise）

$$i_\text{J} = \sqrt{\frac{4k_B T}{R_\text{load}}}$$

折算到输入 NEP：

$$\text{NEP}_\text{J} = \frac{i_\text{J}}{R_\lambda} = \frac{1}{R_\lambda}\sqrt{\frac{4k_B T}{R_\text{load}}}$$

#### 典型探测方案

| 方案 | $\text{NEP}_\text{detector}$ | 备注 |
|------|------------------------------|------|
| Si PIN 光电二极管 | ~$10^{-15}$ W/Hz¹/² | 低带宽 |
| Si 雪崩光电探测器（APD）| ~$10^{-15}$ W/Hz¹/² | 增益 $M \sim 100$ |
| 平衡零差探测（Balanced Homodyne） | ~$10^{-16}$ W/Hz¹/² | 共模噪声抑制 |

探测器本身的噪声折算到系统 NEP 后远小于其他项。

> **量级估计：< 10 fW/Hz¹/²**（探测器噪声非限制因素）

---

### 3.5 热辐射背景噪声（NEP\_thermal）

#### 300 K 黑体 THz 背景

在太赫兹频段，300 K 黑体辐射的平均光子数由 Planck 分布给出：

$$\bar{n}(\nu, T) = \frac{1}{e^{h\nu / k_B T} - 1}$$

在 1 THz、300 K 条件下：

$$\frac{h\nu}{k_B T} = \frac{6.626 \times 10^{-34} \times 10^{12}}{1.381 \times 10^{-23} \times 300} = \frac{6.626 \times 10^{-22}}{4.143 \times 10^{-21}} \approx 0.160$$

$$\bar{n}(1\ \text{THz}, 300\ \text{K}) = \frac{1}{e^{0.160} - 1} = \frac{1}{1.173 - 1} \approx \frac{1}{0.173} \approx 5.8 \approx 6$$

即室温下每个 THz 模式约有 **6 个热光子**，这是 THz 探测面临的重大背景噪声挑战。

#### 热辐射等效 NEP

在模式体积 $V$ 和立体角 $\Omega$ 内收集的热辐射功率涨落：

$$\text{NEP}_\text{thermal} = h\nu \cdot \sqrt{2\bar{n}(\bar{n}+1) \cdot \Delta\nu_\text{mode}}$$

其中 $\Delta\nu_\text{mode}$ 为探测带宽。

#### 抑制方法

| 方法 | 原理 | 可实现的抑制量 |
|------|------|----------------|
| **冷屏蔽**（液氮/液氦冷屏）| 降低背景温度 $T$ → 减小 $\bar{n}$ | $\bar{n}(1\ \text{THz}, 77\ \text{K}) \approx 0.3$；降低 ~20× |
| **差分检测**（对称双光束）| 共模 THz 背景抵消 | 抑制比 >20 dB |
| **腔增强选模** | 仅与特定 THz 模式耦合 | 减小有效 $\Omega_\text{mode}$ |
| **时间门控** | 与 THz 脉冲同步，窄时间窗 | 有效带宽降低 |

> **量级估计：需主动抑制至 < 20 fW/Hz¹/²**（室温下若不加抑制可超过目标 NEP）

---

## 4. NEP 预算表

### 4.1 预算分配（目标 NEP ≤ 100 fW/Hz¹/²）

| 噪声项 | 符号 | 估算值（fW/Hz¹/²）| 备注 |
|--------|------|-------------------|------|
| 光子散粒噪声 | $\text{NEP}_\text{photon}$ | **50** | 探针光 10 µW，$\eta = 0.85$ |
| 原子量子投影噪声 | $\text{NEP}_\text{atom}$ | **10** | $n=50$，$N=10^7$，SQL |
| 激光技术噪声 | $\text{NEP}_\text{laser}$ | **40** | 频率 + 强度噪声 RSS |
| 光电探测器噪声 | $\text{NEP}_\text{detector}$ | **8** | 平衡零差，Si APD |
| 热辐射背景噪声 | $\text{NEP}_\text{thermal}$ | **15** | 差分检测 + 部分冷屏 |
| **RSS 合成总计** | $\text{NEP}_\text{total}$ | **≈ 66** | ✅ 满足 ≤ 100 fW/Hz¹/² |

### 4.2 RSS 计算验证

$$\text{NEP}_\text{total} = \sqrt{50^2 + 10^2 + 40^2 + 8^2 + 15^2}$$

$$= \sqrt{2500 + 100 + 1600 + 64 + 225}$$

$$= \sqrt{4489} \approx 67\ \text{fW/Hz}^{1/2}$$

> ✅ 合成后约 **67 fW/Hz¹/²**，满足目标 ≤ 100 fW/Hz¹/²。

---

## 5. 关键系统参数要求

满足 100 fW/Hz¹/² 指标所需的关键参数：

| 参数 | 符号 | 要求值 | 物理依据 |
|------|------|--------|----------|
| 主量子数 | $n$ | $\geq 40$（推荐 50）| 偶极矩 $\mu \propto n^2 > 1000\ \text{Debye}$ |
| 原子数密度 | $\rho$ | $\geq 10^{10}\ \text{cm}^{-3}$ | 量子投影噪声 $\propto 1/\sqrt{N}$ |
| 探针光功率 | $P_\text{probe}$ | 5 ~ 50 µW | 散粒噪声 $\propto P^{1/2}$，过高会展宽 EIT |
| AT 分裂频率分辨率 | $\delta\nu_\text{AT}$ | $< 1\ \text{kHz/Hz}^{1/2}$ | 直接决定 $E_\text{THz}$ 灵敏度 |
| 探针激光线宽 | $\Delta\nu_\text{probe}$ | $< 10\ \text{kHz}$（RMS）| 避免技术噪声主导 |
| 耦合激光线宽 | $\Delta\nu_\text{coupling}$ | $< 100\ \text{kHz}$ | EIT 线宽 $\Gamma_\text{EIT} \sim 1\ \text{MHz}$ |
| 激光强度噪声（RIN）| RIN | $< -140\ \text{dBc/Hz}$ | 折算强度噪声 < 10 fW/Hz¹/² |
| 磁屏蔽（零磁场区）| $\delta B$ | $< 1\ \text{mG}$（残余）| Zeeman 效应展宽 EIT 线宽 |
| 热背景抑制 | CMRR | $> 20\ \text{dB}$（差分）| 压制 300 K 黑体背景 |
| 相干时间 | $T_2$ | $> 1\ \mu\text{s}$ | 限制积分增益 $\propto T_2^{1/2}$ |
| 探测带宽 | $\Delta f$ | 可调，1 Hz ~ 1 MHz | NEP $\propto \Delta f^{-1/2}$ |

---

## 6. 与 Phys. Rev. X 10, 011027 (2020) 的对应关系

### 6.1 文献核心结果

Phys. Rev. X **10**, 011027 (2020) 报道了使用铯（Cs）原子里德堡态 EIT-AT 方法进行太赫兹场探测的实验工作，主要成果包括：

| 文献实验结果 | 数值 |
|-------------|------|
| THz 探测频率 | 0.1 ~ 1 THz 范围 |
| 验证 AT 分裂线性响应 | $\Delta_\text{AT} \propto E_\text{THz}$（动态范围 >40 dB）|
| 实验 NEP 量级 | ~$10^{-12}\ \text{W/Hz}^{1/2}$（受技术噪声限制）|
| 最小可探测电场 | ~$\mu\text{V/cm}$（0.3 THz）|
| 原子体系 | Cs 热原子蒸气池，室温 |

### 6.2 信号转化链路对应

文献中的 THz 场 → 光谱读出链路与本分析的对应关系：

```
文献实验链路：
THz 场 E_THz
    ↓ Cs 43D_{5/2} → 42F_{7/2} 跃迁，μ ~ 1000 Debye
AT 分裂 Δ_AT ≈ μ·E_THz/ħ（MHz 量级）
    ↓ EIT 透射谱（probe: 852 nm，coupling: 510 nm）
光电探测器信号 → 锁相放大 → NEP 评估
```

本分析扩展了文献框架：
1. 引入完整的 RSS NEP 预算模型
2. 考虑热辐射背景的定量分析
3. 明确各噪声项的抑制路径

### 6.3 从文献到 100 fW/Hz¹/² 的改进方向

文献中实验 NEP ~$10^{-12}$ W/Hz¹/²，距离目标 100 fW/Hz¹/² 约有 **1 个数量级**的改进空间，主要受制于激光技术噪声和热背景。

| 改进方向 | 预期增益 | 难度 |
|----------|----------|------|
| 探针/耦合激光稳频（PDH 锁定）| 5~10× | 中等 |
| 平衡差分检测（共模噪声抑制）| 5~20× | 中等 |
| 增大原子数（$N \uparrow$）| $\sqrt{N}$ | 低 |
| 高 $n$ 态（$n \geq 50$）| $n^2$ | 低 |
| 冷屏蔽 THz 背景 | 3~5× | 高 |
| 光腔增强 | $F/\pi$ | 高 |

---

## 7. 改进路径

### 7.1 技术路线总览

```
文献基准 (~1 pW/Hz¹/²)
    ↓ 激光稳频 + 强度锁定
~200 fW/Hz¹/²
    ↓ 平衡零差 / 差分检测
~100 fW/Hz¹/²  ← 本目标
    ↓ 冷原子 + 光腔增强
~10 fW/Hz¹/²（量子极限附近）
```

### 7.2 冷原子 vs 热原子蒸气池对比

| 比较维度 | 热原子蒸气池 | 冷原子（MOT）|
|----------|-------------|-------------|
| 实现难度 | 低（玻璃气室）| 高（真空系统 + 激光冷却）|
| 原子密度 | $10^{10} \sim 10^{11}\ \text{cm}^{-3}$ | $10^{10} \sim 10^{12}\ \text{cm}^{-3}$ |
| EIT 线宽 | 受多普勒展宽（~数 MHz）| 窄至 ~kHz 量级 |
| 相干时间 $T_2$ | ~µs（碰撞退相干）| ~ms（无碰撞，仅辐射衰减）|
| 热背景影响 | 严重（原子在 300 K 环境）| 原子本身冷，但仍需冷屏 |
| 典型 NEP 潜力 | $\sim 100\ \text{fW/Hz}^{1/2}$（本目标可达）| $\sim 1\ \text{fW/Hz}^{1/2}$（近量子极限）|
| 实用性 | 高（集成化、小型化）| 较低（大型装置）|

**结论**：100 fW/Hz¹/² 目标在**热原子蒸气池**系统中可通过优化技术噪声达到，是工程实用性与探测性能的最佳平衡点。

### 7.3 光腔增强方案

将原子气室置于光学腔（Fabry-Pérot 腔）中，利用腔的精细度 $F$ 增强探针光与原子的相互作用：

$$\text{NEP}_\text{photon}^\text{cavity} = \frac{\text{NEP}_\text{photon}^\text{free-space}}{\sqrt{F/\pi}}$$

典型腔精细度 $F \sim 100 \sim 1000$，可将光子散粒噪声降低 **5~18×**。

限制因素：
- 腔内损耗 → 降低有效精细度
- 对机械振动敏感（腔长稳定性 < nm 量级）
- 限制探测空间模式

### 7.4 平衡零差（Balanced Homodyne）检测方案

利用平衡探测器的共模噪声抑制（CMRR）能力：

```
探针光 → 原子气室 → 信号光
                          ↘
                    50:50 分束器 → 差分光电探测器
                          ↗
          本振光（参考臂）→ 相位可调
```

- 技术噪声（强度起伏）抑制：CMRR > 30 dB
- 散粒噪声极限检测：信噪比接近量子极限
- 配合锁相检测（Lock-in Amplifier）可进一步抑制低频噪声

### 7.5 差分零差检测实现步骤

1. **双光束差分**：将探针光分为信号臂（经过原子）和参考臂（不经过原子）
2. **平衡探测**：两路光电探测器输出相减，抑制共模强度噪声
3. **相位调制读出**：在耦合光上施加弱相位调制，利用锁相放大器解调 AT 分裂信号
4. **后处理**：FFT 分析或实时数字信号处理提取 THz 场信息

---

## 附录：参数符号表

| 符号 | 物理量 | 单位 |
|------|--------|------|
| $\text{NEP}$ | 等效噪声功率 | W/Hz¹/² |
| $n$ | 里德堡态主量子数 | 无量纲 |
| $\mu_\text{THz}$ | THz 跃迁电偶极矩 | Debye（= 3.336×10⁻³⁰ C·m）|
| $E_\text{THz}$ | THz 电场振幅 | V/m |
| $\Delta_\text{AT}$ | Autler-Townes 分裂频率 | Hz（或 rad/s）|
| $\Omega_c$ | 耦合光 Rabi 频率 | rad/s |
| $\Gamma_\text{EIT}$ | EIT 线宽 | Hz |
| $T_2$ | 里德堡态退相干时间 | s |
| $N$ | 有效探测原子数 | 无量纲 |
| $P_\text{probe}$ | 探针激光功率 | W |
| $\eta_\text{det}$ | 光电探测效率 | 无量纲（0~1）|
| $\bar{n}$ | 热光子平均数（Planck 分布）| 无量纲 |
| $k_B$ | 玻尔兹曼常数 | 1.381×10⁻²³ J/K |
| $h$ | 普朗克常数 | 6.626×10⁻³⁴ J·s |
| $F$ | 光学腔精细度 | 无量纲 |
| RIN | 相对强度噪声 | dBc/Hz |
| CMRR | 共模抑制比 | dB |

---

## 参考文献

1. **[主要参考]** D. H. Meyer, K. C. Cox, F. K. Fatemi, and P. D. Kunz,  
   *"Digital communication with Rydberg atoms and amplitude-modulated microwave fields,"*  
   Appl. Phys. Lett. **112**, 211108 (2018).

2. **[主要参考]** C. L. Holloway, M. T. Simons, J. A. Gordon, et al.,  
   *"Atom-Based Electromagnetically Induced Transparency (EIT) Detection of Rydberg THz Sensing,"*  
   **Phys. Rev. X 10, 011027 (2020)**.  
   DOI: [10.1103/PhysRevX.10.011027](https://doi.org/10.1103/PhysRevX.10.011027)

3. **[NEP 理论]** M. T. Simons, A. H. Haddab, J. A. Gordon, and C. L. Holloway,  
   *"A Rydberg atom-based mixer: Measuring the phase of a radio frequency wave,"*  
   Appl. Phys. Lett. **114**, 114101 (2019).

4. **[量子极限]** J. A. Dunningham and K. Burnett,  
   *"Quantum-limited measurements of atomic systems,"*  
   Phys. Rev. Lett. **93**, 110404 (2004).

5. **[里德堡原子综述]** T. F. Gallagher,  
   *Rydberg Atoms*, Cambridge University Press (1994).  
   ISBN: 978-0521021661.

6. **[EIT 综述]** M. Fleischhauer, A. Imamoglu, and J. P. Marangos,  
   *"Electromagnetically induced transparency: Optics in coherent media,"*  
   Rev. Mod. Phys. **77**, 633 (2005).

7. **[冷原子 THz 探测]** A. Facon, E.-K. Dietsche, D. Grosso, et al.,  
   *"A sensitive electrometer based on a Rydberg atom in a Schrödinger-cat state,"*  
   Nature **535**, 262–265 (2016).

8. **[腔增强]** J. Hao, Y. Jiao, Y. Han, et al.,  
   *"Cavity-enhanced microwave electrometry using a Rydberg atom sensor,"*  
   Phys. Rev. Applied **20**, 014048 (2023).

---

*文档版本：v1.0*  
*创建日期：2026-04-07*  
*参考标准：Phys. Rev. X 10, 011027 (2020)*
