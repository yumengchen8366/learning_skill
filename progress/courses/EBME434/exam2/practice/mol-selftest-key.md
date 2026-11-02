# MoL 自测 T1–T3 Key（2026-11-02 18:40；题目在项目文档 `Exam2-MoL专题-知识点与应用.md` §9）

依据：Reasoned（按 10/14 讲义格式手推，backward-difference Neumann）。

## T1  ∂C/∂t = D C_xx − Q；x=0 sealed；x=L C=C₀；C(x,0)=0
网格 x₀=0…x_{N+1}=L，h=L/(N+1)，未知 C₁…C_N。
- x=0 sealed：(C₁ − C₀)/h = 0 ⇒ C₀ = C₁
- x=L：C_{N+1} = C₀（给定值，写作 C_L 避免与节点 C₀ 混淆）
```
i=1:  dC₁/dt = D(C₂ − C₁)/h² − Q
i:    dCᵢ/dt = D(Cᵢ₊₁ − 2Cᵢ + Cᵢ₋₁)/h² − Q
i=N:  dC_N/dt = D(C_L − 2C_N + C_{N−1})/h² − Q
IC:   Cᵢ(0) = 0
```
陷阱：这次密封在左、Dirichlet 在右（和 HW3 Q3 相反）；−Q 不乘 Cᵢ。

## T2  柱 + D + kC；r=0 对称；r=R Robin
rᵢ = ih，h = R/(N+1)。
- r=0：C₀ = C₁（且 1/r₀ 发散不写 ODE）
- r=R：−D(C_{N+1} − C_N)/h = k_c C_{N+1} ⇒ C_{N+1} = C_N/(1 + k_c h/D)
```
i=1:  dC₁/dt = D[(1/r₁)(C₂ − C₁)/(2h) + (C₂ − C₁)/h²] − kC₁
i:    dCᵢ/dt = D[(1/rᵢ)(Cᵢ₊₁ − Cᵢ₋₁)/(2h) + (Cᵢ₊₁ − 2Cᵢ + Cᵢ₋₁)/h²] − kCᵢ
i=N:  dC_N/dt = D[(1/r_N)(C_{N+1} − C_{N−1})/(2h) + (C_{N+1} − 2C_N + C_{N−1})/h²] − kC_N，其中 C_{N+1} = C_N/(1 + k_c h/D)
```
检查：k_c=0 ⇒ C_{N+1}=C_N（回到她的 sealed）；k_c→∞ ⇒ C_{N+1}→0（Dirichlet 0）。

## T3  cable；x=0 sealed；x=L clamped V_L
```
(a) i=1:  dV₁/dt = (λ²/τ_m)(V₂ − V₁)/h² − V₁/τ_m          ← V₀ = V₁
    i:    dVᵢ/dt = (λ²/τ_m)(Vᵢ₊₁ − 2Vᵢ + Vᵢ₋₁)/h² − Vᵢ/τ_m
    i=N:  dV_N/dt = (λ²/τ_m)(V_L − 2V_N + V_{N−1})/h² − V_N/τ_m
(b) 稳态：0 = λ²(Vᵢ₊₁ − 2Vᵢ + Vᵢ₋₁)/h² − Vᵢ  ⇒  Vᵢ₊₁ − (2 + h²/λ²)Vᵢ + Vᵢ₋₁ = 0（三对角线性方程组）
(c) [λ²/τ_m] = cm²/s，和 D 同单位 ⇒ "just a diffusion model"
```
