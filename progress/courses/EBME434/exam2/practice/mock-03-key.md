# Mock-03 Key（2026-11-03 上午出题；题目 PDF：Exam2-Mock03-50min.pdf，课程文件夹 Claude outputs）

## Blueprint
| 题 | Topic | 题型 | 范围/风格依据 | 针对弱点 | 答案依据 |
|---|---|---|---|---|---|
| P1 (30) | T7 写模型：控制体推导、单位、IC/BC 命名、Robin、无量纲 | 场景→模型 | 9/28 p3 三行；10/5 Robin；10/12 无量纲；HW3 Q1d；练习题 2/4 | A1 t/x；A3 Dirichlet/Neumann；漏 D；单位 | Verified computation (t_diff=500 s, group=0.25) |
| P2 (35) | T8 MoL 球坐标 + 一级反应 | 三行 + 边界 + 单位 + stiffness | 10/14 p3–4；练习题 1（柱→球迁移）；9/23 | A2 差分混用；给已知节点写 ODE；漏 1/rᵢ；抄题漏项 | Reasoned（格式按她 10/14） |
| P3 (35) | T7 稳态积分两次（环形、BC 与 Krogh 换边）+ T9 cable 参数/解/passive | 积分 + 概念 | 10/7 p3；HW3 Q2；10/23；练习题 3a；朋友笔记 | A5 解参数；先用含 C' 的 BC；λ∝√a；e^{+x/λ} 的取舍 | Verified computation（ODE 残差 4e-13；C'(r_i)=0；C(r_o)=C₀；min at r_i；因子 ½,2,¼,√2,1） |

## P1
(a) 守恒：A·Δx·∂C/∂t = J_x·A − J_{x+Δx}·A − Q·A·Δx → ∂C/∂t = −∂J/∂x − Q → J = −D∂C/∂x → **∂C/∂t = D ∂²C/∂x² − Q**。单位：每项 mol/(m³·s)；D[m²/s]·C/x²[mol/m⁵] ✓；Q[mol/(m³·s)] ✓。
(b) IC：C(x,0) = C_m。x=0：∂C/∂x(0,t) = 0（Neumann，impermeable support，零通量）。x=L：C(L,t) = C_m（Dirichlet，well-stirred medium 钉住浓度）。
(c) −D ∂C/∂x(L,t) = k_c [C(L,t) − C_m]（Robin/mixed）。k_c→∞ ⇒ C(L,t) = C_m（Dirichlet）；k_c→0 ⇒ ∂C/∂x(L,t)=0（insulated）。
(d) (i) t_diff = L²/D = 10⁻⁶/2×10⁻⁹ = **500 s**。(ii) 代 C=C_mψ, x=Lξ, t=(L²/D)τ：(C_mD/L²)∂ψ/∂τ = (DC_m/L²)∂²ψ/∂ξ² − Q ⇒ **∂ψ/∂τ = ∂²ψ/∂ξ² − QL²/(DC_m)**。群 = QL²/(DC_m) = (10⁻⁴·10⁻⁶)/(2×10⁻⁹·0.2) = **0.25** = t_diff/t_consume（t_consume = C_m/Q = 2000 s）：扩散比耗氧快 4 倍，梯度小。
评分点：三行推导 4；单位 3；反应项在体内不在 flux 里 3；BC 命名 + 理由 8；Robin 符号 −D 在 x=L 3；极限 3；t_diff 2；无量纲方程 2；群 + 含义 2。

## P2
(a) dCᵢ/dt = D[(2/rᵢ)(Cᵢ₊₁ − Cᵢ₋₁)/(2h) + (Cᵢ₊₁ − 2Cᵢ + Cᵢ₋₁)/h²] − kCᵢ，i=1…N。
(b) r=0：(C₁ − C₀)/h = 0 ⇒ C₀ = C₁ ⇒ dC₁/dt = D[(2/r₁)(C₂ − C₁)/(2h) + (C₂ − C₁)/h²] − kC₁。r=R：C_{N+1} = C_s ⇒ dC_N/dt = D[(2/r_N)(C_s − C_{N−1})/(2h) + (C_s − 2C_N + C_{N−1})/h²] − kC_N。r=0 不写 ODE：2/r₀ = 2/0 发散，用对称 BC 消掉 C₀。
(c) Cᵢ(0) = 0，i=1…N；N 个 ODE，N 个 IC；h = R/(N+1)。
(d) D(2/rᵢ)(ΔC)/(2h)：(m²/s)(1/m)(mol/m³)/m = mol/(m³·s)；D·ΔC/h²：(m²/s)(mol/m³)/m² = mol/(m³·s)；kC：(1/s)(mol/m³) ✓ 三项同单位。
(e) |λ_max| ≈ 4D/h² ⇒ h 减半 → ×4 ⇒ Δt_max = 2/|λ_max| **÷4**；用 ode15s / lsoda，理由：stiff。
评分点：三项各 3（一阶 2 项 ÷2h、二阶 3 项 ÷h²、−kCᵢ）+ 无 ∂ 1；i=1 4、i=N 4、r=0 理由 2；IC/计数/h 5；单位 5；÷4 + 理由 3，stiff solver 2。

## P3
(a) ∂C/∂t = D(1/r)∂/∂r(r∂C/∂r) − M，r_i<r<r_o；r=r_i：∂C/∂r(r_i,t) = 0（Neumann，sealed）；r=r_o：C(r_o,t) = C₀（Dirichlet，capillaries）。
(b) 0 = D(1/r)(rC')' − M ⇒ (rC')' = Mr/D ⇒ rC' = Mr²/(2D) + A。**先用 Neumann**：C'(r_i)=0 ⇒ A = −Mr_i²/(2D)。C' = Mr/(2D) − Mr_i²/(2Dr) ⇒ C = Mr²/(4D) − (Mr_i²/(2D)) ln r + B。**再用 Dirichlet**：C(r_o)=C₀ ⇒ B = C₀ − Mr_o²/(4D) + (Mr_i²/(2D)) ln r_o。
**C(r) = C₀ + (M/4D)(r² − r_o²) − (M r_i²/(2D)) ln(r/r_o)**。检查：C(r_o)=C₀ ✓；C'(r_i)=0 ✓；代回 ODE 残差 0 ✓。
(c) 最低在 **r = r_i**：C'(r) = (M/2D)(r − r_i²/r) ≥ 0 在 r ≥ r_i，C 从密封内壁单调升到供氧外壁；内壁离氧源最远且无通量进入。
(d) λ = √(r_m/r_a) [cm]，τ_m = r_m c_m [s]；r_m [Ω·cm]，c_m [F/cm]，r_a [Ω/cm]。
(e) r_m = ρ_mℓ/(2πa) → ×½；c_m = 2πaε/d → ×2；r_a = ρ_a/(πa²) → ×¼；λ² = r_m/r_a → ×2 ⇒ λ ×√2；τ_m = r_m c_m → ×1。
(f) λ²V'' − V = 0，试 e^{sx} ⇒ s = ±1/λ ⇒ V = Ae^{−x/λ} + Be^{x/λ}；x→∞ 有限 ⇒ B = 0；V(0)=V₀ ⇒ A = V₀ ⇒ **V = V₀e^{−x/λ}**。
(g) ∂V/∂t = (λ²/τ_m)∂²V/∂x² − (1/τ_m)V；D_eff = λ²/τ_m [cm²/s]，k_eff = 1/τ_m [1/s]。Passive：r_m、c_m 常数 ⇒ 线性，信号只衰减；active：膜电导随 V、t 变（g_Na(V,t), g_K(V,t)，HH 门控）⇒ 非线性，可再生动作电位。
评分点：PDE+BC 4；积分两次 + BC 顺序 8 + 检查 2；最低点 4；定义/单位 4；因子 5 个各 0.8；通解 2 + 取舍 3；D_eff/k_eff 2 + passive/active 2。
