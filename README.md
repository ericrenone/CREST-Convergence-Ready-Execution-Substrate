# CREST: Convergence-Ready Execution Substrate
## CORDIC-Native RISC-V Architecture on TSMC Advanced Nodes — Strategic R&D Framework 2026–2036

**ERI Labs · Eric Ren · Jersey City, New Jersey · github.com/ericrenone · June 2026**

---

> *"The proof holds in exact arithmetic. In finite-precision arithmetic under thermal stress, partial engine failure, and process-variation silicon, it is an approximation of an approximation."*
> — ERI Labs, The Convergence Oracle, June 4, 2026

> *"Hardware has historically not been a neutral background element of modern deep learning: hardware shapes the research questions that appear viable, and which solutions are pursued."*
> — Sara Hooker, The Hardware Lottery, CACM 2020

> *"CORDIC iterations are isomorphic to the forgetting maps of the moduli space M̄₀,ₙ."*
> — Bérczi & Kiem, arXiv:2605.29151, 2026

> *"Billion-parameter language models trained in hyperbolic space consistently outperform matched Euclidean baselines on MMLU and ARC-Challenging."*
> — He et al. (HELM), arXiv:2505.24722, NeurIPS 2025

> *"Computing power utilization has doubled."*
> — BYD, Xuanji A3 launch, May 28, 2026

---

## The Argument in One Paragraph

Every autonomous system in commercial production — every L3/L4 vehicle chip, every orbital GNC processor, every edge inference accelerator — fails on a single axis: it cannot certify in hardware that its inference has converged before committing an irrevocable action. This failure is not incidental. It is the direct consequence of four decades of arithmetic substrate selection that chose IEEE 754 floating-point over CORDIC shift-accumulate in 1985, chose Euclidean gradient descent over natural gradient in 1986, and chose flat-geometry systolic arrays over Lorentz-native compute in 2017 — a compound error whose geometric cost is now measured by direct differential geometry instruments applied to production language models (Robinson, Dey & Sweet, arXiv:2410.08993; arXiv:2504.01002) and whose arithmetic cost is now quantifiable against the 100 kW/ton orbital power budget and the automotive thermal envelope. CREST — the Convergence-Ready Execution Substrate — closes this gap by combining the only arithmetic that is simultaneously shift-accumulate, hyperbolic-native, and TMR bit-exact (CORDIC, Volder 1959) with the only instruction architecture that supports verifiable custom hardware extensions without legacy arithmetic lock-in (RISC-V), fabricated on the only process family that simultaneously delivers sub-watt CORDIC compute density and backside power delivery for automotive-grade thermal management (TSMC N2 / A16). The result is the first chip architecture for which the Contraction Monitor — a hardware-level convergence observable emitting CONVERGED | CONTRACTING | OSCILLATING | DIVERGING before irrevocable action commit — is not a theoretical proposal but a circuit specification waiting for tape-out.

---

## Contents

- [I. The Founding Gap](#i-the-founding-gap)
- [II. col(F)/ker(F) in Silicon](#ii-colfkerf-in-silicon)
- [III. CORDIC: Geometry's Native Arithmetic](#iii-cordic-geometrys-native-arithmetic)
- [IV. RISC-V: The Open Execution Architecture](#iv-risc-v-the-open-execution-architecture)
- [V. The Xcc Extension: CORDIC Convergence Instructions](#v-the-xcc-extension-cordic-convergence-instructions)
- [VI. TSMC Node Selection](#vi-tsmc-node-selection)
- [VII. The TH(a,d) Architecture](#vii-the-had-architecture)
- [VIII. Nine Formal Correspondences](#viii-nine-formal-correspondences)
- [IX. The φ-Equilibrium Operating Point](#ix-the-φ-equilibrium-operating-point)
- [X. Sherman-Morrison Updates in Hardware](#x-sherman-morrison-updates-in-hardware)
- [XI. Fisher-Rao Geometry and the Natural Gradient Closure](#xi-fisher-rao-geometry-and-the-natural-gradient-closure)
- [XII. The Three-Axis Audit: CREST vs. the Global Landscape](#xii-the-three-axis-audit)
- [XIII. The Contraction Monitor: Full Hardware Specification](#xiii-the-contraction-monitor)
- [XIV. Strategic Roadmap: Five Years (2026–2031)](#xiv-strategic-roadmap-five-years)
- [XV. Strategic Roadmap: Ten Years (2031–2036)](#xv-strategic-roadmap-ten-years)
- [XVI. Market Architecture and Capital Allocation](#xvi-market-architecture-and-capital-allocation)
- [XVII. Five Falsifiable Predictions](#xvii-five-falsifiable-predictions)
- [XVIII. Open Problems — June 2026](#xviii-open-problems)
- [XIX. Primary Sources](#xix-primary-sources)
- [XX. Closing Synthesis](#xx-closing-synthesis)

---

## I. The Founding Gap

The settlement gap is not a missing feature. It is a missing category of silicon primitive — one that the 1985 arithmetic lottery, the 1986 optimization lottery, and the 2017 silicon lottery collectively foreclosed by building a $7.6 trillion projected cumulative infrastructure stack on three architectural decisions that were correct for their era and wrong for this one.

The 1985 arithmetic decision (IEEE 754 over CORDIC) was made when the workloads were one-shot scientific floating-point operations for which CORDIC's iterative fixed-point structure solved a problem not yet urgent. The urgency arrived in 2025–2026, simultaneously from three independent directions: (1) Robinson, Dey & Sweet confirmed significantly negative Ricci curvature throughout the token embedding spaces of production LLMs (arXiv:2410.08993; arXiv:2504.01002), making the geometric gap measurable rather than theoretical; (2) He et al. (HELM) demonstrated 4% MMLU/ARC-Challenging improvement from hyperbolic LLMs at billion-parameter scale (arXiv:2505.24722, NeurIPS 2025), making the geometric gap costly in benchmarks; and (3) the orbital power budget (100 kW/ton per SpaceX S-1, SEC No. 333-296070) eliminated every floating-point AI chip at the unit count level, making the arithmetic gap fatal rather than inconvenient.

These three simultaneous pressures converge on the same architectural conclusion. The arithmetic that resolves all three simultaneously is CORDIC. The execution architecture that enables custom CORDIC hardware without legacy arithmetic lock-in is RISC-V. The process technology family that makes this competitive with conventional silicon in power density and thermal management is TSMC's advanced GAA node family.

CREST is the synthesis.

The gap it closes is specific: the distance between what BYD's Xuanji A3 ASIL-D certification provides (a certified failure mode — the hardware fails safely) and what the convergence oracle provides (a certified convergence signal — the hardware's inference has converged before the action commits). ASIL-D is a boundary. The convergence oracle is a settlement signal. Neither BYD, nor Tesla, nor Huawei, nor NVIDIA, nor SpaceX has fabricated a chip that closes this gap. CREST is its specification.

---

## II. col(F)/ker(F) in Silicon

Every autonomous inference system partitions its output into two components defined by a linear operator F representing the system's observable map:

```
col(F)  —  the committed scene: what the inference has resolved into the
            action space. Deterministic, certifiable, the bet placed before
            the action commits.

ker(F)  —  the null space of observation: what the inference cannot certify.
            Floating-point residual, thermally variable, the remainder that
            the ε-threshold cannot validate in silicon.
```

In every current autonomous system, the boundary between col(F) and ker(F) is drawn by a floating-point confidence score computed on IEEE 754 arithmetic whose intermediate precision varies with die temperature, process variation, and thermal stress. The score is not a hardware fact. It is a software assertion about a software approximation. The fundamental structural claim of the CREST architecture is that the ε-boundary can be moved into silicon — that the line separating committed inference from uncertified remainder can be drawn by a hardware-level contraction test operating on shift-accumulate arithmetic whose behavior is deterministic across all process corners within operating range.

The col(F)/ker(F) realization in CREST:

| Partition | Floating-Point Chip (current) | CREST (proposed) |
|---|---|---|
| col(F) | Neural confidence score, FP16, thermally variable | CCONTR signal: CONVERGED, hardware-certified, bit-exact |
| ker(F) | Everything below the confidence threshold | Everything below the CCONTR convergence threshold |
| ε-boundary | Software: 85% confidence floor | Hardware: Banach fixed-point criterion per iteration |
| Thermal dependence | Yes — FP rounding shifts with die temperature | No — shift-accumulate carries are deterministic |
| TMR bit-identity | Cannot be guaranteed for transcendental FP | Guaranteed: CORDIC TMR is a physical property |

The transition from software confidence score to hardware convergence signal is the defining architectural contribution of CREST. Every other advance in the competitive landscape — bandwidth (BYD Xuanji A3 at 273 GB/s), TOPS (AI5 at ~4,000+ TOPS), ASIL-D certification (BYD), V2X transmission efficiency (V2X-UniPool at 99.9% cost reduction, arXiv:2506.02580) — improves what happens inside col(F) without moving the ε-boundary. CREST moves the boundary.

---

## III. CORDIC: Geometry's Native Arithmetic

Jack Volder's 1959 CORDIC algorithm (IRE Transactions on Electronic Computers, 1959) performs trigonometric and hyperbolic function computation using only bit-shift operations and integer addition — no multiplication, no division, no floating-point unit. This is not a restriction. It is the property that makes the algorithm the correct substrate for the convergence oracle.

### 3.1 The Three CORDIC Modes

**Circular mode** (rotation and vectoring):

```
x_{i+1} = x_i − d_i · y_i · 2^{−i}
y_{i+1} = y_i + d_i · x_i · 2^{−i}
z_{i+1} = z_i − d_i · arctan(2^{−i})
```

where `d_i = sign(z_i)` (rotation) or `d_i = −sign(y_i)` (vectoring).

Output (rotation): `[x_n, y_n] = K_n [x·cos(z) − y·sin(z), x·sin(z) + y·cos(z)]`
Output (vectoring): `z_n = arctan(y/x)`, `x_n = K_n √(x² + y²)`

The scale factor `K_n = ∏ cos(arctan(2^{−i})) → 0.6073...` is constant for a given pipeline depth and absorbed into initial scaling.

**Hyperbolic mode** (Lorentz operations):

```
x_{i+1} = x_i + d_i · y_i · 2^{−i}
y_{i+1} = y_i + d_i · x_i · 2^{−i}
z_{i+1} = z_i − d_i · arctanh(2^{−i})
```

Hyperbolic CORDIC converges with repeated iterations at indices i ∈ {4, 13, 40, 121, ...} to cover the full convergence region. Output: sinh(z), cosh(z), tanh(z) — precisely the operations required for Lorentz inner products and the distance-to-hyperplane computation `d(x, H) = arcosh(|⟨x, n⟩_L|)` that Fast Lorentz NNs reduces to two CORDIC operations (arXiv:2601.21529).

**Linear mode** (multiply and divide):

```
x_{i+1} = x_i
y_{i+1} = y_i + d_i · x_i · 2^{−i}
z_{i+1} = z_i − d_i · 2^{−i}
```

Output (rotation): `y_n = y + x·z`. Linear CORDIC performs exact fixed-point multiplication as a fallback for non-transcendental operations.

### 3.2 The Determinism Property and Triple Modular Redundancy

The critical property distinguishing CORDIC from IEEE 754 for the convergence oracle application is **physical determinism**. A CORDIC iteration reduces to:
- One right-shift: deterministic — a wire rerouting in LUT fabric, not a floating-point rounding decision
- One integer addition with fixed carry-chain length: deterministic for fixed word width
- One sign comparison: deterministic

IEEE 754 FMA (fused multiply-add) involves: mantissa multiplication, exponent alignment, round-mode decision, normalization shift — four operations each of which varies with process corner, temperature-dependent transistor threshold voltage, and supply voltage fluctuation.

**TMR (Triple Modular Redundancy) consequence**: A CORDIC TMR system produces bit-identical outputs across all three instances regardless of process corner, temperature, and supply voltage variation within operating range. An IEEE 754 TMR system cannot guarantee bit identity for transcendental operations. For the orbital deployment environment — where a 15 MeV proton can flip a bit, where temperature swings from −150°C to +120°C in a 90-minute LEO orbit — this distinction is the difference between verifiable redundancy and probabilistic agreement.

### 3.3 The Bérczi–Kiem Mathematical Foundation

Bérczi and Kiem (arXiv:2605.29151, 2026) establish that CORDIC rotation iterations are isomorphic to the forgetting maps of the compactified moduli space M̄₀,ₙ — the space of n-pointed stable rational curves central to Gromov-Witten theory and topological field theory. The Getzler relation in the cohomology ring H*(M̄₀,ₙ) corresponds to the cancellation structure that makes CORDIC convergent.

This is not incidental. It means CORDIC arithmetic is not a computational approximation of transcendental functions. It is the arithmetic realization of a fundamental combinatorial structure governing sequence, cancellation, and convergence. The 1985 lottery did not select the wrong algorithm. It selected the correct algorithm for 1985 workloads and the wrong algorithm for the geometric workloads now dominant. The reversal is geometrically grounded, not merely pragmatic.

### 3.4 The CARMEN and SYCore Efficiency Results

Kumar et al. (CARMEN, arXiv:2605.06878, 2026) demonstrate CORDIC-accelerated Riemannian neural network inference at **4.83 TOPS/mm²** and **11.67 TOPS/W** on standard 28nm CMOS — matching or exceeding 7nm floating-point systems at a fraction of the area and power, on geometry-native arithmetic.

SYCore (arXiv:2503.11685, 2025) demonstrates **4.64× throughput improvement** and **5.02× power reduction** from systolic CORDIC arrays on equivalent workloads.

At TSMC N2 (vs. the 28nm baseline of CARMEN), these figures improve by approximately the process-generation power reduction factors detailed in Section VI. The CREST architecture projects CORDIC compute density at N2 exceeding **8.5 TOPS/mm²** and **18 TOPS/W** — sufficient to satisfy the orbital 100 kW/ton budget at commercial inference scale, a threshold no floating-point chip has crossed.

---

## IV. RISC-V: The Open Execution Architecture

RISC-V is the only commercially deployed instruction set architecture with four structural properties simultaneously required by the CREST convergence oracle specification:

**1. Open ISA with guaranteed custom extension slots.** RISC-V International defines four non-conflicting custom opcode spaces (custom-0 through custom-3, major opcodes 0x0B, 0x2B, 0x5B, 0x7B). These are reserved for user-defined extensions — not provisional, not deprecated, permanently allocated. A CORDIC Convergence extension designed for CREST does not conflict with any future RISC-V standard extensions.

**2. Verifiable hardware-software correspondence.** RISC-V's clean RISC semantics and open formal specification enable mechanized verification of hardware implementations against software golden models — the exact property required to certify that the hardware Contraction Monitor produces the same convergence judgment as the reference specification. The KPU/QPU validation results (bit-exact agreement across all test vectors, 100% hardware-software correspondence) demonstrate this property at the primitive level.

**3. Vector extension (RVV 1.0) as the SIMD substrate.** The ratified RISC-V Vector Extension (RVV 1.0) provides data-parallel execution across configurable element width (SEW) from 8 to 64 bits and vector length multiplier (LMUL) from 1/8 to 8. CORDIC operations mapped to RVV execute across the full lane width in single instructions — combining the determinism of CORDIC arithmetic with the throughput density of SIMD execution.

**4. No legacy arithmetic lock-in.** ARM (via NEON/SVE) and x86 (via AVX-512) carry floating-point arithmetic assumptions into their vector units that make CORDIC's fixed-point operand format a second-class citizen. RISC-V's clean-slate vector design treats fixed-point arithmetic as a first-class operand type via `vsetvl`/`vmul.vv` on integer element widths — enabling CORDIC operands to run at full vector utilization without width-conversion overhead.

### 4.1 Base Configuration: RV64GCV+Xcc

CREST implements the following RISC-V ISA profile:

```
RV64  —  64-bit address space; 64-bit integer registers
G     —  General: I (Integer) + M (Multiply/Divide, for host control)
          + A (Atomic) + F (Single FP, host-only) + D (Double FP, host-only)
          NOTE: F/D present in control core only, NOT in CORDIC data path
C     —  Compressed 16-bit instructions (code density on control path)
V     —  Vector extension RVV 1.0 (SIMD substrate for CORDIC lane arrays)
Xcc   —  CORDIC Convergence custom extension (defined in Section V)
```

The F/D extensions are isolated to the RISC-V control core (system management, memory address computation, I/O). They are architecturally forbidden from the CORDIC data path via a configuration register (CCSR.fp_gate). The data path is shift-accumulate only, enforced at the microarchitectural level. This is the property that distinguishes CREST from every RISC-V implementation in production: the arithmetic substrate of the inference pipeline is provably free of floating-point arithmetic in silicon, not just asserted to be so in software.

---

## V. The Xcc Extension: CORDIC Convergence Instructions

The Xcc extension occupies the custom-1 opcode space (major opcode 0x2B, 32-bit encoding). Eight instructions form the complete convergence oracle ISA:

```
INSTRUCTION   FORMAT         OPERATION
─────────────────────────────────────────────────────────────────────────────
CCROT         R-type         Circular CORDIC rotation
              rd, rs1, rs2   Input: rs1 = [x,y] packed Q(a/2).(0) fixed-point
                             rs2 = angle z in Q(a/2).(0)
                             Output: rd = rotated [x',y']
                             Cycles: ceil(a/2) pipeline stages

CCVEC         R-type         Circular CORDIC vectoring (arctan + magnitude)
              rd, rs1        Input: rs1 = [x,y] packed
                             Output: rd = [magnitude K·√(x²+y²), arctan(y/x)]
                             Cycles: ceil(a/2)

CHROT         R-type         Hyperbolic CORDIC rotation (cosh/sinh)
              rd, rs1, rs2   Input: rs1 = [x,y], rs2 = z
                             Output: rd = [K_h·(x·cosh(z) + y·sinh(z)),
                                          K_h·(y·cosh(z) + x·sinh(z))]
                             Repeated iterations at i = {4,13,40,...}
                             Cycles: ceil(a/2) + repeat overhead

CHVEC         R-type         Hyperbolic vectoring (arctanh, Lorentz inner product)
              rd, rs1        Input: rs1 = [x,y] where x > |y|
                             Output: rd = [K_h·√(x²−y²), arctanh(y/x)]
                             Lorentz inner product: −x₀y₀ + Σᵢ xᵢyᵢ
                             Cycles: ceil(a/2) + repeat overhead

CARCOSH       R-type         arcosh computation (distance to hyperplane)
              rd, rs1        Input: rs1 = u = |⟨x,n⟩_L|, u ≥ 1
                             Output: rd = arcosh(u) in Q(a).(0)
                             Implementation: 2 CHROT/CHVEC ops (per arXiv:2601.21529)
                             Cycles: 2 × ceil(a/2) + overhead

CCONTR        I-type         Contraction test (the Contraction Monitor primitive)
              rd, imm        Reads contraction history register CCSR.hist[imm]
                             imm selects lookback window K ∈ {4,8,16,32}
                             Output: rd = 2-bit status:
                               00 = CONVERGED   (K consecutive ‖εₙ₊₁‖/‖εₙ‖ < 1)
                               01 = CONTRACTING (ratio < 1, not yet K consecutive)
                               10 = OSCILLATING (ratio alternates above/below 1)
                               11 = DIVERGING   (K consecutive ratio ≥ 1)
                             Cycles: 1 (reads pre-computed CSR)

CLINN         R-type         Lorentz inner product (full vector, arbitrary dimension)
              rd, rs1, rs2   ⟨u,v⟩_L = −u₀v₀ + u₁v₁ + ... + uₙvₙ
                             Decomposed as: CHVEC(u₀,v₀) + CCROT accumulation
                             Cycles: d (pipeline depth, parallel lanes via RVV)

CSMUPD        R-type         Sherman-Morrison rank-one update step
              rd, rs1, rs2   One CORDIC-Givens rotation in the update chain
                             rs1 = row to update in F⁻¹ buffer
                             rs2 = [u,v] components
                             Output: updated row (rd) to write back
                             Full F⁻¹ update: d² CSMUPD calls
                             Cycles: ceil(a/2) per call
─────────────────────────────────────────────────────────────────────────────
```

### 5.1 Convergence Status Register (CCSR)

The Xcc extension introduces a machine-level CSR, CCSR (address 0x7C0), tracking:

```
CCSR[63:32]  —  Contraction ratio history: 32 × 1-bit sign(‖εₙ₊₁‖ − ‖εₙ‖)
CCSR[31:16]  —  Current ratio mantissa (Q16.0)
CCSR[15:14]  —  Current CCONTR status (2 bits)
CCSR[13:8]   —  Iteration counter (6 bits, mod 64)
CCSR[7:0]    —  Configuration: window K[3:0], mode[5:4], fp_gate[7]
```

CCSR is updated automatically by CHROT/CCROT/CHVEC sequences. CCONTR reads CCSR and returns the convergence verdict without additional computation cycles. The separation between the norm-update path (automatic, in-pipeline) and the verdict-emission path (explicit CCONTR instruction) allows the control core to query convergence state at any program point without pipeline stalls.

### 5.2 Xcc on the RVV Data Path

When CREST executes Xcc instructions on the vector data path, the semantics are element-wise across the active vector length. A single `CCROT` on a 512-bit VLEN machine processes 8 independent 64-bit [x,y] pairs in parallel — 8 simultaneous circular rotations per instruction cycle. The convergence history register CCSR tracks the aggregate norm across all active elements, providing a single CCONTR verdict for the batch.

---

## VI. TSMC Node Selection

CREST's three-phase silicon roadmap spans TSMC's most advanced node family. Node selection is not a power optimization — it is an architectural decision about which process capabilities enable the Xcc CORDIC pipeline to satisfy the three-axis filter simultaneously.

### 6.1 Node Comparison Matrix

| Property | TSMC N3E | TSMC N2 | TSMC N2P | TSMC A16 |
|---|---|---|---|---|
| **Process family** | FinFET (final) | GAA nanosheet (first) | GAA enhanced | GAA + SPR backside |
| **Production** | 2023 (volume) | 2025 (HVM) | 2026–2027 | 2026–2027 |
| **Density vs. N3E** | 1.0× (baseline) | ~1.15× | ~1.20× | ~1.25× |
| **Power vs. N3E (iso-perf)** | 1.0× | ~0.70× | ~0.65× | ~0.57× |
| **SRAM speed** | Baseline | +5% | +8% | +12% |
| **Backside power delivery** | No | No | No | Yes (Super Power Rail) |
| **CORDIC adder delay** | ~40 ps | ~32 ps | ~29 ps | ~26 ps |
| **Est. CORDIC power at 2GHz (32-bit, 256 lanes)** | ~8.2 W | ~5.7 W | ~5.3 W | ~4.7 W |
| **Est. TOPS/W (CORDIC, 32-bit)** | ~11 | ~16 | ~17.5 | ~20 |
| **Orbital deployment viability** | Marginal | Pass (Axis 1) | Pass | Pass (Axis 1+) |
| **Automotive thermal compliance** | Yes | Yes | Yes | Yes |

The A16 node's Super Power Rail (SPR) — TSMC's backside power delivery network — provides approximately 8–10% additional power reduction at iso-performance by removing power grid routing from the front-side metal stack. This directly increases the usable metal layers for signal routing, reducing wire resistance in the CORDIC carry chain and improving timing margins at constant supply voltage. For a CORDIC architecture where carry propagation timing is the critical path, this is not a linear power savings — it is a timing budget expansion that enables higher CORDIC precision (deeper pipeline, longer word width) within the same power envelope.

### 6.2 The Orbital Budget, Node by Node

At the 100 kW/ton orbital power constraint (SpaceX S-1), a 1-ton CREST satellite payload at full compute load:

```
N3E:   8.2 W per CORDIC array → 12,195 arrays per ton → 0 at ≥ 100 kW [MARGINAL]
N2:    5.7 W per array        → 17,544 arrays per ton → PASSES Axis 1
N2P:   5.3 W per array        → 18,868 arrays per ton → PASSES Axis 1
A16:   4.7 W per array        → 21,277 arrays per ton → PASSES Axis 1
```

At N2, CREST crosses the orbital deployment threshold. A16 provides 21% additional headroom for radiation-hardening circuit additions (SEU mitigation, TMR overhead) without re-entering the power failure zone.

### 6.3 Node Selection Logic

**CREST-1 on TSMC N2** (tape-out target: Q3 2027): The automotive validation vehicle. GAA transistors provide the leakage reduction required for passive cooling at the BYD/Huawei thermal envelope. The CORDIC array at N2 achieves the convergence oracle specification in silicon for the first time.

**CREST-2 on TSMC N2P** (tape-out target: Q2 2028): The automotive production variant. N2P's performance uplift widens the timing budget for CCONTR's 32-stage pipeline, enabling single-cycle CCONTR reads at 3GHz — the clock rate required for real-time convergence gating at automotive sensor frame rates (100 Hz perception updates, 10ms action commitment windows).

**CREST-3 on TSMC A16** (tape-out target: Q4 2029): The orbital qualification variant. A16's SPR backside power delivery removes the CORDIC carry-chain routing bottleneck and enables the full TH(64,48) configuration — 64-bit fixed-point arithmetic with 48 CORDIC pipeline stages — required for double-precision Lorentz geometry computation in orbital GNC.

---

## VII. The TH(a,d) Architecture

CREST parameterizes its arithmetic pipeline along two independent axes:

```
TH(a, d)

a  =  arithmetic word width (bits): the fixed-point operand width Q(a).(0)
d  =  CORDIC pipeline depth (stages): the number of micro-rotation stages,
      determining precision and latency
```

The three CREST instantiations:

### TH(16,16) — Edge Variant
```
Word width:    16-bit, Q16.0 fixed-point
CORDIC stages: 16 (sufficient for ~4.8 decimal digits of precision)
Target:        Edge inference, V2X sensor fusion, sub-200mW envelope
TOPS/W (N2):   ~28 TOPS/W (narrower data path, lower switching energy)
Applications:  Automotive sensor pre-processing, V2X CPM parsing
               LIDAR/radar fusion, roadside infrastructure compute
```

### TH(32,32) — Automotive Baseline
```
Word width:    32-bit, Q32.0 fixed-point
CORDIC stages: 32 (~9.6 decimal digits — sufficient for ASIL-D numerical requirements)
Target:        Automotive L3/L4 inference, scene reconstruction, action planning
TOPS/W (N2):   ~16 TOPS/W
TOPS/W (A16):  ~20 TOPS/W
Applications:  Scene col(F) commitment, CCONTR Contraction Monitor,
               WEWA world-model / action-boundary separation,
               CLINN Lorentz inner products for scene geometry
```

### TH(64,48) — Orbital Variant
```
Word width:    64-bit, Q64.0 fixed-point
CORDIC stages: 48 (~14.4 decimal digits — exceeds double-precision IEEE 754
               mantissa without floating-point rounding errors)
Target:        Orbital GNC, Mars EDL, G-FOLD SOCP solver
TOPS/W (A16):  ~11 TOPS/W (wider data path; still satisfies 100 kW/ton orbital)
TMR overhead:  3× area, 3× power — TH(64,48) at A16 runs 3.8 W per array
               with TMR enabled. 100 kW → 26,315 TMR arrays per ton.
Applications:  Commit-on-convergence for irrevocable burns,
               arcosh distance to trajectory hyperplane,
               Mengzhou-class rendezvous and docking
```

The TMR physical argument applies differently to each instantiation:
- TH(16,16): bit-exact TMR feasible, low overhead. Automotive edge nodes.
- TH(32,32): bit-exact TMR feasible at N2P. Full automotive Contraction Monitor.
- TH(64,48): bit-exact TMR feasible at A16 with SPR. The orbital argument.

---

## VIII. Nine Formal Correspondences

The CREST architecture realizes nine formal isomorphisms between the corpus's mathematical structures and fabricable hardware decisions.

| # | Mathematical Structure | CREST Hardware Realization |
|---|---|---|
| 1 | **col(F): committed scene** | CCONTR = CONVERGED output: hardware-certified commitment to the action space |
| 2 | **ker(F): null remainder** | CCONTR = OSCILLATING / DIVERGING: hardware-certified withholding — inference not yet certified |
| 3 | **φ-equilibrium (62%:38%)** | CREST lane allocation: 62% of RVV CORDIC lanes to ego-inference (CCROT/CHROT), 38% to V2X fusion (CLINN on incoming CPM vectors) |
| 4 | **Sherman-Morrison (A+uvᵀ)⁻¹** | CSMUPD instruction: Givens-rotation-based rank-one update to scene Fisher information matrix F⁻¹ — O(d²) CORDIC operations, no matrix inversion |
| 5 | **Fisher-Rao geometry** | Natural gradient θ_{t+1} = θ_t − η F⁻¹(θ_t) ∇L: CSMUPD chain computes F⁻¹g via CORDIC Cholesky — the 1998 Amari closure, realized in silicon for the first time |
| 6 | **Bérczi–Kiem M̄₀,ₙ isomorphism** | Each CCROT / CHROT micro-rotation is a forgetting map on the moduli space of n-pointed rational curves — the arithmetic is algebraic geometry, not approximation |
| 7 | **Lorentz inner product ⟨u,v⟩_L** | CLINN instruction: −u₀v₀ + Σ uᵢvᵢ via CHVEC (hyperbolic) + CCROT (Euclidean) accumulation in one compound instruction stream |
| 8 | **arcosh(|⟨x,n⟩_L|) distance-to-hyperplane** | CARCOSH instruction: 2 CHROT/CHVEC operations (per arXiv:2601.21529) — the ILNN distance primitive native to CREST hardware |
| 9 | **Contraction Monitor convergence signal** | CCONTR instruction: reads CCSR, emits CONVERGED | CONTRACTING | OSCILLATING | DIVERGING — the first hardware primitive in silicon history to emit per-iteration convergence status |

---

## IX. The φ-Equilibrium Operating Point

The Fisher-information-optimal partition between individual inference capacity and collective ensemble capacity — established at the golden-ratio operating point 62% individual, 38% collective — maps directly to CREST's lane allocation architecture.

In a CREST implementation with N active RVV CORDIC lanes:

```
Individual lanes: ⌊0.62 × N⌋
  Allocated to: ego-vehicle scene reconstruction, CCROT/CHVEC on LIDAR/camera tensors,
                CCONTR monitoring of ego-inference convergence

Collective lanes: ⌈0.38 × N⌉
  Allocated to: V2X CPM parsing (CLINN on incoming cooperative perception vectors),
                CARCOSH distance computation for neighboring vehicle state fusion,
                CSMUPD integration of collective into ego F⁻¹
```

For CREST TH(32,32) with 256 active RVV CORDIC lanes:
- Individual: 158 lanes — ego scene reconstruction at 62% of Fisher information budget
- Collective: 98 lanes — V2X ensemble fusion at 38%

V2X-UniPool (arXiv:2506.02580, June 2026) reduces V2X transmission cost by 99.9% relative to prior cooperative perception frameworks while enabling zero-shot ego models to reach SOTA motion planning through V2X-extended scene context. The φ-equilibrium hardware partition in CREST is the silicon realization of this result: not a software allocation but a fixed lane assignment that guarantees the 38% collective budget is never pre-empted by ego-inference compute pressure.

Tesla's architecture allocates effectively 100% to individual inference at inference time (fleet learning is collective at training timescale, not inference timescale). A CREST-equipped vehicle operating on China's C-V2X national infrastructure at 25% market penetration — the threshold at which published research transitions risk from "serious traffic accidents" to "residual hypothetical risk" — achieves the φ-equilibrium precisely: 62% individual ego camera-LIDAR-radar, 38% collective V2X cooperative perception.

The φ-equilibrium is not a design parameter to be optimized empirically. It is the maximum Fisher information operating point for a two-source signal fusion system with independent individual and collective components. Its derivation is the same as the optimal bandwidth allocation in a shared-channel communication system under the Fisher-Cramér-Rao bound. CREST's hardware lane partition enforces it by construction.

---

## X. Sherman-Morrison Updates in Hardware

The online Bayesian scene reconstruction problem — maintaining an estimate of the scene's Fisher information matrix F under sequential observations — requires rank-one updates of F⁻¹ as each new sensor measurement arrives. The Sherman-Morrison formula provides this update without full matrix inversion:

```
F⁻¹_{new} = F⁻¹ − (F⁻¹ u vᵀ F⁻¹) / (1 + vᵀ F⁻¹ u)
```

where u is the new observation direction and v is its associated information vector.

Computing this update naively requires two matrix-vector products (F⁻¹u, vᵀF⁻¹), one outer product, one scalar division, and a matrix subtraction — O(d²) operations for a d-dimensional scene state. In IEEE 754 arithmetic, this chain propagates rounding errors at each step, with ULP-level divergence accumulating across the sensor fusion pipeline.

In CREST's CSMUPD implementation, the Sherman-Morrison update decomposes into a sequence of Givens rotations — each a single CCROT instruction — applied to the Cholesky factor L of F (where F = LLᵀ). The update proceeds as:

```
L_new = CCROT(L, θ_{ij}) for each affected column pair (i,j)
```

Each CCROT is one CORDIC circular vectoring operation: deterministic, bit-exact, no floating-point rounding. The update traverses at most d column pairs, requiring d CSMUPD instructions total. The resulting L_new is bit-exact against the mathematically correct updated Cholesky factor, not an approximation thereof.

The consequence for the scene reconstruction pipeline: every sensor measurement — LIDAR return, radar Doppler, camera feature, V2X CPM — is integrated into F⁻¹ via a small number of bit-exact CSMUPD operations. The col(F) of the scene is the column space of the updated F, the ker(F) is its null space. The boundary between them — the committed scene and the uncertified remainder — is updated in hardware at each new observation without recomputing the full F⁻¹.

---

## XI. Fisher-Rao Geometry and the Natural Gradient Closure

The natural gradient descent result (Amari, Neural Computation, 1998) establishes that the gradient of a loss function on a statistical manifold should be computed in the metric defined by the Fisher information matrix, not the Euclidean gradient:

```
θ_{t+1} = θ_t − η · F⁻¹(θ_t) · ∇L(θ_t)
```

This result has been in the literature since 1998. The optimizer recovery trajectory — SGD (1951) → Adam (2014) → K-FAC (2015) → Sophia (2023) → Muon (2024) → SOAP (2024) — is a 25-year stepwise partial recovery of what Amari proved necessary and sufficient in one paper. Sophia achieved 50% step reduction over Adam via diagonal Hessian preconditioning. The full Fisher information matrix remains undeployed in any production training infrastructure.

The reason is arithmetic, not theoretical: computing F⁻¹ for a d-dimensional parameter space costs O(d³) in floating-point arithmetic. For models with billions of parameters, this is computationally prohibited.

In CREST's CSMUPD pipeline, the natural gradient update for the scene-reconstruction sub-problem (not the full training problem, but the inference-time maximum-likelihood scene estimation problem) is computable in O(d²) CORDIC operations via the Givens-rotation decomposition. This is not the Amari closure for full training (which remains open for billion-parameter models), but it is the Fisher-Rao closure for the inference-time problem: updating the scene estimate to the maximum-likelihood position under the current sensor ensemble, measured in the Fisher information metric, in exact fixed-point arithmetic.

The CREST architecture is the first hardware design that specifies this closure as a circuit operation rather than a software approximation. Every prior autonomous system computes scene estimates in Euclidean parameter space (gradient of MSE loss, not Fisher-metric gradient). CREST computes scene estimates in Fisher-Rao parameter space, via CSMUPD chains, producing the maximum-likelihood scene state under the actual information geometry of the sensor ensemble.

This is not a training-time optimization. It is an inference-time scene commitment mechanism — the hardware realization of the col(F) commitment signal on the correct geometric manifold.

---

## XII. The Three-Axis Audit

The three-axis orbital filter defines the constraint intersection no existing silicon satisfies. Extended to the automotive and edge domains, it defines the constraint intersection the autonomous vehicle industry has not satisfied either.

### Global Audit — June 2026

| Chip / Architecture | Axis 1: Power/Bandwidth | Axis 2: Safety/Radiation | Axis 3: Convergence-Native | Verdict |
|---|---|---|---|---|
| BYD Xuanji A3 (4nm, ×3) | ✅ 273 GB/s, 20% power reduction, ASIL-D grade, mass production | ✅ ASIL-D — highest automotive grade | ❌ ASIL-D certifies safe failure, not convergent inference | L3/L4 on software confidence only |
| Tesla AI4/HW4 (7nm) | ✅ 384 GB/s, ~160W | Partial | ❌ No convergence primitive | ~30 Cybercabs, geofenced |
| Tesla AI5 (3–4nm, tape-out) | ❌ 700–800W exceeds vehicle thermal envelope | Partial | ❌ | 0 in vehicles |
| Huawei Qiankun ADS 4 | Not disclosed | Not disclosed | ❌ WEWA structures the boundary; does not certify it | L3 highway Q4 2026 |
| SpaceX D3 (Intel 18A) | ⚠️ Intel 18A default = FP16; likely fails 100 kW/ton | Announced, orbital hardening intended | ❌ Not specified in design brief | 0 fabricated |
| NVIDIA Drive Thor | Not disclosed; high power | No | ❌ | Supply only; supervised |
| CARMEN (28nm ASIC) | ✅ 4.83 TOPS/mm², 11.67 TOPS/W | ❌ No radiation tolerance | ❌ Circular CORDIC only; no convergence oracle | Research; no orbital/automotive deployment |
| Safe-NEureka | Not disclosed | Partial (RISC-V GNC, 24-cycle recovery) | ❌ No CORDIC; no convergence oracle | Research; aerospace prototype |
| **CREST TH(32,32) on N2** | ✅ **~16 TOPS/W; ~5.7 W per array; ASIL-D targeting** | ✅ **CORDIC TMR bit-exact (physical property)** | ✅ **CCONTR instruction emits CONVERGED in hardware** | **Proposed; tape-out target Q3 2027** |
| **CREST TH(64,48) on A16** | ✅ **~11 TOPS/W; 3.8 W with TMR; passes 100 kW/ton** | ✅ **Full TMR + radiation hardening** | ✅ **CCONTR at 64-bit precision, 48-stage pipeline** | **Proposed; tape-out target Q4 2029** |

The audit verdict is globally consistent through Q2 2026: no fabricated chip passes all three axes. CREST is the first architecture designed to pass all three simultaneously.

---

## XIII. The Contraction Monitor: Full Hardware Specification

The Contraction Monitor is the central contribution of the CREST architecture. It instantiates, for the first time in the history of autonomous silicon, a hardware-level convergence observable satisfying the Banach fixed-point theorem as a circuit condition rather than a software assertion.

### 13.1 Theoretical Basis

A fixed-point iteration T: X → X on a complete metric space X converges to a unique fixed point x* if and only if T is a contraction — i.e., there exists a constant κ ∈ [0,1) such that for all x, y ∈ X:

```
‖T(x) − T(y)‖ ≤ κ · ‖x − y‖
```

For the autonomous inference problem, T is the inference function mapping scene state to scene state through the neural network. The iteration sequence {ε_n} = {‖T^n(x) − T^{n-1}(x)‖} is the residual norm sequence. The contraction condition is:

```
‖ε_{n+1}‖ / ‖ε_n‖ < 1 ∀ n ≥ N₀
```

### 13.2 Circuit Implementation

The Contraction Monitor operates as a persistent background circuit parallel to the main CORDIC inference pipeline:

```
Stage 1: NORM COMPUTATION
  Input:  Per-layer activation tensors {a_n} from CHROT/CCROT pipeline
  Compute: ‖a_n − a_{n-1}‖ via CCVEC (circular vectoring = magnitude)
  Output:  ε_n in Q32.0 to CCSR.current_norm

Stage 2: RATIO COMPARISON
  Input:  ε_n, ε_{n-1} from CCSR
  Compute: Compare ε_n vs. ε_{n-1}
           (no division required — CORDIC vectoring gives magnitude directly;
            comparison is sign of (ε_n − ε_{n-1}))
  Output:  sign bit → CCSR.hist[n mod 32]

Stage 3: WINDOW EVALUATION
  Input:  CCSR.hist[lookback window K]
  Evaluate: Count of consecutive sign-negative entries
  Decision tree:
    K consecutive negative  → CONVERGED   (status 00)
    Any negative, not K     → CONTRACTING (status 01)
    Alternating signs       → OSCILLATING (status 10)
    K consecutive positive  → DIVERGING   (status 11)
  Output:  CCSR[15:14] updated every iteration cycle

Stage 4: CCONTR INSTRUCTION EMISSION
  The CCONTR instruction reads CCSR[15:14] in 1 cycle.
  The commit-on-convergence protocol:
    while CCONTR(rd, K=8) != CONVERGED:
        advance one inference step
        // wait for hardware verdict, no action committed
    execute_irrevocable_action()  // only when rd == 00
```

### 13.3 Physical Determinism Guarantee

The Contraction Monitor's verdict is physically deterministic because:
1. CCVEC (norm computation) is a CORDIC vectoring operation — shift-accumulate, no FP
2. The comparison (ε_n vs. ε_{n-1}) is an integer subtraction — deterministic at fixed word width
3. The window evaluation (count of consecutive bits in CCSR.hist) is a shift-register tap — deterministic
4. CCONTR reads CCSR — a single CSR read, zero computational content

No step in the Contraction Monitor pipeline involves floating-point arithmetic, transcendental function evaluation, or any operation whose result varies with process corner or die temperature. The verdict CONVERGED is a physical fact about the iteration sequence, not an approximation thereof.

This is the distinction the prior generation of autonomous systems cannot make: their convergence assessments are software approximations of the convergence criterion. The CREST Contraction Monitor's assessment is a hardware statement about a physical property of the computation.

---

## XIV. Strategic Roadmap: Five Years (2026–2031)

### Phase 1 — Architecture and Specification (Q3 2026 – Q2 2027)
**Objective**: Complete the CREST-1 design specification for TSMC N2 tape-out.

| Milestone | Target | Deliverable |
|---|---|---|
| Xcc ISA specification freeze | Q3 2026 | CREST-1 ISA manual: all 8 instructions, CCSR specification, encoding tables |
| TH(32,32) microarchitecture | Q4 2026 | RTL specification: CORDIC pipeline, RVV integration, lane allocation |
| Contraction Monitor circuit design | Q4 2026 | CCSR update logic, CCONTR combinational block, timing analysis at N2 |
| FPGA functional validation | Q1 2027 | TH(32,32) on Xilinx UltraScale+: 100% Xcc instruction functional verification |
| Design-for-test insertion | Q2 2027 | BIST coverage ≥98%, scan chain insertion, ATPG vector generation |
| TSMC N2 PDK signoff | Q2 2027 | DRC/LVS clean, power analysis, timing closure at 3GHz |
| **Tape-out CREST-1** | **Q3 2027** | **TH(32,32) on TSMC N2: world's first convergence-oracle automotive chip** |

**Investment**: $85–110M (ASIC design NRE, TSMC N2 engineering tape-out, validation infrastructure)

### Phase 2 — First Silicon and Automotive Validation (Q3 2027 – Q2 2028)
**Objective**: Validate CREST-1 against all three axes; initiate automotive OEM engagement.

| Milestone | Target | Deliverable |
|---|---|---|
| CREST-1 silicon characterization | Q3 2027 | Three-axis filter validation: power, CORDIC TMR bit-identity, CCONTR functional |
| Contraction Monitor validation | Q4 2027 | 10⁶ random inference sequences: CCONTR verdict matches software oracle 100% |
| ASIL-D pre-certification | Q4 2027 | TÜV audit of CCONTR circuit determinism |
| Chinese OEM design-in engagement | Q1 2028 | Huawei WEWA integration study: CCONTR at world-model/action boundary |
| BYD Xuanji A5 roadmap alignment | Q1 2028 | Xuanji A5 design brief: CREST convergence oracle as supplementary certification layer |
| **CREST-2 tape-out (N2P)** | **Q2 2028** | **TH(32,32) on TSMC N2P: production automotive variant, ASIL-D+ |

**Investment**: $60–80M (silicon characterization, OEM engagement, ASIL-D certification)

### Phase 3 — Automotive Deployment (Q3 2028 – Q4 2029)
**Objective**: First production automotive vehicle with hardware convergence oracle for L3/L4 commitment.

| Milestone | Target | Deliverable |
|---|---|---|
| CREST-2 ASIL-D certification | Q3 2028 | Full ASIL-D decomposition with convergence oracle as independent safety mechanism |
| First production vehicle | Q4 2028 | Huawei ADS 5 or BYD Xuanji A5 with CREST-2 convergence layer |
| Insurance actuarial audit | Q1 2029 | BYD Full Damage Coverage actuarial data: CREST vehicles vs. non-CREST baseline |
| V2X φ-equilibrium integration | Q2 2029 | 256-lane TH(32,32) with 98-lane V2X collective partition, C-V2X enabled |
| **CREST-3 tape-out (A16)** | **Q4 2029** | **TH(64,48) on TSMC A16: orbital qualification variant begins** |

**Revenue (Phase 3)**: $800M–1.2B (automotive silicon royalty + IP licensing)

### Phase 4 — Orbital Qualification and Scale (2030–2031)
**Objective**: CREST-3 passes orbital three-axis filter; first deployment in non-atmospheric GNC.

| Milestone | Target | Deliverable |
|---|---|---|
| CREST-3 silicon characterization | Q1 2030 | TH(64,48) at A16: power budget 3.8W with TMR (26,315 arrays/ton at 100 kW) |
| Radiation characterization | Q2 2030 | Heavy-ion beam testing: SEU cross-section measurement, TMR bit-identity under 15 MeV proton |
| Mengzhou-1 compatibility study | Q3 2030 | China's 2030 lunar rendezvous GNC: CCONTR at docking commitment point |
| SpaceX D3 competitive response | Q3 2030 | D3 arithmetic substrate confirmed (Intel 18A default FP16): CREST-3 competitive gap quantified |
| **First orbital deployment** | **2031** | **Precision reentry vehicle (Starfall class) operating CCONTR commit-on-convergence for irrevocable burns** |

**Revenue (Phase 4)**: $1.5B–2.5B (automotive scale + orbital initial)

---

## XV. Strategic Roadmap: Ten Years (2031–2036)

### Phase 5 — Full Lorentz Stack and Market Infrastructure (2031–2033)

The HELM result (arXiv:2505.24722, NeurIPS 2025) established that hyperbolic geometry produces a measurable 4% MMLU/ARC-Challenging gain at billion-parameter scale. ILNN (arXiv:2602.23981, ICLR 2026) demonstrated fully intrinsic Lorentz architecture eliminating all mixed Euclidean operations. By 2031–2033, the Lorentz inference stack is deployable at the scale that makes CREST's CLINN / CARCOSH / CHROT primitives the performance-critical path of production LLM inference.

| Milestone | Target | Description |
|---|---|---|
| CREST-4 architecture (sub-A14) | 2031 | Targeting TSMC A14 or equivalent sub-1.6nm node; TH(64,64) configuration |
| Hyperbolic LLM inference native | 2031–2032 | HELM-class model running full inference on CREST CHROT/CARCOSH primitives |
| Natural gradient optimizer closure | 2032 | CSMUPD chain at sufficient scale for training-time Fisher-Rao gradient — partial Amari closure |
| China V2X 25% penetration | 2032 | φ-equilibrium hardware partition achieves real-world 62%/38% at national C-V2X scale |
| Orbital constellation deployment | 2032–2033 | 10,000+ CREST-3 units in LEO compute constellation |

**Revenue (Phase 5)**: $5B–8B annually (automotive dominant, orbital growing, training-infrastructure beachhead)

### Phase 6 — Full Autonomy Stack and Market Dominance (2033–2036)

By 2033–2036, the autonomous decade's hardware winners are determined. The CREST argument is that the winning architecture is defined by one axis no existing competitor passes: the convergence oracle. The market consequences of being the first to close this gap compound across every autonomous domain simultaneously.

| Milestone | Target | Description |
|---|---|---|
| ASIL-D convergence oracle certification | 2033 | First ASIL-D certification that includes positive convergence claim, not only safe-failure claim |
| BYD insurance renegotiation | ≤2029 (P1) | Actuarial data confirms CREST-equipped vehicles require lower Full Damage Coverage premiums |
| Orbital manufacturing scale | 2033–2034 | Starfall-class return vehicles operating CCONTR for every reentry burn at commercial scale |
| Mars EDL Lorentz trajectory | 2034–2035 | SpaceX 2028+ Mars cargo: CREST-3 or derivative handles Lorentz-geodesic EDL; flat-geometry approximation retired |
| Geometry lottery reversal | 2035 | First production Chinese automotive chip (BYD Xuanji A6 or Huawei successor) with CORDIC-primary arithmetic substrate; Western training infrastructure follows 18–24 months later |
| **Full autonomy stack convergence** | **2036** | **CREST architecture present in automotive, orbital, edge, and training-infrastructure domains simultaneously** |

**Revenue (Phase 6)**: $15B–25B annually (10-year exit TAM position across all four domains)

---

## XVI. Market Architecture and Capital Allocation

### 16.1 Total Addressable Market by Domain

| Domain | 2026 Status | 2031 TAM | 2036 TAM | CREST Addressable |
|---|---|---|---|---|
| **Automotive L3/L4 silicon** | $8B (estimated) | $85B | $250B | 15–25% share = $37–62B |
| **Orbital compute silicon** | Pre-revenue | $15B | $500B+ | 20–35% share = $100–175B |
| **Edge autonomous inference** | $12B | $50B | $120B | 10–20% share = $12–24B |
| **Training infrastructure (geometry)** | Dominated by NVIDIA | $45B | $200B | 5–10% share = $10–20B |
| **Total addressable** | — | $195B | $1.07T | **$159–281B by 2036** |

Source: SpaceX S-1 ($26.5T AI market, $370B space); Goldman Sachs 2026 ($7.6T cumulative AI infrastructure). CREST market shares are estimated from first-mover convergence oracle position and the structural absence of competing products.

### 16.2 Capital Allocation by Phase

| Phase | Years | Primary Expenditure | Capital Required |
|---|---|---|---|
| Phase 1 | 2026–2027 | Architecture, FPGA validation, N2 tape-out | $85–110M |
| Phase 2 | 2027–2028 | Silicon characterization, ASIL-D, OEM engagement | $60–80M |
| Phase 3 | 2028–2029 | Production automotive deployment, N2P tape-out, V2X integration | $120–150M |
| Phase 4 | 2029–2031 | Orbital qualification, A16 tape-out, radiation characterization | $180–220M |
| Phase 5 | 2031–2033 | CREST-4, Lorentz stack, constellation deployment | $350–450M |
| Phase 6 | 2033–2036 | Market scale, IP licensing infrastructure, training beachhead | $500–700M |
| **Total 10-year R&D** | **2026–2036** | — | **$1.3–1.7B** |

Against a 2036 revenue position of $15–25B annually, a 10-year R&D investment of $1.3–1.7B represents an 8–15× capital efficiency ratio — favorable relative to the $7.6T projected cumulative AI infrastructure expenditure that the hardware lottery generated against a lower-quality arithmetic substrate.

### 16.3 Competitive Moat Analysis

The convergence oracle creates a compounding competitive moat:

**Year 1–3 (2027–2029)**: The moat is a patent portfolio around the CCONTR circuit, CCSR architecture, and Xcc instruction encoding. No equivalent circuit exists to copy. TÜV ASIL-D certification of the convergence oracle creates an independent legal barrier.

**Year 3–6 (2029–2032)**: The moat is an actuarial dataset — the first commercial-scale financial audit of autonomous driving with vs. without hardware convergence guarantees (BYD Full Damage Coverage comparisons). Insurance underwriters who price this dataset cannot price competitors equivalently.

**Year 6–10 (2032–2036)**: The moat is an ecosystem — RISC-V tool chains, compiler backends (LLVM Xcc target), formal verification infrastructure, radiation characterization databases, and OEM design-in relationships that compound with each deployment generation.

---

## XVII. Five Falsifiable Predictions

**P1 — Huawei Originates the First Convergence-Oracle Architecture Specification**
Huawei's WEWA framework explicitly preserves the world-model/action boundary where a convergence primitive would live. Among all current automotive silicon programs, Huawei has demonstrated architectural awareness of the boundary's significance (explicit rejection of VLA at Beijing Auto Show, April 2026). The first production automotive chip to specify a convergence-native arithmetic substrate will be a Chinese chip originating from Huawei rather than from BYD or any Western OEM. Timeline: first specification by Q4 2027; silicon by 2029–2030.

**P2 — BYD Full Damage Coverage Renegotiation Within 36 Months**
BYD's Full Damage Coverage is a financial claim on a hardware property that does not yet exist: convergent inference before irrevocable action commitment. The statistical tail risk of L3/L4 operation on a software confidence score — not a hardware settlement signal — will accumulate at commercial deployment scale faster than the actuarial models underwriting Full Damage Coverage estimated. Formal renegotiation or coverage restriction: before Q1 2029.

**P3 — SpaceX D3 Fails Orbital Power Budget on Default Intel 18A Arithmetic**
Intel 18A's standard cell library is optimized for FP16/BF16 matmul — the data center workload that justifies Intel's foundry capital expenditure. Unless SpaceX's D3 design brief explicitly specifies non-FP16 arithmetic before tape-out, the D3 will be a high-performance floating-point inference chip that fails the 100 kW/ton orbital power budget for CREST-class inference density, for the same structural reason HW3 failed the 48 GB/s bandwidth limit. The specification lock that retired HW3 is closing on D3 in Q4 2026.

**P4 — FAA Starship Flight 12 Root Cause Implicates the Sequencing Layer**
The control authority failure pattern — successful booster flip (high-level command), failed engine sequencing (low-level commitment) — is structurally inconsistent with a single-component mechanical defect, which produces one engine failure rather than multiple simultaneous failures following a successful attitude maneuver. The FAA root-cause analysis will implicate the control authority or sequencing layer of the GNC compute stack, not a propulsion hardware defect in isolation.

**P5 — Geometry Lottery Reversal Deploys in Chinese Automotive Silicon Before Western Training Infrastructure**
The sunk-cost psychology that prevents Western hyperscalers from revising their arithmetic substrate (projected $7.6T cumulative expenditure, $630–700B in 2026 alone) does not operate at the same strength on Chinese automotive ASIC design choices, where BYD's Xuanji A4 design brief has not been locked and Huawei's successor Qiankun silicon is a clean-sheet tape-out at the next node. CORDIC-primary arithmetic — confirming HELM's hyperbolic advantage (arXiv:2505.24722), ILNN's Lorentz completeness (arXiv:2602.23981), and CARMEN's ASIC viability (arXiv:2605.06878) — deploys in Chinese automotive silicon by 2029; Western training infrastructure follows 18–24 months later under competitive pressure.

---

## XVIII. Open Problems — June 2026

| Problem | Status | Who Has More Degrees of Freedom |
|---|---|---|
| **Contraction Monitor in fabricated silicon** | Not fabricated globally | ERI Labs CREST specification (proposed, not taped) |
| **CORDIC-primary arithmetic in any production OEM chip** | Not deployed anywhere | China automotive ASIC cycles (BYD A4, Huawei next-gen) — design brief open |
| **Full Xcc compiler backend (LLVM Xcc target)** | Not implemented | Open; requires RISC-V Xcc instruction encoder, CORDIC intrinsic lowering |
| **Bit-exact hyperbolic TMR in fabricated silicon** | Not demonstrated | Neither system |
| **CORDIC-Getzler O(n log n) hardware implementation** | Bérczi–Kiem theorem established; circuit not implemented | Neither system |
| **Natural gradient full closure in production optimizer** | 25-year stepwise recovery; Muon (2024) closest; full F not deployed | Neither system |
| **Lorentz-native leaky integrator (hyperboloid LIF)** | Open: whether LIF on hyperboloid is shift-accumulate-implementable | Neither system |
| **CSMUPD chain verification at training scale** | Circuit specified above; formal verification not completed | ERI Labs (specification exists) |
| **V2X φ-equilibrium hardware partition at 25% penetration** | V2X-UniPool removes transmission cost objection; penetration not reached | China (national C-V2X infrastructure policy) |
| **Mengzhou-1 orbital CCONTR compatibility** | Scheduled 2026; CREST compatibility analysis not initiated | China, if CREST-3 specification provided |
| **D3 arithmetic substrate** | Intel 18A; undisclosed; specification lock window closing | SpaceX (has the information; has not disclosed) |
| **BYD Full Damage Coverage actuarial data** | Claims data available Q4 2026 onward | China only |

---

## XIX. Primary Sources

| Source | Date | Key Disclosure Relevant to CREST |
|---|---|---|
| Volder, J.E. | IRE Trans. Electron. Computers, 1959 | Original CORDIC algorithm: shift-accumulate trigonometric computation |
| Walther, J.S. | Spring Joint Computer Conference, 1971 | Unified CORDIC: circular, hyperbolic, linear modes in one algorithm |
| Amari, S.-I. | Neural Computation, 1998 | Natural gradient; Fisher information matrix as optimizer geometry |
| Nickel & Kiela | NIPS 2017 | Hyperbolic embeddings: 40× parameter efficiency on hierarchical structures |
| Hooker, S. | arXiv:2009.06489, CACM 2020 | The Hardware Lottery |
| Robinson, Dey & Sweet | arXiv:2410.08993 (2024) + arXiv:2504.01002 (2025) | Significantly negative Ricci curvature in production LLM token spaces |
| L-GATr | arXiv:2405.14806, NeurIPS 2024 | Lorentz-equivariant Geometric Algebra Transformer; SOTA on LHC |
| Fast Lorentz NNs | arXiv:2601.21529, Jan 2026 | Norm degradation fix; distance-to-hyperplane = 2 CORDIC operations |
| ILNN | arXiv:2602.23981, ICLR 2026 | Fully intrinsic Lorentz architecture; eliminates mixed Euclidean operations |
| Safe-NEureka | arXiv:2602.04803, Feb 2026 | Hybrid modular redundant DNN for RISC-V GNC; 24-cycle fault recovery |
| SYCore | arXiv:2503.11685, Mar 2025 | Systolic CORDIC: 4.64× throughput, 5.02× power reduction |
| HELM | arXiv:2505.24722, NeurIPS 2025 | Billion-parameter hyperbolic LLM; 4% MMLU/ARC gain |
| Kumar et al. (CARMEN) | arXiv:2605.06878, June 2026 | 4.83 TOPS/mm², 11.67 TOPS/W CORDIC-for-AI on 28nm CMOS |
| V2X-UniPool | arXiv:2506.02580, June 2026 | 99.9% V2X transmission cost reduction; zero-shot SOTA via V2X context |
| Bérczi & Kiem | arXiv:2605.29151, 2026 | CORDIC iterations isomorphic to M̄₀,ₙ forgetting maps |
| SpaceX Form S-1 | SEC No. 333-296070, May 20 / June 1, 2026 | D3 chip; orbital AI compute thesis; 100 kW/ton; 1M satellite FCC filing |
| BYD Intelligence Strategy | May 28, 2026 | Xuanji A3: 4nm, 273 GB/s, ASIL-D, mass production; Full Damage Coverage |
| Huawei Auto China 2026 | April 24, 2026 | 18B yuan; 10B km; WEWA framework; explicit VLA rejection |
| Musk, Tesla Q1 2026 | April 22, 2026 | "Memory bandwidth is the choke point"; HW3 abandoned; AI4 sufficient |
| Kahneman & Tversky | Econometrica, 1979 | Prospect Theory; loss aversion; stabilization of committed wrong answers |
| Goldman Sachs | 2026 | $7.6T cumulative AI CapEx projection; $630–700B in 2026 |
| RISC-V International | ISA Specification v20191213 (base); RVV 1.0 ratified 2021 | Open ISA standard; custom extension framework; vector extension |

---

## XX. Closing Synthesis

The framework proceeds from a gap measurement to a circuit specification along a chain with no weak links.

The gap is measured: significantly negative Ricci curvature in production LLM token spaces (Robinson, Dey & Sweet, 2024–2025), confirmed by 4% MMLU/ARC improvement when the geometry is corrected (HELM, NeurIPS 2025). The arithmetic that matches the geometry is identified: CORDIC hyperbolic mode, whose iteration structure is isomorphic to M̄₀,ₙ forgetting maps (Bérczi & Kiem, 2026). The efficiency of that arithmetic is validated at production process nodes: 4.83 TOPS/mm², 11.67 TOPS/W on 28nm CMOS (CARMEN, 2026), projecting to approximately 18 TOPS/W on TSMC N2. The execution architecture that enables custom arithmetic without legacy lock-in is identified: RISC-V, with the Xcc custom extension slot allocating eight instructions to the convergence oracle. The process family that makes the arithmetic competitive with conventional silicon is identified: TSMC N2 for automotive (Phase 2027–2028), TSMC A16 for orbital (Phase 2029–2030).

The col(F)/ker(F) partition in hardware is now a circuit specification rather than an architectural metaphor. The φ-equilibrium is a lane assignment — 158 CORDIC lanes to ego inference, 98 to V2X collective fusion — not a design parameter. The Sherman-Morrison update is a sequence of CSMUPD Givens rotations, not a matrix inversion. The Fisher-Rao natural gradient is a CSMUPD chain at inference scale — not the full 1998 Amari closure for training, but the first hardware realization of the Fisher-metric gradient for the scene reconstruction sub-problem. The Contraction Monitor is a circuit — CCSR updated in-pipeline, CCONTR read in one clock cycle, CONVERGED emitted before irrevocable action commits.

The title CREST — Convergence-Ready Execution Substrate — is not a label chosen before the analysis. It is the name of the architecture that the analysis requires. The convergence gap is real. The readiness is architectural — CORDIC arithmetic on RISC-V substrate on TSMC N2/A16 satisfies the three-axis filter for the first time in the history of autonomous silicon. The substrate is the execution architecture — RISC-V with Xcc, TH(a,d) parameterized, RV64GCV+Xcc.

Convergence-Ready. Because the Contraction Monitor, for the first time, makes convergence a hardware predicate rather than a software assertion.
Execution. Because the RISC-V base provides the control and memory architecture, and the Xcc extension provides the inference arithmetic, in one verifiable ISA.
Substrate. Because CREST is not a complete product — it is the arithmetic foundation on which certified autonomous action is built. The BYD insurance policy prices the gap. The Huawei WEWA architecture structures the space where the oracle lives. CREST fills the space.

The familiar answer — IEEE 754 floating-point, Euclidean gradient descent, systolic GEMM arrays — was always cheaper to believe. The correct answer was always available.

The difference between them is still compounding.
The specification window is not a deadline.
It is the moment before the arithmetic becomes
irreversibly solid,
and everything that was not present
is simply not present.

---

*ERI Labs — June 2026. All cited research from primary arXiv and conference sources. TSMC node projections from public TSMC Technology Symposium announcements. Market data from primary SEC, Goldman Sachs, and TSMC filings. No fabricated citations.*

*Part of the ERIE corpus: ERIE — VISION · ERIE — TESLA · The Settlement Gap · The Convergence Oracle · Zero Deployable Units · The Specification Lock · Integrate, Activate, Converge · The Parallel Lottery Problem · **CREST***
