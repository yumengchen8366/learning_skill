# Oral Practice 01 · Key（Exam 1 口试模拟，2026-10-25）

**不要在作答前看。** 题目在聊天中给出（也抄录在文末）。

## Blueprint

| 题 | Topic | 题型 | 范围/风格依据 | 针对弱点 | 答案依据 |
|---|---|---|---|---|---|
| P1 | T5 不动点 + Jacobian 分类（2D 非线性） | 白板推导，4 步 | Sept 21 Equilibrium & Stability 的 Pathogen–Immune 例题；用户回忆 Exam 1 考了"再难一点"的版本 | C-01（det→tr→判别式顺序；"有虚部就不收敛"误解） | Verified computation（sympy，2026-10-25） |
| P2 | T4 MM/QSSA 推导 + 可辨识性（加一个变量） | 白板推导 + 简答 | Sept 9 / Sept 14 MM；用户回忆 Exam 1 考了"加入其他变量"的 MM 可辨识题 | C-03 极限情形；QSSA 合法性解释（短回想中误解） | Verified computation（sympy 验证 v 表达式） |

原创情境：P1 给 pathogen 加 logistic 容量 K（课堂例题没有）；P2 加竞争性抑制剂 I（课堂没讲）。

---

## P1 Key

系统：dP/dt = rP(1 − P/K) − aPI，dI/dt = bPI − kI；r=1, K=10, a=1, b=0.5, k=2。

**(a) 不动点**：令两式为 0。第二式 I(bP − k)=0 → I=0 或 P=k/b=4。
- I=0 代入第一式：P(1−P/10)=0 → P=0 或 10 → **(0,0)、(10,0)**
- P=4：1·(1−4/10) − I = 0 → **I = 0.6** → **(4, 0.6)**。一般式 I* = (r/a)(1 − k/(bK))，需要 bK>k 才有生物意义。

**(b) Jacobian**：J = [[r − 2rP/K − aI, −aP], [bI, bP − k]]

**(c) 分类**
| 不动点 | J | tr | det | 特征值 | 类型 |
|---|---|---|---|---|---|
| (0,0) | [[1,0],[0,−2]] | −1 | **−2 <0** | 1, −2 | **saddle**（det<0 直接定） |
| (10,0) | [[−1,−10],[0,3]] | 2 | **−3 <0** | 3, −1 | **saddle** |
| (4,0.6) | [[−0.4,−4],[0.3,0]] | **−0.4** | **1.2** | −0.2 ± 1.077i | **stable spiral** |

一般式（内部点）：tr = −rk/(bK) < 0，det = rk(1 − k/(bK)) > 0。

**(d) 和课堂例题对比**：课堂版（无 K）内部点 tr = 0 → 纯虚 → 中性稳定、永久振荡。加入 logistic 自限项后 J₁₁ 从 0 变成 −rk/(bK) < 0 → tr<0 → **阻尼螺旋，收敛到 (4,0.6)**。
→ **纠正规则**：虚部只决定"是否绕圈"，收不收敛由实部（tr 符号）决定。有虚部 + 负实部 = 转着圈收敛。

**(e) 反馈类型**：J₁₂·J₂₁ = (−4)(0.3) < 0 → 负反馈（pathogen 促进 immune，immune 抑制 pathogen）。

---

## P2 Key

反应：S + E ⇌(k₁,k₋₁) ES →(k₂) P + E；I + E ⇌(k₃,k₋₃) EI。

**(a) Mass action ODE**（6 个量 s, e, c, c_I, p, i）
- ds/dt = −k₁se + k₋₁c
- dc/dt = k₁se − (k₋₁+k₂)c
- dc_I/dt = k₃ie − k₋₃c_I
- de/dt = −k₁se + k₋₁c + k₂c − k₃ie + k₋₃c_I
- dp/dt = k₂c
- di/dt = −k₃ie + k₋₃c_I

**(b) 守恒**：酶 e + c + c_I = e₀；底物 s + c + p = s₀；抑制剂 i + c_I = i₀。用 e = e₀ − c − c_I 消去 e 方程。

**(c) QSSA**（dc/dt ≈ 0, dc_I/dt ≈ 0）：
- c_I = (k₃/k₋₃) i e = (i/K_I) e，K_I = k₋₃/k₃
- c = (s/Km) e，Km = (k₋₁+k₂)/k₁
- e₀ = e(1 + s/Km + i/K_I) → c = e₀ s / (Km + s + Km·i/K_I)

**v = dp/dt = k₂c = Vmax·s / (Km(1 + i/K_I) + s)**，Vmax = k₂e₀。（sympy 验证一致）

**(d) 可辨识性**：从 v–s 数据（固定 i）只能拟合两个数：Vmax 和 **表观 Km_app = Km(1 + i/K_I)**。
- 可辨识：Vmax = k₂e₀（若 e₀ 已知则 k₂ 可得）；Km_app。
- 若在多个 i 水平做实验：Km（i=0 截距）和 K_I 可分开。
- **永远不可辨识**：k₋₁ 与 k₂ 分开（只以和出现在 Km 里）；k₃ 与 k₋₃ 分开（只以比值 K_I 出现）。
- 这是教授 takeaway 的延伸：机理模型 6 个速率常数 → 数据只能给 3 个组合。

**(e) 为什么 QSSA 用在 c 上而不是 s 上**：无量纲化后 c̃ 的方程带 1/ε，ε = e₀/s₀ ≪ 1 → c 是快变量，几乎瞬间"追上"s 的当前值；s 是慢变量，整个反应过程就是 s 的消耗。dc/dt≈0 的意思是"c 相对自身的快时间尺度已平衡"，不是 c 不变（c 跟着 s 慢慢降）。i≪... 对 c_I 同理（e₀ 也远小于 i₀）。

**(f) 极限**：i=0 退回 MM；s ≫ Km(1+i/K_I) → v → Vmax（抑制剂挡不住饱和，因为竞争性抑制只改 Km 不改 Vmax）；s ≪ → 一级，斜率 Vmax/Km_app 变小。

---

## 题目抄录

**P1**（白板，约 12 分钟）A pathogen population P(t) grows logistically with carrying capacity K and is killed by immune cells I(t); immune cells proliferate in response to pathogen and die naturally:
dP/dt = rP(1 − P/K) − aPI, dI/dt = bPI − kI, with r=1, K=10, a=1, b=0.5, k=2 (units omitted).
(a) Find all fixed points. (b) Write the Jacobian. (c) Classify each fixed point (eigenvalues or tr/det). (d) The in-class version had no carrying capacity and gave a neutrally stable center. What changed, and why? (e) Is the P–I interaction positive or negative feedback? Justify from the Jacobian.

**P2**（白板，约 12 分钟）An enzyme E converts substrate S to product P through complex ES (rates k₁, k₋₁, k₂). A competitive inhibitor I also binds E reversibly to form an inactive complex EI (rates k₃, k₋₃).
(a) Write the mass-action ODEs. (b) State the conservation laws and use them to reduce the system. (c) Apply QSSA to both complexes and derive v = dp/dt as a function of s and i. Define Vmax, Km, K_I. (d) From v-vs-s data at one fixed inhibitor level, which parameters (or combinations) can be identified? Which can never be separated? (e) Why is QSSA applied to dc/dt and not to ds/dt? (f) What happens to v as s → ∞? Does the inhibitor change this limit?
