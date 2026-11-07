# Tameria — The First Beacon
## Game Design Document (GDD)

**Document type:** Game Design Document — *design of record*
**Version:** **v0.1** (Draft for Design Review)
**Date:** 2026-11-06
**Target platform:** PC-first isometric ARPG (Godot 4.7 / GDScript 2.0), console/controller-parity planned
**Status:** Pre-Production — Design Lock candidate

---

### Document Map (how this file relates to the others)

| Document | Role | Authority |
| :--- | :--- | :--- |
| `tameria_project_specifications.md` (v1) | Technical blueprint & data schemas | Raw source |
| `tameria_action_plan.md` (v1.3) | Audit, conflict register, roadmap, feasibility | Analysis |
| **This GDD** | **Consolidated design of record** | **Design intent** |

> **Convention used throughout.** Every rule is tagged **[Ratified]** (comes from the source spec or an explicit author ruling) or **[Proposed]** (a design recommendation awaiting sign-off). Cross-references to the audit use the action-plan IDs (`G-xx` gap, `B-xx` finding, `Q-xx` open question, `C-xx` conflict). No number is invented silently; all unlabeled values below are **[Ratified]**.

---

## 1. Vision Statement

**High Concept (one line):**
> A dark-fantasy isometric ARPG where you save paradise — and are permanently cast out of it for the taint you accumulated doing so.

**Elevator pitch.**
The world of Tameria is being consumed by a mutating spatial anomaly, the **Calamity**. Across a 7-Act campaign the player grows from survivor to savior, arming themselves with Precursor relics and cleansing corrupted land. In the finale they activate the **World Sieve**, purging the last sanctuary to perfect purity — and are violently **rejected** by it, because they carry the very taint they fought. Expelled to the stone wall of the **Outer Ward**, the player spends the endgame as an exiled warden, opening Calamity Rifts from *The Lonely Watch* to hold back the tide that will never let them home.

**The thesis.** The campaign's reward is a door closed forever. The game is about the cost of being the one who does what others cannot.

---

## 2. Design Pillars

Every feature decision is measured against these five pillars.

| # | Pillar | What it means in play | Rejects |
| :--- | :--- | :--- | :--- |
| **P1** | **Kill fast, loot faster** | Moment-to-moment combat is legible, punchy, and readable at 60+ FPS; loot decisions happen in seconds, not menus. | Long animation locks, menu-heavy loot handling |
| **P2** | **The taint you carry** | Corruption is both the environment's threat and the hero's cost. Mechanics that accumulate taint must be *felt*, not read. | Purely cosmetic corruption |
| **P3** | **Depth you can plan** | Four progression layers presented as one coherent budget, not four disconnected screens. | "Parallel tax" trees with no shared view |
| **P4** | **Earned exile** | The Rejection is a consequence of play, foreshadowed and chosen — never a cutscene that robs agency. | Scripted-only endings |
| **P5** | **Variance you can beat** | Double-variance loot is tamed with floors, pity, and a mandatory filter so a bad roll is a setback, not a wall. | Unfiltered drop soup |

---

## 3. Target Platform & Production Standards

| Standard | Target | Note |
| :--- | :--- | :--- |
| Frame rate | **60 FPS target**, CPU-bound AI budget | Isometric ARPG perf is dominated by AI count + VFX, not draw calls (G-15) |
| Input | Keyboard + mouse **and** full gamepad parity; touch considered for any mobile branch | Cross-input is a shipping requirement |
| Resolution | Aspect-ratio-consistent scaling; UI never obscures hazards or interaction points | Visual-hierarchy rule (P2) |
| Engine | Godot 4.7, GDScript 2.0, strict typing | Resource/JSON-driven content |
| Architecture | `SignalBus` decoupling; single `StatModifier` pipeline; data-driven content | See §13 |

---

## 4. Core Gameplay Loops

The design defines three nested loops. Only the outer loop exists in the source spec; the two inner loops are **[Proposed]** (F-01) and are the priority of the first vertical slice.

| Loop | Duration | Beats | Status |
| :--- | :--- | :--- | :--- |
| **Moment** | 2–8 s | Locate pack → engage → kill → filter pings → pick up → next pack | **[Proposed]** |
| **Session** | 20–40 min | Enter area/rift → clear → boss → extract loot → craft/respec → repeat | **[Proposed]**, partially implied by §6 |
| **Meta** | Season | Level → gear → refine build → push keystone tiers → ladder | **[Proposed]** |

**The signature moment-loop — "Calamity Cleansing" [Proposed] (F-01).**
Slain corrupted mobs drop **Calamity Motes** (ratified, §6.1). Motes visibly corrupt the ground. The player must balance **collecting** them (progress toward the Cleansing Meter) against **cleansing** them (mitigating the hazard they create). This turns the Cleansing Meter from a passive progress bar into a risk/reward skill expression, and is the game's core novelty — it must be validated first in prototyping.

---

## 5. Character System — 4-Layer Progression

**[Ratified]** The progression system comprises four layers. **[Proposed]** they should be surfaced in a unified *Character Plan* UI rather than four separate screens (F-04).

```text
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 1: GLOBAL PASSIVE TREE & VIGIL POWER                             │
│ • Levels 1–100: shared node web, 130 Max Points.                       │
│ • Levels 100+: infinite VIGIL POWER matrix (Offense/Def/Util/Scavenge).│
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
┌───────────────────────────────────▼────────────────────────────────────┐
│ LAYER 2: CLASS TALENT TREES                                            │
│ • Talent Points unlock Active Skills at depth thresholds.              │
│ • Dual-Class Mastery vs. Single-Class Mastery paths.                  │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
┌───────────────────────────────────▼────────────────────────────────────┘
│ LAYER 3: MASTERY TREE & FUSION SKILLS                                  │
│ • Mastery passives & FUSION SKILLS (2 actives → 1).                    │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
┌───────────────────────────────────▼────────────────────────────────────┐
│ LAYER 4: INDIVIDUAL SKILL TREES & GLYPH SOCKETS                        │
│ • Gameplay XP levels slotted skills to spend points on mini-trees.     │
│ • Socket GLYPHS (Chaining, Multishot, Echoing, Execution).             │
└────────────────────────────────────────────────────────────────────────┘
```

### 5.1 Layer 1 — Global Passive Tree & Vigil Power **[Ratified]**

- **Global Passive Points:** capped at **130** = `1 (Lv 1) + 99 (Lv 2–100) + 30 (Act side quests)`.
- **Distribution:** the full **Act × Level × Points map** is in **[§12.1.3](#1213-act--level--points-distribution-ratified)** (C-05 / B-13 resolved) — level bands **shrink as the campaign deepens** (`14/12/11/10/9/8/5`) and **quest points front-load** (`6/5/5/4/4/3/3`, all in-campaign).
- **Leveling:** soft cap at **Lv 100**; levels beyond 100 continue infinitely with exponentially scaling XP.
- **Vigil Power (post-100):** each level past 100 awards **Vigil Points**.
  - **Hard-capped nodes** — high-impact stats, e.g. Crit Chance max **+3%**, Max Resist Cap max **+2%**, CDR max **+5%**, Move Speed max **+5%**.
  - **Uncapped nodes** — baseline stats, e.g. `+0.5 Primary Stat`, `+2 Health`, `+3 Armor`.
  - **Soft-cap rule** — past **Rank 200** in any uncapped node, per-point returns drop by **50%**.

> **Resolved (B-01, v1.13).** The §7.3 JSON example formerly stated `totalVigilPointsEarned: 42` while its nodes allocate `15 + 210 + 50 = 275`. The **per-point math was correct** (see below) and the nodes are **provably correct** — §2.1's Rank-200 soft cap forces `conquest_primary_stat ≥ 200` points, so the nodes cannot shrink (§7.3 exists *to demonstrate* the soft-cap crossing). The `42` (= `142 − 100`) was therefore the error. **Ratified faucet: 1 Vigil Point per level past 100**, so the earned total must equal the allocated total. Corrected example → `characterLevel: 375, totalVigilPointsEarned: 275`. **Q-07 answered.** Full derivation in Action Plan **Appendix K**. *(This is the separate, infinite Vigil budget — not the finite 130-point tree above.)*

**Verified per-point conversions [Ratified, math audited]:**
- `conquest_primary_stat`: 200 pts × 0.5 = 100 → 10 pts × 0.5 × 0.5 = 2.5 → **102.5** ✔
- `resiliency_max_health`: 50 × 2 = **100** ✔
- `conquest_crit_chance`: 30 × 0.1% = **3%** = the hard cap ✔

### 5.2 Layer 2 — Class Talent Trees & Mastery Parity **[Ratified]**

- **Six base archetypes:** Warrior, Rogue, Sorcerer, Vanguard, Sage, Artificer.
- **Tree size [Ratified]:** each class tree is **~150 nodes / ~200 nominal TP** — **deliberately larger than any budget**. A player **never completes one**, so every point is a *choice*.
- **Dual-Class Mastery:** access to **two** distinct Class Talent Trees, with **full independent Talent Point pools for both** (no split required) — `P` into each tree.
- **Single-Class Mastery:** an **Empowered** tree with **higher depth gates** and **2× Talent Points** (`2P`) into that one tree.

**Depth gating [Ratified] (C-06 closed).** Nodes sit behind cumulative-investment gates, so the two paths diverge *automatically* — no special-casing:

| Tier | Gate (points spent in tree) | Access |
| :--- | :--- | :--- |
| 1 Minor | ≥ 0 | both paths |
| 2 Major | ≥ 20 | both paths |
| 3 Keystone | ≥ 50 | both paths |
| 4 Apex | ≥ 100 | **Empowered (Single) only** |

With `P = 60` **[Proposed]**, both paths award **120 TP**: **Dual** reaches **2 × Tier-3 Keystones** across two themes; **Single** reaches the **Tier-4 Apex + an Empowered-exclusive capstone** in one theme. **Parity axis [Ratified]: Dual = breadth/ceiling, Single = depth/consistency.** Full model in the action plan's **Appendix I**.

### 5.3 Layer 3 — Mastery Tree & Fusion Skills **[Ratified + Proposed]**

- **Fusion mechanics [Ratified]:** two actives combine into one high-impact ability.
  - *Dual-Class:* Class A skill + Class B skill — e.g. *Whirlwind* + *Chain Lightning* = **Storm Gale**.
  - *Single-Class:* two skills from one class into an apex — e.g. *Leap Slam* + *Earthquake* = **Tectonic Cataclysm**.
- **Fusion parity [Ratified] (C-06):** both paths receive **one** fused ability at **equal power budget** — Dual expresses it as *hybrid utility*, Single as *apex magnitude*.
- **Fusion table [Ratified] (C-08 closed):** the open combinatorial matrix (≈`15S² + 3S(S−1)` → ~1,128 abilities at `S = 8`) is replaced by a **curated exact table** with a parity-driven **floor of 21** — **15 class-pair recipes + 6 single-class apexes** — enforced by a **coverage validator**. Each recipe resolves to an equal `power_budget` (App. I.6). Full spec in the action plan's **Appendix J**.

### 5.4 Layer 4 — Individual Skill Trees & Glyphs **[Ratified + Proposed]**

- **Specialization slots [Ratified]:** slotted actives earn skill-specific XP in combat.
- **Mini-trees [Ratified]:** Skill Points buy behavioral shifts, elemental conversions, and utility.
- **Glyph sockets [Ratified]:** nodes accept **Glyphs** — e.g. *Glyph of Chaining, Multishot, Echoing, Execution*.
- **[Proposed] (F-07):**
  - Glyph rarity ladder: Common → Mythic.
  - Socket rule: **1 at skill Lv 1, +1 per 10 skill levels, max 3**.
  - Glyphs are **stat/behavior modifiers only** (never new code paths) — implemented via the modifier stack.
  - **[Open] (B-09):** number of specialization slots is undefined.

### 5.5 Attributes **[Proposed] (G-01)**

"Primary Stat" is referenced across the source but never defined. Proposal — four primary attributes, each class biased to a primary + secondary:

| Attribute | Governs |
| :--- | :--- |
| **Might** | Melee damage, Armor |
| **Agility** | Crit chance, Evasion, Attack speed |
| **Insight** | Spell damage, Mana/Focus, Ailment chance |
| **Resilience** | Life, Resist cap |

Retains the §7.3 convention of `+0.5 Primary Stat` per Vigil point.

### 5.6 Respec Model **[Proposed] (G-10)**

| Layer | Model |
| :--- | :--- |
| Global passive | Free during campaign; **paid** (currency) post-campaign |
| Skill mini-tree | Free |
| Class / Talent | **Locked per character** |

> Table-stakes for player trust; must be ratified before any tree is authored.

---

## 6. Classes

**[Ratified]** the six archetypes exist. **[Proposed] (F-09)** the following identities, resources, and signature mechanics:

| Class | Fantasy | Resource | Signature | Attribute bias |
| :--- | :--- | :--- | :--- | :--- |
| **Warrior** | Duelist / raw physical | Rage (built by hits) | Whirlwind, Leap Slam | Might / Resilience |
| **Rogue** | Assassin / evasion | Combo points | Shadow Step, multishot | Agility |
| **Sorcerer** | Arcane artillery | Mana | Chain Lightning, Frost Nova | Insight |
| **Vanguard** | Shield bruiser / protector | Stamina | Shield Bash, Guard aura | Might / Resilience |
| **Sage** | Support / summoner / DoT | Focus | Ailment spread, wards | Insight / Agility |
| **Artificer** | Traps, constructs, elements | Charges (gadgets) | Turrets, mines, elemental infusions | Insight / Might |

**Parity rule [Proposed]:** every class must field **≥1 viable melee-range** and **≥1 ranged** build, so no class is locked out of a fight pattern.

---

## 7. Combat & Damage System

### 7.1 Damage-Type Taxonomy **[Ratified — author ruling]**

A **closed set of six damage types**:

| # | Damage Type | Elemental? | Axis | Mitigated by |
| :-- | :--- | :--- | :--- | :--- |
| 1 | **Physical** | No | Material | Armor (DR) |
| 2 | **Fire** | **Yes** | Elemental | Fire Resistance |
| 3 | **Lightning** | **Yes** | Elemental | Lightning Resistance |
| 4 | **Ice** | **Yes** | Elemental | Ice Resistance |
| 5 | **Radiant** | **No** | **Cleansing / Beacon** | Radiant Resistance |
| 6 | **Umbral** | **No** | **Corruption / Void** | Umbral Resistance |

**The Radiant ↔ Umbral axis.** **Radiant** is the *cleansing* polarity (the World Sieve, the Beacon, the purging of Tameria Island); **Umbral** is its *corruption/void* opposite (the Calamity, taint, the Rejection). They are **mirror types** — both **non-Elemental**, and neither is reached by "All Elemental" modifiers.

**Formal Elemental rule:**
```text
ELEMENTAL ≡ { Fire, Lightning, Ice }     // exclusive membership
Radiant   ∉  ELEMENTAL
Umbral    ∉  ELEMENTAL
Physical  ∉  ELEMENTAL
```

Any modifier worded **"All Elemental Resistance(s)"** resolves to **exactly Fire + Lightning + Ice**.

**Conversion & class coverage [Ratified — v1.16, closes B-18].** Every damage type is *reachable*, so none is a dead enum member:
- **Conversion channel** — a skill's damage type can be converted via a **skill-tree node** (global web or skill mini-tree) **or a socketed glyph**. Conversion occurs at **pipeline stage 2 (§7.4)**, on the **flat base**, before any scaling; `Σ converted_out ≤ 100%` per source type.
- **Class-coverage rule** — **every class must guarantee ≥3 distinct damage types** through its skills. Together with conversion, this is how the previously "orphan" types are supplied.
- **Enemies mirror the taxonomy** — each Act introduces foes dealing one or more of the five non-Physical types, so every resistance matters in play.
- **No relic grants `Umbral` favor** (the Precursor relics are cleansing-aligned; §5).

**Non-damage channels — must not be modelled as damage types:**
- **Calamity** — a **foe category** ("+3% Damage vs. Calamity Foes"), not a type.
- **Hazard** — an **environmental channel** ("-10% Hazard Damage Taken"), separate from resistances.

### 7.2 Resistance Stats **[Ratified]**

**Five** discrete resistances — **Fire, Lightning, Ice, Radiant, Umbral** — plus **Armor** for Physical. Together these are **six mitigation channels — exactly one per damage type** (Armor for Physical; a percentage resistance for each of the other five). "All Elemental Resistance" is a **scope**, not a stat.

- **Base cap [Proposed, v1.14]:** **75%** per type (the source states only the Vigil "+2% Max Resist Cap") → **Q-09 answered**.
- **Floor:** **−100%** (a fully exposed target takes at most 2× damage).
- **Vigil "+2% Max Resist Cap" [Resolved, v1.14]:** applies to **all five** percentage resistances **including Radiant and Umbral** → **77%** cap. **B-20 closed.**
- **"All Resistances" [Resolved, v1.14]:** the term is **retired**; the only legal collective scope is **"All Elemental Resistance(s)"** ≡ Fire + Lightning + Ice. **B-19 closed.**

### 7.3 Mitigation & Offense Formulas **[Proposed] (G-02 / F-02)**

> This is the **Combat Formula Charter**. Structural rules (stage order, rounding, scope) need sign-off; numeric constants are tuning proposals. Develop **spreadsheet-first**, implement in GDScript only after tuning passes in the sheet. Full detail in Action Plan **Appendix L**.

| Constant | Value | Note |
| :--- | :--- | :--- |
| Accuracy / Evasion | `HitChance = clamp(Acc / (Acc + Evasion × k), 0.05, 1.0)` | `k = 1.0` [Proposed] in-campaign |
| Armor DR | `DR = clamp(Armor / (Armor + 10 × EnemyLevel), 0, 0.90)` | consumes Vigil "+3% Armor/DR" |
| Resistance cap / floor | cap **75%** (→ **77%** Vigil); floor **−100%** | §7.2 |
| Crit multiplier | base **150%**, `+ Σ crit_multi` additive | |
| Crit chance cap | **global 60%**; **Vigil node cap +3%** | **B-08 resolved, v1.14 (different scopes)** |
| "Damage vs. Calamity" | a **single global multiplier** stage (not a type) | see §7.4 |

> **B-08 (crit scope) — resolved (v1.14).** The T10 `+8%` crit affix and the Vigil `+3%` are **different scopes**: the Vigil value is a **node-track cap** (how much *that node* may contribute), **not** a global character cap. The global character crit-chance cap is **60%** [Proposed]. Rename the §2.1 node stat to *"Crit Chance (Vigil node, max +3%)"* in authoring.

### 7.4 Damage-Resolution Pipeline **[Proposed] (G-02 — P0 blocker, v1.14)**

The ordered resolver — the thing every affix rolls into. **Ordering is the design**; moving a stage changes the result. Evaluated per damage type, in the fixed order `[Physical, Fire, Lightning, Ice, Radiant, Umbral]`.

```text
 STAGE 0  Snapshot           gather all inputs into one immutable attack record
 STAGE 1  Source collection  base (per type) + added flat (per type)
 STAGE 2  Conversion         move damage between types — BEFORE any scaling
 STAGE 3  Increased / More   additive "increased", then multiplicative "more"
 STAGE 4  Global multipliers "vs Calamity", grade, conditional global "more"
 STAGE 5  Accuracy / hit     miss -> 0 damage, no ailments
 STAGE 6  Critical strike    roll; if crit, apply CritMultiplier
 STAGE 7  Penetration        reduce target's effective resistance (this type)
 STAGE 8  Mitigation         Armor DR (Physical) or Resistance (other five)
 STAGE 9  Ailment roll       never on a miss; a crit GUARANTEES its type's ailment
 STAGE 10 Application        round ONCE, subtract life, death check
```

**Normative rules:**
- **Conversion before scaling**, on `flat` only; `Σ out ≤ 100%` per source type.
- `dmg[t] = flat[t] × (1 + Σ increased[t]) × Π (1 + more[t]) × Π global_more`.
- **Cap-test order:** `eff_res = clamp(raw_res − pen, −1.00, cap)` — penetration is subtracted **before** the cap.
- **Single rounding:** carry `float64` through all stages; round **exactly once** at stage 10.
- **Hazard** (env. channel) is a flag on the damage event applied **after** stage 8, never a type.

**Worked DoD example (Lv 70 attacker → Armor 2,000 / Fire-80%-over-cap target):** `200 Physical`, 50%→Fire, `+40 Fire`, `+80% inc Fire`/`+30% inc Phys`, `×1.25 more`, `+3% vs Calamity`, `35% crit`/`+40% multi`, `15% Fire pen` ⇒ **298 damage** (216 Fire + 82 Physical) + Ignite. Full stage-by-stage arithmetic in Action Plan **Appendix L.6**.

**Definition of done — met:** a damage event resolves end-to-end for all six types against a target with mixed resistances and an **over-cap** value, **reproducibly from the written spec alone**. ✔

**"Damage vs. Calamity"** is a **single global multiplier (stage 4)** — it applies uniformly to every type and is **not** a damage type.

### 7.5 Ailments & CC **[Proposed] (G-04 / F-03)**

Cap at **6 ailments, 3 CC types** at launch; expand post-launch.

| Ailment | Type | Effect |
| :--- | :--- | :--- |
| Ignite | Fire | Damage-over-time |
| Chill / Freeze | Ice | Slow / hard CC |
| Shock | Lightning | Increased damage taken |
| Bleed | Physical | DoT while moving |
| Corrupt | Calamity | DoT that ignores a % of resistance (thematic) |
| Radiant | Radiant | Burning + debuff-cleanse interaction |
| Umbral | Umbral | Corrupting DoT that scales with the target's missing life |

Directly feeds §5's *"+5% Fire & Radiant Resistance"* and *"-10% Debuff Duration."*
**Boss rule [Proposed]:** enforce an internal **CC-immunity ramp** (diminishing returns per application), or every boss becomes cheeseable.

> **[Resolved] (B-18 — closed v1.16):** the "orphan damage types" defect is closed by the **six-type taxonomy + conversion channel + class-coverage rule** (§7.1). Every type now has sources; none is a dead enum member.

### 7.6 Corruption — Master Difficulty Scalar **[Proposed] (v1.14, closes B-06 / Q-06)**

Corruption `c ∈ [0,1]` (the per-Act values in §12.1) is the campaign's **single master difficulty scalar**: it scales the **enemy side** of the pipeline. Affine, zero-based at Act 1:

```text
EnemyHP        ×= 1 + (c - 0.10) × 3.00
EnemyDamage    ×= 1 + (c - 0.10) × 1.60
AilmentChance  ×= 1 + (c - 0.10) × 1.00
RarePackDensity×= 1 + (c - 0.10) × 1.30
ItemRarity     += (c - 0.10) × 100      (percentage points)
```

| Act | Corruption | HP × | Dmg × | Ailment × | Rare-pack × | Item Rarity |
| :-- | ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 10% | 1.00 | 1.00 | 1.00 | 1.00 | +0% |
| 2 | 25% | 1.45 | 1.24 | 1.15 | 1.20 | +15% |
| 3 | 45% | 2.05 | 1.56 | 1.35 | 1.46 | +35% |
| 4 | 60% | 2.50 | 1.80 | 1.50 | 1.65 | +50% |
| 5 | 75% | 2.95 | 2.04 | 1.65 | 1.85 | +65% |
| 6 | 95% | 3.55 | 2.36 | 1.85 | 2.11 | +85% |
| 7 | Breach axis | — | — | — | — | — |

Corruption is **two-sided**: harder **and** more rewarding (aligns with the Taint tradeoff). It is deliberately **not** attached to enemy elemental bias, pack composition, or boss modifiers — those belong to zone/rift modifiers.

---

## 8. Itemization & Equipment

### 8.1 Rarity Tiers & Affix Caps **[Ratified]**

Affixes are strictly capped at **3 Prefixes + 3 Suffixes (max 6)**.

| Rarity | Affix count | Rules | Grade eligible? |
| :--- | :--- | :--- | :--- |
| **Common** | 0 | Baseline item | No |
| **Uncommon** | 1–2 | Standard mix (1P + 1S) | No |
| **Rare** | 2–4 | 2-affix items **must be skewed** (2P or 2S); 3–4 mixed | No |
| **Epic** | 3–6 | 3- and 4-affix items **must be skewed**; 5–6 mixed | No |
| **Legendary** | 5–6 | 5 ⇒ `3P+2S`/`2P+3S`; 6 ⇒ `3P+3S` (see §8.2b) | **Yes (F to S)** |
| **Mythic** | 6 | Fixed max allocation (3P + 3S) | **Yes (B to SSS)** |

### 8.2 Corrected Affix Classification Matrix **[Ratified — author ruling]**

**Rule:** the "3 Prefixes OR 3 Suffixes" skew clause applies **exclusively to Epic**. An Epic item with **4 affixes** may use **only** `3P+1S` or `1P+3S`. A **2P+2S** split is **never Epic** — a 2/2 item is **definitionally Rare**.

| Rarity | Affix count | Legal splits |
| :--- | :--- | :--- |
| Rare | 2 | `2P+0S` or `0P+2S` (skewed) |
| Rare | 3–4 | mixed (`2P+1S`, `1P+2S`, `2P+2S`) |
| Epic | 3 | `3P+0S` or `0P+3S` (skewed) |
| Epic | 4 | **`3P+1S` or `1P+3S`** |
| Epic | 5–6 | mixed |
| Legendary | 5–6 | mixed ("standard high-tier mix") |
| Mythic | 6 | fixed `3P+3S` |

> **Summary:** *Rare = balanced, Epic = skewed*, with the 2/2 split as the exact boundary.
> **[Resolved — v1.15] Q-01 / Q-02 / Q-03 / Q-04, B-10 / B-11 / B-12 — see §8.2b.**

### 8.2b Generation Order & Canonical Rarity → Split Table **[Proposed] (v1.15)**

**Ordering ruling — *rarity-first*.** Rarity is the **authoritative, explicitly-rolled** field; the affix **count** and the **prefix/suffix split** are **derived** from it and never inferred back. This dissolves the "overlapping ranges" defect: no item is ever ambiguous by count.

```text
roll RARITY  →  pick COUNT  →  pick SPLIT  →  pick STAT  →  pick TIER  →  roll VALUE
```

| Rarity | Rolled count (weights) | Legal splits |
| :--- | :--- | :--- |
| **Common** | 0 (100%) | — |
| **Uncommon** | 1 (70%) · 2 (30%) | 1 → `1P+0S`/`0P+1S` · 2 → **`1P+1S`** |
| **Rare** | 2 (45%) · 3 (35%) · 4 (20%) | 2 → `2P+0S`/`0P+2S` · 3 → `2P+1S`/`1P+2S` · 4 → **`2P+2S`** |
| **Epic** | 3 (20%) · 4 (40%) · 5 (25%) · 6 (15%) | 3 → **`3P+0S`/`0P+3S`** · 4 → **`3P+1S`/`1P+3S`** · 5 → `3P+2S`/`2P+3S` · 6 → `3P+3S` |
| **Legendary** | 5 (55%) · 6 (45%) | 5 → `3P+2S`/`2P+3S` · 6 → `3P+3S` |
| **Mythic** | 6 (100%) | `3P+3S` (fixed) |

- **Q-01:** Epic 3-affix = `3P+0S`/`0P+3S`. ✔
- **Q-02:** Rare = the **2–4 family** (2 = skewed, 3 = `2P+1S`/`1P+2S`, 4 = `2P+2S`); *not* "only 2P+2S".
- **Q-04 / B-11:** Legendary 5 ⇒ `3P+2S`/`2P+3S`; 6 ⇒ `3P+3S`. **"Standard high-tier mix" is superseded.**
- **Discriminator:** `1P+1S` = Uncommon · `2P+0S`/`0P+2S` = Rare · `2P+2S` = Rare(4) · `3P+1S`/`1P+3S` = Epic(4).

*Corroboration:* the spec's own §7.1 worked item is a Legendary `3P+2S` — exactly the Legendary-5 rule. Full derivation in Action Plan **Appendix M**.

### 8.3 Affix Tier Pools **[Ratified]**

| Rarity | Standard affix tiers | Exclusive affixes |
| :--- | :--- | :--- |
| Uncommon → Epic | Tier **0–10** | — |
| Legendary | Tier **5–10** | + **Legendary** affixes |
| Mythic | Tier **9–10** | + Legendary affixes + pinnacle **Mythic** affixes |

**[Resolved — v1.15] (B-03)** — the tier→value table is now defined as a **shared ladder + per-stat anchor**:

```text
value(stat, T) = T10Anchor(stat) × R[T] × uniform(0.90, 1.00)
R (T0..T10)    = [0.05, 0.08, 0.12, 0.17, 0.24, 0.32, 0.42, 0.55, 0.70, 0.85, 1.00]

maxTier(ilvl)   = clamp(idiv(ilvl, 6), 0, 10)     // T10 at ilvl ≥ 60
minTier(rarity) = Uncommon/Rare/Epic → 0 · Legendary → 5 · Mythic → 9
```

Strictly monotone with **no overlap** — every adjacent ratio `R[T+1]/R[T] ≥ 1.17 > 1.111`, so a higher tier always beats the one below. `T10Anchor(stat)` is authored per stat.

### 8.4 Unique Items **[Ratified]**

- **[Ratified]** Uniques carry a **fixed, build-defining mechanic set** — they **never roll a different affix** (no random affix *identity*).
- **[Ratified — author ruling, C-02 resolved]** "Fixed" qualifies **selection, not value**: a unique whose slot is defined as *Fire Resistance 30–60* can **only** roll Fire Resistance there, but its **magnitude rolls within that range**. A Unique is therefore **deterministic in shape, variable in magnitude** — a "good roll" chase with no "wrong affix" outcome.
- **[Ratified]** A Unique can drop at **any rarity Uncommon→Mythic** (never Common); higher rarity unlocks **gated unique affixes** and **widens the numeric roll ranges**.
- **[Ratified]** The **grade multiplier** (§9.1) applies on top of the rolled value for Legendary/Mythic uniques.
- **[Proposed] (F-xx):** ship **~30 uniques** at launch.
- **[Resolved — v1.15] (Q-03 / B-03):** generation order is **rarity → count → split → stat → tier → value** (§8.2b), and the per-tier values are the §8.3 ladder. Uniques use the same order; their "fixed" set means the **stat identity** is pre-authored, only the **value** rolls (within the rarity-scaled range).

### 8.5 Base Types, Implicits & Item Level **[Proposed] (v1.15 — B-02 / B-03 closed)**

- **Implicits [Resolved — B-02]:** each base type carries **exactly one implicit** (its identity). An `implicits[]` array is added to the schema (§7.1), and the **grade multiplier applies** to it (§9.1).
- **`itemLevel`:** gates `maxTier` (§8.3) and the affix pool.
- **`requiredLevel` = `max(1, itemLevel − 4)`** [Proposed].
- **Still to author:** the **base-type catalog** per slot (each with its implicit + socket capacity) and absolute **drop tables / drop rates** (economy gap **G-06**).

### 8.6 Equipment vs. Skill Sockets **[Ratified]**

| Socket location | Accepts |
| :--- | :--- |
| Equipment sockets | **Calamity Crystals** (stat gems) or **Precursor Runes** (gear utility/defense) |
| Layer-4 skill-tree sockets | **Glyphs** (skill augment mods) |

---

## 9. Quality Grade System & Forging

### 9.1 Grade Stat Multipliers **[Ratified]**

Grades apply **exclusively** to **Legendary (F–S)** and **Mythic (B–SSS)** items, acting as a global multiplier across **base damage/defense, implicits, and all affix values**:

```text
Final Stat = Base Value × Grade Multiplier

F (80%) → E (85%) → D (90%) → C (95%) → B (100% baseline) → A (110%) → S (120% Leg max) → SS (130%) → SSS (150% Mythic max)
```

### 9.2 Grade Forging — *The Purified & Calamity Anvils* **[Ratified]**

Each attempt with Catalysts resolves to one of three outcomes:

1. **Success** — grade **+1** step.
2. **Neutral** — materials consumed; grade unchanged.
3. **Failure** — materials consumed; grade **−1** step.

**Design ruling (C-03 — Accepted).** The "brick" (downgrade) risk is **retained deliberately** — it is genre-core, benchmarked against Path of Exile's corruption currency. Risk is healthy **when it is opt-in, terminal, and mitigated**; Tameria adds the mitigation ladder below.

**Edge cases (closes B-07):**
- At the **cap (S / SSS):** a Success roll is a **no-op**; materials are **not** consumed.
- At the **floor (F / B):** a Failure roll is a **no-op**; no underflow.

**Mitigation-currency ladder [Proposed]:**

| Family | Item | Effect | PoE analogue |
| :-- | :-- | :-- | :-- |
| Odds-tip | **Tempering Catalyst** | Next attempt: Failure → **Neutral** (no downgrade) | "Cannot be changed" |
| Odds-tip | **Resonant Catalyst** | Next attempt: **+X% Success** | Quality / lucky |
| Preview | **Seer's Lens** | Reveals the next outcome **before** committing | Hinekora's Lock |
| Guarantee | **Warden's Sigil** | Next attempt: **guaranteed Success** | — |
| Anchor | **Grade Anchor** | **Permanent:** grade can never drop below its current value | Fracturing Orb |
| Recovery | **Restorative Catalyst** | Restores the item to its **highest grade previously achieved** | Eternal Orb (legacy) |
| High-risk | **Ruinous Anvil** *(mode)* | May jump **+2 grades** or **strip the grade**; applies a **Calamity-Touched** flag blocking further forging | Vaal Orb |

**Two-anvil structure [Ratified].** The forge splits along the game's central **Cleansed ↔ Corrupted** axis (mirroring the Purifier/Symbiote factions):

| Anvil | Theme | Outcomes | Cost |
| :-- | :-- | :-- | :-- |
| **The Purified Anvil** | Cleansed | Success / Neutral only (no downgrade) | **Higher** |
| **The Calamity Anvil** | Corrupted | Success / Neutral / Failure (±1) | Lower, higher ceiling |

The **Purified Anvil** is the sanctuary's method (clean, slow, costly); the **Calamity Anvil** is *wielding the taint* (fast power, instability) — the crafting expression of the Hero's Rejection and the post-campaign Purifier/Symbiote split. The mitigation ladder below applies to the **Calamity Anvil**.

**Floor asymmetry (Legendary F=80% vs Mythic B=100%) [Ratified intentional]:** *premium rarity ⇒ baseline-or-better floor* — the wider Legendary band is a risk the player opts into (Calamity Anvil) or avoids (Purified Anvil).

---

## 10. Precursor Relics & World Sieve Favor

**[Ratified]** Three relics are recovered during the campaign and grant global permanent favor:

| Relic | Act | Favor |
| :--- | :--- | :--- |
| **The Sunken Aegis** | Act 2 | `+5% Max Life` \| `+3% Armor/DR` \| `+3% All Elemental Resistances` |
| **The Hearth of Ignition** | Act 3 | `+5% Fire & Radiant Resistance` \| `-10% Debuff Duration` \| `+3% Damage vs. Calamity Foes` |
| **The Astral Key** | Act 5 | `+3% Movement Speed` \| `+5% Cooldown Reduction` \| `-10% Hazard Damage Taken` |

### 10.1 Derived Total Favor **[Corrected — author ruling]**

Because **Radiant is not Elemental**, the Aegis's "+3% All Elemental" does **not** apply to Radiant. Derived totals:

| Type | Aegis | Hearth | **Derived total** |
| :--- | :--- | :--- | :--- |
| Fire | +3% | +5% | **8%** |
| Lightning | +3% | — | **3%** |
| Ice | +3% | — | **3%** |
| **Radiant** | **0%** (not Elemental) | +5% | **5%** |

**Corrected copy (replaces the source's printed `+8% Fire/Radiant`):**
> `+5% Max Life` \| `+3% Armor/DR` \| `+3% Fire/Lightning/Ice Resistance (+8% Fire, +5% Radiant)` \| `+3% Move Speed` \| `+5% CDR` \| `+3% Damage vs Calamity` \| `-10% Debuffs & Hazard Damage`

**[B-15 — CLOSED, v1.17]** This is the **adopted wording**; the source's printed `+3% All Resistances (+8% Fire/Radiant)` is superseded. **Copy-only** change — relic numbers are unchanged.

> **[Open] (B-04 / Q-05):** are relic favor effects **live on pickup**, or only once **socketed into the World Sieve**? The source labels the total "(Act 7+)" but never states activation timing.
> **[Open] (B-17):** the Sieve sits on the now-inaccessible island, yet the endgame operates from the Ward — the relationship is unstated.

---

## 11. Endgame — Calamity Rifts

**[Ratified]**

- **Keystones (Tier 1–100+):** set monster level, health, and damage scaling.
- **Cleansing Meter:** slaying corrupted mobs drops **Calamity Motes**; at **100%** the area is cleansed and an **Apex Rift Guardian** spawns.
- **Loot weighting (no minimum grade floors):** high-risk modifiers — *Spatial Instability, Miasmic Tide, Vampiric Taint* — do **not** enforce guaranteed grade floors. Instead they scale **Item Quantity** and increase the **weighted probability** of Mythic drops and higher initial Quality Grades.

**[Proposed] (F-11 / G-05):**
- Ship **~10 rift modifiers** at launch, weighted, on one reusable `RiftGenerator`.
- **Pity system:** after N rifts without a Mythic, escalate weighted probability (the spec's own "weighted probability" language invites this).
- **Forbidden zone rule:** never let keystone scaling compound with untelegraphed rift modifiers to one-shot the player without a visual warning.

> **[Open] (§2.6):** the Cleansing Meter has no mob count, time pressure, or fail state defined; the rift-modifier pool is 3 named of an unspecified total.

---

## 12. World, Narrative & Content

### 12.1 Campaign Structure **[Ratified]**

7-Act linear campaign, Levels 1–70:

| Act | Region | Corruption | Milestone |
| :--- | :--- | :--- | :--- |
| 1 | Whispering Frontier | 10% | — |
| 2 | Fallen Marches | 25% | Recover **The Sunken Aegis** |
| 3 | Iron Crags | 45% | Recover **The Hearth of Ignition** |
| 4 | Shattered Coast | 60% | — |
| 5 | Miasmic Voyage | 75% | Recover **The Astral Key** |
| 6 | Tempest Ring | 95% | — |
| 7 | Tameria Island | 20% Breach → Purged Sanctuary | Activate the **World Sieve** |

> **[Ratified — v1.7] Breach defined (C-04 closed).** See §12.1.1.
> **[Resolved — v1.14] Corruption is the master difficulty scalar (B-06 / Q-06 closed).** Each Act's Corruption value drives enemy HP, enemy damage, ailment chance, rare-pack density, **and** item rarity (two-sided risk/reward). Formula + table in **§7.6**.
> **[Ratified — v1.10] Act × Level × Points map (C-05 / B-13 closed).** See **§12.1.3**.

#### 12.1.1 Breach — Zone Barrier-Penetration Metric **[Ratified]**

**Breach** = the percentage of Calamity corruption that has **physically penetrated the barrier** of Tameria Island before the World Sieve is fully activated. It is a **zone-level** metric — distinct from the hero's taint (**Corruption**).

- **Type:** dynamic float, `0.0%`–`100.0%`.
- **Act 7 starts at `20.0%`** — 20% of the perimeter is breached; drives environment rendering (tainted ground vs. pristine marble), spawn density, and hazard spawns.
- **Objective loop:** sub-objectives + relic activation reduce it: `20.0 → 0.0`.
- **At `0.0%`:** the World Sieve fires a total purge → the zone becomes cleansed & impenetrable → the Hero is rejected (keyed to personal taint).

| Relic | Δ Breach |
| :-- | :-- |
| Sunken Aegis | −5.0 |
| Hearth of Ignition | −5.0 |
| Astral Key | −10.0 |

Loop: `20.0 → 15.0 → 5.0 → 0.0` (order-independent; sum = `20.0`). **Clamp at `0.0` (B-21).**

```json
{
  "zone_id": "act7_tameria_sanctum",
  "zone_state": {
    "breach_percentage": 20.0,
    "is_purged": false,
    "active_environment_profile": "corrupted_sanctuary_tier1",
    "spawns_calamity_hazards": true
  },
  "relic_activation_triggers": [
    { "relic_id": "sunken_aegis", "breach_reduction": 5.0 },
    { "relic_id": "hearth_of_ignition", "breach_reduction": 5.0 },
    { "relic_id": "astral_key", "breach_reduction": 10.0 }
  ]
}
```

#### 12.1.2 Taint — The Hero's Own Corruption **[Ratified]**

Fighting through the corrupted world **taints the Hero**. This is the player character's own corruption — distinct from an Act's *environmental* Corruption and from *Breach*. Causal chain: **Act Corruption → Hero Taint → Rejection (Act 7).**

| Axis | Scope | Meaning |
| :-- | :-- | :-- |
| **Corruption** | Zone / Act | Environmental intensity (10/25/45/60/75/95%) |
| **Taint** | Hero | How corrupted the player character has become |
| **Breach** | Zone (Act 7) | Barrier penetration before the Sieve |

**Accumulation — hybrid model [Ratified].**

```text
Taint = clamp( max(ActFloor[act], Accrued), 0, 100 )
Accrued += exposure_rate(zone, act) × mitigation_multiplier × dt
```

- **ActFloor** — an unavoidable minimum per Act; **guarantees the Rejection for every player**.
- **Exposure** — time in corrupted zones, hazard damage taken, Calamity kills, rift exposure.
- **Mitigation** — gear / relics / resistances lower the *rate*.
- **Cleansing** — reduces taint **toward** the floor, never below.

The **Rejection Threshold (proposed 75)** sits at/below `ActFloor[7]`, so the story cannot be "beaten clean" — only the *excess above the floor* varies, and that excess drives the endgame build.

**Effects — a two-sided tradeoff [Ratified].** Taint is attuned to the **Calamity** and repellent to the **cleansed** (hooking into the ratified damage taxonomy — **Radiant** is the cleansed type):

| Taint band | Vs. Calamity | Vs. Cleansed | World |
| :-- | :-- | :-- | :-- |
| **0–19 Clean** | Baseline | Baseline Radiant taken | Purifier NPCs friendly |
| **20–39 Touched** | +5% damage | +5% Radiant taken | — |
| **40–59 Tainted** | +10%; −5% Calamity hazard dmg | +10% Radiant taken | Symbiote vendor appears |
| **60–79 Corrupted** | +15% damage | +15% Radiant taken | Ward NPCs wary |
| **80–100 Revenant** | +20%; Calamity allies non-hostile in rifts | +20% Radiant taken | Symbiote skill line unlocked |

*(Values are proposals.)* **Visible:** armour/portrait corruption stages keyed to the band — satisfying Pillar **P2**, avoiding "purely cosmetic corruption."

**Endgame tie-in:** the post-campaign **Purifier vs Symbiote** factions become build paths — *Purifier* scrubs to the floor; *Symbiote* leans in. Mirrors the two-anvil structure (§9.2) on the character axis.

#### 12.1.3 Act × Level × Points Distribution **[Ratified]**

Closes **C-05 / B-13**. Three author rulings shape the map: (1) **level bands shrink** as the campaign deepens (leveling grows harder); (2) **quest points front-load** (they matter most early); (3) **all 30 quest points are earned in the campaign** — the endgame keeps its own exclusive systems.

**Curves.** Level-ups `14 + 12 + 11 + 10 + 9 + 8 + 5 = 69` (Lv 1 → 70); quest points `6 + 5 + 5 + 4 + 4 + 3 + 3 = 30`.

| Act | Region | Level band | Lv pts (cum) | Quest pts (cum) | **Total (cum)** | % of 130 |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| — | *(start)* | 1 | 1 | 0 | **1** | 1% |
| 1 | Whispering Frontier | 2–15 | 15 | 6 | **21** | 16% |
| 2 | Fallen Marches | 16–27 | 27 | 11 | **38** | 29% |
| 3 | Iron Crags | 28–38 | 38 | 16 | **54** | 42% |
| 4 | Shattered Coast | 39–48 | 48 | 20 | **68** | 52% |
| 5 | Miasmic Voyage | 49–57 | 57 | 24 | **81** | 62% |
| 6 | Tempest Ring | 58–65 | 65 | 27 | **92** | 71% |
| 7 | Tameria Island | 66–70 | 70 | 30 | **100** | 77% |
| — | **Outer Ward (endgame)** | 71–100 | 100 | 30 | **130** | 100% |

**Properties.** The tree reaches **130 / 130 exactly at Lv 100** — the level **Vigil Power** begins, so the two layers never compete. The campaign delivers **100 / 130 (77%)**; the final **30** points arrive in the endgame alongside its exclusive systems (Calamity Rifts, Vigil Power, Purifier/Symbiote), so **nothing needs to be deferred** to it and **nothing is overloaded** onto it. The exact bands and quest curve are **proposals** (tunable); the *structure* is ratified.

### 12.2 The Rejection & Endgame Pivot **[Ratified — the game's spine]**

Activating the **World Sieve** purges Tameria Island to **0% corruption**, turning it into an inaccessible paradise. The Hero — heavily infected — is **violently rejected** and expelled to **The Outer Ward**. Operating from *The Lonely Watch*, the Hero opens **Calamity Rifts** via the *Sieve Mirror* to cleanse localized tears before they reach the barrier.

**[Proposed] narrative elevation (F-xx):**
- **Foreshadow the taint** from Act 2; make the hero's corruption track **visible** (corrupting armor/portrait).
- Make the choice **earned, not scripted**: a late-Act-7 decision — *enter the sanctuary and die purified* vs *step back and become the Warden of the Ward*. The endgame is the **consequence** of choices.
- **Give the Ward a purpose:** *The Lonely Watch* is where the rejected heroes of previous cycles stood — the player joins a **lineage of exiled guardians**.

### 12.3 Lore & Factions **[Proposed] (F-08, F-12, F-13)**

| Element | Hook |
| :--- | :--- |
| **The Three Relics** | Each relic is the climax of a self-contained Act arc with an NPC embodying its theme: Aegis = sacrifice, Hearth = preservation, Astral Key = passage |
| **The Sieve's Makers** | The Precursor civilization that built the Sieve — their fate explains why the Calamity exists |
| **The Ward Cycle** | The order of exiled guardians on the Outer Ward and their unwritten history |
| **Factions: Purifiers vs Symbiotes** | Post-campaign: purge the taint or wield it — drives rift objective variety |
| **Side-quest economy** | Formalize the 30 quest points as rewards from named NPC arcs, not an invisible counter |

### 12.4 The Calamity — Defined Rules **[Proposed] (F-08)**

- It **mutates space** → explains rift modifiers.
- It is **selective** → explains why the hero is rejected but the island is purged.
- It is **precursor-adjacent** → explains the World Sieve and the relics.

### 12.5 Enemies & Bosses **[Proposed] (G-05, F-11)**

- **Enemy families:** ~8 per Act, mixing melee packs, ranged, casters, chargers, plus a **Calamity-mutated** variant that interacts with the Cleansing Meter.
- **Elite affix pool:** PoE-style modifiers (e.g. *Corrupting, Warding, Splitting, Volatile*). Elites are the primary difficulty lever between tiers.
  - **Note:** the source's *Vampiric Taint* is a **rift modifier** (§6.1), **not** an elite affix.
- **Boss ladder:** Act boss → **Apex Rift Guardian**, on a **3-phase + enrage** template with a CC-immunity ramp.
- **Campaign:** ~25 enemy families; 30 uniques; ~40 quests + side quests (full production scope).

### 12.6 Hub, Town & Waypoints **[Proposed] (G-08)**

The Act 7 pivot removes any sanctuary and supplies **no replacement**. The **Outer Ward / The Lonely Watch** must be formalized **early** as the permanent post-Act-7 hub — vendors, stash, waypoints — so its art and systems are not a surprise late in production.

---

## 13. Technical & Data Architecture **[Proposed]**

1. **Everything data-driven.** Itemization, passive trees, skill mini-trees, glyphs, fusions, rift modifiers, relics and Vigil nodes must be `Resource`/JSON-driven. The §7 schemas are the right instinct — extend them to **every** content type.
2. **Persistence spine first (G-11).** A single `SaveManager` with **item-DB versioning** (migration hooks per schema version) is required **before** content authoring — ARPGs iterate on item schemas forever.
3. **Central `StatModifier` pipeline.** One ordered resolver:
   `base → implicits → affixes (tier × grade) → relics → Vigil → rift modifiers`.
   Without it, ordering bugs are constant.
4. **Defer multiplayer (G-12).** Build **SSF-first**, architecture-ready but not networked at launch.
5. **Performance budget (G-15).** Lock a target now (e.g. **60 FPS / 200+ concurrent AI**).
6. **Fail-loud deserialisation.** Validate the §7.1 item schema at load so bad data fails loudly (inline validator).

---

## 14. UI / UX **[Proposed]**

Per production standards and pillar P3:

| Area | Design |
| :--- | :--- |
| Core RPG panels | **Fixed-position, non-draggable** panels (inventory, skills, stats) |
| Navigation | **Single-active-window** pattern with a **centralized bottom menu** |
| Progression | One **Character Plan** view showing all four layers as a single budget |
| Loot filter | **Mandatory** (with T0–T10 × F–SSS × rarity, unfiltered loot is unplayable) |
| Input | Full keyboard/mouse + gamepad parity; touch branch considered |
| Safety | UI must never obscure hazards or interaction points (collision-aware placement) |
| Accessibility | Colorblind modes, full remapping, text-size scaling |
| Tooltips | Must map **6 damage types + 5 resistances** clearly |

---

## 15. Meta, Persistence & Long-Term

| System | Status |
| :--- | :--- |
| Save / persistence + item-DB versioning | **[Proposed] critical (G-11)** |
| Stash | **[Proposed] critical (G-11)** |
| Seasons / ladder | **[Proposed] (G-12)** |
| SSF vs trade stance | **[Proposed] — decide (G-12)** |
| Difficulty modes (Normal/Cruel/Merciless) | **[Proposed] (G-13)** |
| Hardcore | **[Proposed] (G-13)** |
| Pity / protection crafting | **[Ratified] mitigation ladder defined (§9.2)** |

---

## 16. Balancing Framework **[Proposed]**

- **Whiten the loot floor (R2):** raise the Legendary grade floor F→**B**, *or* guarantee a "reforge currency" drop on F–D.
- **Decouple variance:** grade multiplies **base + implicits only**; affix **tiers** handle affix variance — this halves the compounding.
- **Two clean difficulty knobs:** **Corruption %** (campaign) and **keystone tier** (endgame).
- **Fusion table capped** at ~15–20 recipes; **Glyphs** as modifier-stack entries only.
- **Attribute system** (4 stats) + **Combat Formula Charter** are prerequisites for any numeric balance pass.

---

## 17. Critical Path to Design Lock

The load-bearing walls — no content authoring until these are resolved:

| # | Gate | Source |
| :--- | :--- | :--- |
| 1 | Close the open register (C-02→C-08, B-01→B-20, Q-01→Q-09) | Action Plan §2 |
| 2 | **Combat Formula Charter** approved | GDD §7.3 |
| 3 | **Damage-Resolution Pipeline** ratified | GDD §7.4 |
| 4 | **Persistence spine** specified | GDD §13 |
| 5 | **Item / Skill schemas** versioned | GDD §13, §8 |
| 6 | **Act × Level × Points** matrix published | B-13 |
| 7 | **6 class identities** locked | GDD §6 |

**Immediate next step:** the **Damage-Resolution Pipeline spec (v0.1)** (§7.4) and the **§5 favor-copy fix** (§10.1) — the latter is the only author-confirmed numeric erratum outstanding.

---

## Appendix — Data Schemas (from source §7)

### A.1 Item **[Ratified — extended v1.15]**
```json
{
  "itemId": "weapon_sword_042",
  "name": "Sun-Shatterer",
  "itemType": "OneHandSword",
  "baseRarity": "Legendary",
  "itemLevel": 62,
  "requiredLevel": 58,
  "qualityGrade": "A",
  "gradeMultiplier": 1.10,
  "isUnique": false,
  "implicits": [
    { "stat": "FlatPhysicalDamage", "value": 24, "finalValue": 26.4, "source": "base" }
  ],
  "sockets": {
    "maxCapacity": 2,
    "insertedComponents": [
      { "type": "CalamityCrystal", "id": "ruby_flawless", "stat": "FlatFireDamage", "value": 45 },
      { "type": "PrecursorRune", "id": "rune_of_warding", "stat": "ArmorPercent", "value": 0.05 }
    ]
  },
  "affixes": [
    { "slot": "Prefix", "type": "Prefix", "tier": 8,  "stat": "PhysicalDamagePercent",  "baseValue": 120,  "finalValue": 132 },
    { "slot": "Prefix", "type": "Prefix", "tier": 10, "stat": "FlatPhysicalDamage",      "baseValue": 50,   "finalValue": 55 },
    { "slot": "Prefix", "type": "Prefix", "tier": "Legendary", "stat": "ArmorPenetration", "baseValue": 0.15, "finalValue": 0.165 },
    { "slot": "Suffix", "type": "Suffix", "tier": 9,  "stat": "AttackSpeedPercent",       "baseValue": 0.12, "finalValue": 0.132 },
    { "slot": "Suffix", "type": "Suffix", "tier": 10, "stat": "CriticalStrikeChance",     "baseValue": 0.08, "finalValue": 0.088 }
  ]
}
```
> **Extended v1.15:** `itemLevel`, `requiredLevel`, `implicits[]` and a per-affix `slot` added (§8.5, B-02/B-03). Per-tier values come from the §8.3 ladder; `baseRarity` is **authoritative** (§8.2b). This item is a Legendary `3P+2S` — exactly the §8.2b Legendary-5 rule.

### A.2 Skill & Glyph Socket **[Ratified]**
```json
{
  "skillId": "skill_warrior_whirlwind",
  "skillLevel": 18,
  "assignedSpecializationSlot": 1,
  "miniTreeAllocations": [
    { "nodeId": "node_aoe_radius_1", "pointsSpent": 3, "maxPoints": 3 },
    { "nodeId": "node_elemental_convert_fire", "pointsSpent": 1, "maxPoints": 1 }
  ],
  "glyphSockets": [
    {
      "socketIndex": 0,
      "unlocked": true,
      "insertedGlyph": {
        "glyphId": "glyph_chaining",
        "name": "Glyph of Chaining",
        "effect": "Causes whirlwind shockwaves to chain to 2 nearby enemies."
      }
    }
  ]
}
```

### A.3 Vigil Power Matrix **[Ratified — B-01 corrected]**
```json
{
  "characterLevel": 375,
  "totalVigilPointsEarned": 275,
  "softCapRank": 200,
  "nodes": {
    "conquest_crit_chance":   { "type": "HardCapped", "points": 15,  "maxPoints": 30,  "currentBonus": 0.015 },
    "conquest_primary_stat":  { "type": "Uncapped",   "points": 210, "softCapRank": 200, "currentBonus": 102.5 },
    "resiliency_max_health":  { "type": "Uncapped",   "points": 50,  "softCapRank": 200, "currentBonus": 100 }
  },
  "pointsSpent": 275,
  "pointsUnspent": 0
}
```
> Faucet rule: **1 Vigil Point per level past 100** (`earned == characterLevel − 100`). `375 − 100 = 275` = `15 + 210 + 50` ✔. See §5.1 and Action Plan **Appendix K**.

---

## Appendix — Change Log vs. Source Spec (v1)

| # | Change | Reason |
| :--- | :--- | :--- |
| 1 | Damage taxonomy formally closed: Physical/Fire/Lightning/Ice/Radiant; Elemental ≡ {Fire, Lightning, Ice}; Radiant **not** elemental | Author ruling |
| 2 | §5 favor total corrected: Radiant **5%** (not 8%); "All Resistances" scope replaced | Author ruling (B-15, B-19) |
| 3 | Epic 4-affix split fixed to `3P+1S` / `1P+3S`; `2P+2S` = Rare | Author ruling (C-01 withdrawn) |
| 4 | Unique roll semantics defined — "fixed" = affix **identity**; values roll within a range (C-02 resolved) | Author ruling |
| 5 | Forge "brick" risk **retained** (genre-core); **two-anvil structure approved** — Purified/Calamity, on the Cleansed↔Corrupted axis; mitigation ladder added; B-07 closed; floor confirmed intentional (C-03 closed) | Author-approved |
| 6 | **Breach** defined — zone barrier-penetration metric (`0–100%`; Act 7 `20% → 0%`); zone-state schema supplied (C-04 closed) | Author definition |
| 7 | **Taint** defined — hybrid model (Act floor + exposure) + mechanical/visible tradeoff; drives the Rejection; Purifier/Symbiote build axis (B-22 closed) | Author-approved |
| 8 | Added attribute, respec, combat-formula, pipeline, ailments, economy, meta, UI/UX | Audit gaps G-01→G-15 |
| 9 | Flagged B-01 aggregate defect, B-18 orphan types, and the open questions Q-01→Q-09 | Audit |
| 10 | **Act × Level × Points map** authored — level bands shrink with Act depth (`14/12/11/10/9/8/5`); quest points front-load (`6/5/5/4/4/3/3`), all in-campaign (§12.1.3); tree completes at Lv 100 → Vigil Power handoff (C-05 / B-13 closed) | Author ruling |
| 11 | **Mastery parity** defined — trees exceed any budget (~150 nodes / ~200 TP, never completed); **depth gating** (Tier 1–4 at 0/20/50/100) makes Dual reach 2 Keystones and Single reach the Empowered-only Tier-4 Apex + exclusive capstones; axis = breadth vs depth (§5.2/§5.3); fusion parity stated (C-06 closed) | Author ruling |
| 12 | **Fusion matrix** closed — open matrix (~1,128 abilities) replaced by a **curated exact table**; C-06 parity forces a **floor of 21** (15 class pairs + 6 apexes) with a **coverage validator** and equal `power_budget` (§5.3) | Author ruling |
| 13 | **Vigil point accounting** corrected — nodes validated (`15 + 210 + 50 = 275`), `42` proven to be the error (Rank-200 soft cap forces the node spend); faucet ratified as **1 Vigil Point per level past 100**; example corrected to `characterLevel: 375, totalVigilPointsEarned: 275` (§5.1, A.3) (B-01 closed / Q-07 answered) | Author ruling |
| 14 | **Damage Resolution Pipeline** authored — ordered 10-stage resolver, defense layer, crit rules, worked DoD example, Corruption as the **master difficulty scalar**; base resist cap **75%**, floor **−100%**, Radiant in the Vigil cap bonus, "All Resistances" retired (§7.2–§7.6) (G-02 specified; B-06, B-08, B-19, B-20 closed; Q-06, Q-09 answered) | Author ruling |
| 15 | **Item generation specified** — *rarity-first* ordering, canonical rarity→count→split table, T0–T10 tier ladder with `maxTier(ilvl)`, `implicits[]` + `itemLevel`/`requiredLevel` in the schema (§8.2b, §8.3, §8.5, §7.1) (R2 resolved; B-02, B-03, B-10, B-11, B-12 closed; Q-01…Q-04 answered) | Author ruling |
| 16 | **Damage taxonomy expanded to six types** — adds **`Umbral`** (corruption/void), the antonym of `Radiant` (cleansing/Beacon); Elemental ≡ {Fire, Lightning, Ice}, Radiant & Umbral ∉ Elemental. Adds the **conversion channel** (skill-tree node + glyph) and the **class-coverage rule** (≥3 damage types per class). Resistances now **five** (incl. Umbral); Vigil resist-cap covers all five; pipeline type order + ailment table updated (§7.1, §7.2, §7.4, §7.5) (B-18 closed) | Author ruling |
| 17 | **§5 relic-favor copy corrected** — the printed `+3% All Resistances (+8% Fire/Radiant)` superseded by `+3% Fire/Lightning/Ice Resistance (+8% Fire, +5% Radiant)`; Radiant = **5%**, "All Resistances" scope retired; copy-only, model unchanged (§10.1) (B-15 closed) | Author ruling |
