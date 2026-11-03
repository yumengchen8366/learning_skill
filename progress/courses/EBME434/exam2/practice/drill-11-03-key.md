# 题型专练 Key（2026-11-03 15:30；题目 PDF：Exam2-题型专练.pdf）

**11/3 教授 office hour 确认：MoL 一阶导用 backward (Cᵢ − Cᵢ₋₁)/h。** 此前文档/key 里的 central 全部作废。

## A1 判断
1 PDE ✓ ｜ 2 BC Dirichlet ✓ ｜ **3 ✗ 不合法**：BC 不能用时间导数 → `∂C/∂x(L,t) = 0` ｜ 4 BC Neumann ✓ ｜ 5 IC ✓ ｜ **6 ✗ 不合法**：单位不符（左 mol/m⁴、右 mol/m³）→ `C(0,t) = C₀` ｜ 7 BC Robin ✓ ｜ 8 IC ✓

## A2
(i) **会变。** 密封只说"没东西穿过这面墙"，东西从另一端进来仍会在墙附近堆积，C(L,t) 随时间升高，直到稳态才不变。
(ii) `∂C/∂x = 0` 是**空间**上这一点左右一样高（切线水平）；`∂C/∂t = 0` 是这一点的**值**不随时间变。前者是你给的条件，后者是 PDE 算出来的结果——只有稳态时才处处为零。

## A3 翻译
1 `C(0,t) = C₀` Dirichlet ｜ 2 `−D∂C/∂x(L,t)=0 ⇒ ∂C/∂x(L,t)=0` Neumann ｜ 3 `∂C/∂r(0,t)=0` Neumann（对称） ｜ 4 `C(L,t)=0` Dirichlet ｜ 5 `D∂C/∂x(0,t)=k_c C(0,t)` Robin（x=0 面 +D；x=L 面 −D∂C/∂x=k_c(C−C∞)） ｜ 6 `C(x,0)=0` IC ｜ 7 `C_A2 = m₁C_A1` at x=L₁ 分配 ｜ 8 `−D_A1∂C_A1/∂x = −D_A2∂C_A2/∂x` at x=L₁ 通量连续

## A4 练习题 4 的 8 条
x=0：`C_A1(0,t) = C₀(t)` D ｜ `∂C_B1/∂x(0,t) = 0` N
x=L₁：`C_A2 = m₁C_A1` ｜ `−D_A1∂C_A1/∂x = −D_A2∂C_A2/∂x` ｜ `C_B2 = m₁C_B1` ｜ `−D_B1∂C_B1/∂x = −D_B2∂C_B2/∂x`
x=L₁+L₂：`C_A2 = 0` D ｜ `C_B2 = 0` D
IC：C_A2(x,0)=0、C_B1(x,0)=0、C_B2(x,0)=0（题给）；C_A1(x,0)=0（题没给，自补并注明）

## B1 平板
(a) `∂C/∂t = D∂²C/∂x² − Q`；x=0: `∂C/∂x(0,t)=0` N；x=L: `C(L,t)=C₀` D
(b) 稳态 `DC'' = Q` ⇒ `C' = (Q/D)x + A`；**用 C'(0)=0 ⇒ A=0**；`C = (Q/2D)x² + B`；**用 C(L)=C₀ ⇒ B = C₀ − QL²/(2D)**
   **C(x) = C₀ − Q(L² − x²)/(2D)**
(c) 最低在 **x=0**（离液池最远且密封）；不缺氧 ⇔ **C₀ ≥ QL²/(2D)**

## B2 实心球
(a) `∂C/∂t = D(1/r²)∂/∂r(r²∂C/∂r) − Q`；r=0: `∂C/∂r(0,t)=0`（或 C 有限）；r=R: `C(R,t)=C_s`
(b) `(r²C')' = (Q/D)r²` ⇒ `r²C' = Qr³/(3D) + A` ⇒ `C' = Qr/(3D) + A/r²`
   **A/r² 在 r→0 发散，浓度必须有限 ⇒ A = 0**
   `C = Qr²/(6D) + B`；C(R)=C_s ⇒ **C(r) = C_s − Q(R² − r²)/(6D)**
(c) **C_s ≥ QR²/(6D)**
(d) 平板 2D、柱 4D、球 6D —— 分母 = **2(n+1)D**，n = 0/1/2。几何越"外扩"，同样的 Q 造成的中心压降越小。

## B3 Krogh 柱壳
(a) `∂C/∂t = D(1/r)∂/∂r(r∂C/∂r) − M`，r_i<r<r_o；r_i: `C(r_i,t)=C₀` D；r_o: `∂C/∂r(r_o,t)=0` N
(b) `(rC')' = (M/D)r` ⇒ `rC' = Mr²/(2D) + A` ⇒ `C' = Mr/(2D) + A/r`
   **第一次积分后用 r_o 的零通量 BC（含 C′ 的那条）**：C'(r_o)=0 ⇒ `A = −Mr_o²/(2D)`
   `C = Mr²/(4D) − (Mr_o²/2D) ln r + B`；用 C(r_i)=C₀ 定 B
   **C(r) = C₀ + (M/4D)(r² − r_i²) − (M r_o²/2D) ln(r/r_i)**（= 她 10/7 p4）
(c) 最低在 **r = r_o**：C'(r) = (M/2D)(r − r_o²/r) < 0 在 r<r_o，C 从血管壁单调降到外缘；外缘离氧源最远。
(d) 柱：∫(A/r)dr = A ln r；球：∫(A/r²)dr = −A/r。差别来自算子里的 rⁿ 幂次。

## C1 平板 + 对流 + 反应
h = L/(N+1)，x_i = ih，未知 C₁…C_N
一般 i：`dCᵢ/dt = D(Cᵢ₊₁ − 2Cᵢ + Cᵢ₋₁)/h² − v(Cᵢ − Cᵢ₋₁)/h − kCᵢ`
i=1（C₀ = C_in 已知，不写 ODE）：`dC₁/dt = D(C₂ − 2C₁ + C_in)/h² − v(C₁ − C_in)/h − kC₁`
i=N（C_{N+1} = C_N）：`dC_N/dt = D(−C_N + C_{N−1})/h² − v(C_N − C_{N−1})/h − kC_N`
IC：`Cᵢ(0) = 0`，i=1…N；**N 个 ODE，N 个 IC**
单位：D/h² [1/s]、v/h [1/s]、k [1/s]，乘 C 后都是 mol/(m³·s)

## C2 实心球 MoL
一般 i：`dCᵢ/dt = D[(2/rᵢ)(Cᵢ − Cᵢ₋₁)/h + (Cᵢ₊₁ − 2Cᵢ + Cᵢ₋₁)/h²] − kCᵢ`
i=1：C₀ = C₁ ⇒ **一阶项 (2/r₁)(C₁ − C₁)/h = 0**；二阶项 (C₂ − 2C₁ + C₁)/h² = (C₂ − C₁)/h²
   `dC₁/dt = D(C₂ − C₁)/h² − kC₁`
i=N：C_{N+1} = C_s（只进二阶导）；**反应项是 −kC_N，不是 −kC_s**
   `dC_N/dt = D[(2/r_N)(C_N − C_{N−1})/h + (C_s − 2C_N + C_{N−1})/h²] − kC_N`
(d) r=0 处 2/r₀ 发散，不能写 ODE，用对称 BC 消掉 C₀
(e) |λ_max| ≈ 4D/h² ⇒ h 减半 ⇒ ×4 ⇒ **Δt 上限 ÷4**；更 stiff，用 ode15s/lsoda

## D1 Cable 参数
(a) 电流穿过膜：长度 = 膜厚 ℓ，截面 = 膜面积 2πaΔx ⇒ `R_m = ρ_m ℓ/(2πaΔx)` [Ω]；`r_m = R_m·Δx = ρ_m ℓ/(2πa)` [Ω·cm]
(b) 电流沿轴：长度 = Δx，截面 = πa² ⇒ `R_a = ρ_aΔx/(πa²)` [Ω]；`r_a = R_a/Δx = ρ_a/(πa²)` [Ω/cm]
(c) `c_m = C_m·2πa` [F/cm]（= C/Δx，C = C_m·2πaΔx）
(d) **两段膜并联**（越长漏得越多、总电阻越小，R_m ∝ 1/Δx）⇒ 乘 Δx 才与长度无关；**两段轴向串联**（越长电阻越大，R_a ∝ Δx）⇒ 除 Δx。电容并联相加 ⇒ 除 Δx。
(e) `λ = √(r_m/r_a) = √(ρ_m ℓ a/(2ρ_a))`，单位 √(Ω·cm ÷ Ω/cm) = cm ✓；`τ_m = r_m c_m = ρ_m ℓ C_m`，单位 Ω·cm × F/cm = Ω·F = s ✓
(f) a→3a：r_m **×1/3**（∝1/a）｜c_m **×3**（∝a）｜r_a **×1/9**（∝1/a²）｜λ² = r_m/r_a ∝ a ⇒ ×3 ⇒ λ **×√3**｜τ_m ∝ (1/a)(a) = 1 ⇒ **不变**

## D2 Cable 的解
(a) `∂V/∂t = (λ²/τ_m)∂²V/∂x² − (1/τ_m)V`；**D_eff = λ²/τ_m [cm²/s]，k_eff = 1/τ_m [1/s]**
(b) `τ_m dV/dt = −V` ⇒ `V = V₀e^{−t/τ_m}`；`V(t½) = ½V₀` ⇒ e^{−t½/τ_m} = ½ ⇒ **t½ = τ_m ln2 ≈ 0.69τ_m**；r_m 加倍 ⇒ τ_m = r_m c_m 加倍 ⇒ **t½ 加倍**
(c) 稳态：`λ²V'' − V = 0`，试 e^{sx} ⇒ λ²s² = 1 ⇒ s = ±1/λ ⇒ `V = Ae^{x/λ} + Be^{−x/λ}`
   **x→∞ 有限 ⇒ 扔掉 e^{+x/λ}，A = 0**；**V(0)=V₀ ⇒ B = V₀** ⇒ `V = V₀e^{−x/λ}`
(d) 一般 i：`dVᵢ/dt = (λ²/τ_m)(Vᵢ₊₁ − 2Vᵢ + Vᵢ₋₁)/h² − Vᵢ/τ_m`
   i=1（V₀ 已知）：`dV₁/dt = (λ²/τ_m)(V₂ − 2V₁ + V₀)/h² − V₁/τ_m`
   i=N（sealed ⇒ V_{N+1}=V_N）：`dV_N/dt = (λ²/τ_m)(−V_N + V_{N−1})/h² − V_N/τ_m`
(e) Passive：r_m、c_m 是常数 ⇒ 线性，信号只衰减。Active：膜电导随电压和时间变（g_Na(V,t)、g_K(V,t)）⇒ 非线性，能再生动作电位。

## E 膜电位
(a) `μ = μ⁰ + RT ln C + zFφ`；μ_in = μ_out ⇒ `zF(φ_in − φ_out) = RT ln(C_out/C_in)` ⇒ **E_ion = (RT/zF) ln([ion]_out/[ion]_in)**
(b) RT/F = 8.314×310/96485 = 0.0267 V = **26.7 mV**；单位 (J/(mol·K))·K ÷ (C/mol) = J/C = V ✓
(c) **E_K < 0**（负）：out/in = 5/140 < 1，ln 为负。**E_Na > 0**（正）：145/15 > 1，ln 为正。（数值：E_K ≈ −89 mV，E_Na ≈ +61 mV）
(d) 电容 = lipid bilayer（储电荷）；电阻 = ion channels（g = 1/R）；电池 = Nernst potential（该离子的平衡电位）
(e) KCL：`C_m dV_m/dt + (V_m − E)/R = 0` ⇒ `τ = RC_m`，解 `V_m = E + (V₀ − E)e^{−t/τ}`
(f) 见 D2(e)
