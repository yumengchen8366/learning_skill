# Mock-02 Key（简短复习题，2026-11-02 00:40 出题；题目在聊天里）

## Blueprint
| 题 | Topic | 题型 | 范围/风格依据 | 针对弱点 | 答案依据 |
|---|---|---|---|---|---|
| Q1 | T7 特征尺度/无量纲 | 计算+判断 | HW3 Q1；10/5、10/12 | 单位、kL²/D 的意义 | Verified computation (Python) |
| Q2 | T7 柱坐标稳态扩散-反应 | 建模+BC+积分两次 | HW3 Q2（球）、Krogh（柱）、练习题 2 | A1 t/x；A3 Dirichlet/Neumann；A5 "解函数不解参数" | Verified computation (手算+代回验证) |
| Q3 | T8 MoL on cable eq | 手写离散格式 | HW3 Q3、练习题 1；10/14 + 10/23 | A2 差分公式；ghost node；stiffness 接口 | Reasoned |
| Q4 | T8b/T9 Nernst + cable 参数 | 计算+概念 | 10/14、10/21、练习题 3b | λ∝√a、τ_m 与 a 无关 | Verified computation |

## Q1  D = 2×10⁻¹⁰ m²/s，L = 0.5 mm 贴片，一级降解 k = 1×10⁻³ s⁻¹
(a) t_diff = L²/D = (5×10⁻⁴)²/2×10⁻¹⁰ = 1250 s ≈ **21 min**。
(b) 10 min：ℓ = √(Dt) = √(2×10⁻¹⁰×600) = 3.5×10⁻⁴ m = **0.35 mm < 0.5 mm → 还没到对面**。
(c) ξ = x/L, τ = Dt/L², ψ = C/C₀ ⇒ ∂ψ/∂τ = ∂²ψ/∂ξ² − (kL²/D) ψ。
    kL²/D = 10⁻³ × 1250 = **1.25**（≈1：降解和扩散同样快，药物穿过贴片前约有 e⁻¹·²⁵ 的量损失量级；>>1 意味着到不了对面就被降解完）。

## Q2  圆柱组织柱，半径 R，表面 C(R)=C₀，零级耗氧 Q，稳态
(a) ∂C/∂t = D(1/r)∂/∂r(r ∂C/∂r) − Q。单位：每项 mol/(m³·s)。
(b) BC：C(R,t) = C₀（Dirichlet）；∂C/∂r|_{r=0} = 0（对称/零通量）。IC 本题稳态不需要。
(c) D(1/r)(rC')' = Q → rC' = Qr²/(2D) + A；r=0 有限（或 C'(0)=0）⇒ A=0
    C' = Qr/(2D) → C = Qr²/(4D) + B；C(R)=C₀ ⇒ B = C₀ − QR²/(4D)
    **C(r) = C₀ − Q(R² − r²)/(4D)**。代回验证：D·(1/r)·d/dr(r·Qr/(2D)) = D·(1/r)·(Qr/D) = Q ✓
(d) 中心不缺氧 ⇔ C(0) ≥ 0 ⇔ **C₀ ≥ QR²/(4D)**（或 R ≤ √(4DC₀/Q)）。

## Q3  τ_m ∂V/∂t = λ² ∂²V/∂x² − V，x=0 clamped V₀，x=L sealed，网格 i=0…N，h=L/N
(a) 内部 i=1…N−1：dVᵢ/dt = (λ²/τ_m)(Vᵢ₊₁ − 2Vᵢ + Vᵢ₋₁)/h² − Vᵢ/τ_m
(b) x=0：V₀ 已知，不写 ODE；i=1 方程里 Vᵢ₋₁ = V₀。
    x=L sealed ⇒ ∂V/∂x=0 ⇒ (V_{N+1} − V_{N−1})/(2h)=0 ⇒ V_{N+1}=V_{N−1}
    dV_N/dt = (λ²/τ_m)(2V_{N−1} − 2V_N)/h² − V_N/τ_m
(c) h 减半 → 最快时间尺度 ∝ h²/λ²·τ_m → 最大 |特征值| 变 4 倍 → Forward Euler 的 Δt 上限（2/|λ_max|）要**除以 4**；系统更 stiff，用 lsoda/ode15s。

## Q4  [Na]ₒ=145 mM，[Na]ᵢ=15 mM，T=310 K；轴突 a 变 2 倍
(a) RT/F = 8.314×310/96485 = 0.0267 V = 26.7 mV；E_Na = 26.7 × ln(145/15) = 26.7 × 2.27 ≈ **+61 mV**。
(b) λ = √(R_m a/(2ρ_i)) ∝ √a ⇒ **λ 变 √2 ≈ 1.41 倍**；τ_m = R_m C_m ⇒ **不变**。
(c) lumped：V = V₀e^{−t/τ_m}；降到一半 t½ = τ_m ln2 ≈ 0.69 τ_m。r_m 加倍 ⇒ τ_m 加倍 ⇒ t½ 加倍。
