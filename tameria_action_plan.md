# Tameria — The First Beacon
## Concept Refinement & Expansion Action Plan

**Source analyzed:** `tameria_project_specifications.md` (v1 — Technical Specification & System Architecture)
**Analysis date:** 2026-11-06
**Revision:** **v1.18** — **Relic activation & Sieve continuity ratified (closes B-04, B-17; answers Q-05).** New **Appendix N**: relic favor is **live on pickup** (each relic self-activates the act it is recovered — Aegis Act 2, Hearth Act 3, Astral Key Act 5; the full total is assembled by **Act 5**), and the source's "(Act 7+)" label is re-scoped to the *Sieve's operation*, not activation — so socketing at the Act 7 climax is a **numeric no-op**. Across the Rejection the **Sieve Mirror** (portable focus) carries the relics' favor to the Ward, so the total is **continuous** with no post-campaign power drop. (v1.17 corrected the §5 relic-favor copy, B-15; v1.16 expanded the taxonomy to six types + closed B-18; v1.15 specified the item generator, App. M + closed B-02/B-03/B-10/B-11/B-12, Q-01…Q-04; v1.14 authored the Combat Charter, App. L + closed B-06/B-08/B-19/B-20, Q-06/Q-09; v1.13 closed B-01; v1.12 C-08; v1.11 C-06; v1.10 C-05 + B-13.)
**Scope:** Full review of speculative content, conflict/gap mapping, targeted design feedback, feasibility assessment, prioritized roadmap, balancing, narrative tie-ins, and ARPG-standard QC.

> **How to read this document:** Existing spec content is referenced by section (e.g. §3.1). Findings are tagged `C-xx` (register item), `G-xx` (gap), `B-xx` (new finding, v1.1), `Q-xx` (open question), `F-xx` (proposed feature). Each register item is now **typed** as Conflict / Ambiguity / Gap / Design risk / Underdevelopment. All numbers outside of direct spec quotes are **proposals** and require design sign-off.

---

## 0. Executive Summary

The v1 document is a **strong meta-systems blueprint** with a genuinely novel hook (a 7-Act campaign that culminates in the player being *permanently expelled from the paradise they saved*), and its internal math is unusually clean — the Vigil Power **per-point** math in §7.3 reconciles exactly against the rules in §2.1 (see §1.3), and the one aggregate point-accounting defect in that block (**B-01**) is now **closed** (Appendix K). It is strongest where most ARPG pitches are weakest: item variance, affix allocation, and post-cap progression.

It is weakest where ARPGs live or die: **moment-to-moment combat, enemy design, item generation/valuation, economy, hubs, quests, persistence, and multiplayer/season model are absent entirely.** Roughly 40% of a shippable ARPG's surface is specified; the other 60% is silence.

Three headline risks:

| # | Risk | Impact |
| :-- | :--- | :--- |
| R1 | **No combat math or defense layer exists** (§ missing). Itemization is defined in a vacuum — affixes roll into a system with no formula to consume them. | Critical — blocks prototyping |
| R2 | **Double-variance loot** (affix *tier* + *grade multiplier* + rarity overlay on uniques) may produce unusable "brick" items and unbalance the economy from day one. | High — affects retention |
| R3 | **Combinatorial progression explosion**: 6 classes × dual/single mastery × 4 layers × fusion × glyphs × 130-node web is a very large design/QA surface for an unproven team. | High — scope risk |

**Recommended immediate action:** freeze itemization scope at its current stage, and pivot the next design block entirely to **Combat & Encounter Fundamentals** plus a **Hub/Economy/Persistence spine**, before any content authoring begins. See the roadmap in §5.

---

## 1. Full Review & Analysis of Speculative Content

### 1.1 Idea Inventory (what the document actually commits to)

| System | Specified content | Section |
| :--- | :--- | :--- |
| Narrative frame | Dark fantasy; mutating anomaly "The Calamity"; 7-Act linear campaign Lv 1–70; Corruption % per Act | §1.1 |
| Endgame pivot | World Sieve purges Tameria Island to 0%; Hero rejected → Outer Ward → Rift endgame Lv 70–100+ | §1.1 |
| Progression (4 layers) | Global passive web (130 pts) → Class talents → Mastery+Fusion → Skill mini-trees+Glyphs | §2 |
| Post-cap | Soft cap 100; infinite levels; Vigil Power matrix (hard-capped + uncapped nodes, soft-cap rank 200) | §2.1 |
| Classes | 6 archetypes named (Warrior, Rogue, Sorcerer, Vanguard, Sage, Artificer); dual vs single mastery | §2.2 |
| Skills | Fusion skill examples only (Whirlwind+Chain Lightning; Leap Slam+Earthquake) | §2.3 |
| Items | 6 rarities, 3 Pre/3 Suf cap, affix tiers 0–10, uniques as fixed mechanics | §3 |
| Sockets | Gear sockets (Crystals/Runes) vs skill-tree sockets (Glyphs) | §3.4 |
| Quality grades | F–S (Legendary), B–SSS (Mythic); global multiplier; risk-based forging | §4 |
| Relics | 3 campaign relics with summed "World Sieve Favor" | §5 |
| Endgame | Rift keystones T1–100+, Cleansing Meter, Apex Rift Guardian, loot weighting | §6 |
| Data schemas | Item, Skill/Glyph, Vigil JSON models | §7 |

### 1.2 Coverage Heat Map

| Domain | Status | Notes |
| :--- | :--- | :--- |
| Loot structure / rarity rules | **Mature** | Best-developed area; **generator order now specified (v1.15, App. M)** |
| Post-cap progression math | **Mature (defect fixed)** | Per-point conversion correct; the aggregate point-accounting defect (**B-01**) is now **CLOSED (v1.13)** — see Appendix K |
| Narrative premise & twist | **Thin-but-strong** | Great hook, no characters/quests |
| Progression meta-structure | **Thin** | Layers named, contents undefined |
| Classes | **Skeleton** | Names only, zero kit/identity |
| Combat mechanics | **Specified (Proposed)** | Resolver + defense layer + crit + ailments now authored — **Appendix L** (G-02); pending sign-off |
| Enemies / bosses | **Absent** | Only "Apex Rift Guardian" is named |
| Item generation & economy | **Partial** | **Generation order, rarity→split table and tier ladder specified (App. M, v1.15)**; base-type catalog, absolute drop rates and currency still absent |
| Hub / town / NPCs | **Absent** | — |
| Quests | **Absent** | Side quests referenced (§2.1) but undefined |
| Persistence / save / stash | **Absent** | Critical for a loot game |
| Multiplayer / seasons / trade | **Absent** | — |
| UI/UX / accessibility | **Absent** | — |
| Performance / tech targets | **Absent** | — |

### 1.3 Cross-System Consistency Audit

**Confirmed consistent (no action):**

- §2.1 point budget: `1 (Lv1) + 99 (Lv2–100) + 30 (side quests) = 130` ✔
- §5 relic totals: the per-relic values sum exactly to the "Total World Sieve Favor" block, including `+3% All Res + 5% Fire/Radiant = +8% Fire/Radiant` ✔
- §3.1 grade eligibility (only Legendary/Mythic) matches §4.1 exclusivity ✔
- §7.1 grade application: every worked `finalValue` = `baseValue × 1.10` (Grade A), confirming §4.1's multiplier is applied per-affix ✔

**Verified working (per-value math only):**

The §7.3 `conquest_primary_stat` example proves the *per-point* soft-cap conversion is coherent: `200 pts × 0.5 = 100`, then `10 pts × 0.5 × 0.5 = 2.5` → **102.5** = the documented `currentBonus`. Likewise `resiliency_max_health` (50 × 2 = 100) and `conquest_crit_chance` (30 pts × 0.1% = 3% = the §2.1 hard cap).

**Defect found in v1.1 — now CLOSED (v1.13, Appendix K):** the *per-value* math is correct, but the *aggregate* point accounting in the **same** JSON block was not — `totalVigilPointsEarned: 42` could not fund the `15 + 210 + 50 = 275` node points shown. Resolution: the three nodes are provably correct and cannot shrink (§2.1's Rank-200 soft cap forces ≥200 points in `conquest_primary_stat`), so the **`42` was the error**; the faucet is ratified as **1 Vigil Point per level past 100**, making the earned total equal the allocated total (`275`). The corrected example is `characterLevel: 375, totalVigilPointsEarned: 275`. The per-point math remains verified and self-consistent.

### 1.4 Gap Register (systems missing entirely)

| ID | Gap | Why it is critical |
| :--- | :--- | :--- |
| G-01 | Attribute/primary-stat definitions | "Primary Stat" is referenced everywhere (§2.1, §7.3) but never defined |
| G-02 | Damage & defense formulas, hit/crit, armor DR | Affixes cannot be balanced without them |
| G-03 | Damage-type taxonomy | "Elemental," "Fire," "Radiant," "Calamity" used inconsistently (§3, §5) |
| G-04 | Ailments / status effects / CC | Core ARPG combat depth |
| G-05 | Enemy & boss design, elite affixes | No bestiary, no AI, no encounter design |
| G-06 | Item base types, implicits, item level, drop tables | **PARTIAL (v1.15):** generative model specified (**App. M** — order, rarity→split, tier ladder, `implicits[]`); **base-type catalog + absolute drop rates** remain |
| G-07 | Crafting currency ladder (beyond Catalysts) | Economy cannot function on one currency |
| G-08 | Hub/town, vendors, stash, waypoints | The Act 7 pivot removes any sanctuary and supplies no replacement |
| G-09 | Quest/side-quest framework & reward rules | §2.1 sources 30 points from "side quests" that do not exist |
| G-10 | Respec rules (passive/talent/skill) | #1 player-agency lever in ARPGs |
| G-11 | Save/persistence, item DB versioning | A loot game with no persistence spec is unshippable |
| G-12 | Multiplayer / seasons / trade / SSF model | Defines long-term retention & economy |
| G-13 | Difficulty modes (campaign difficulty, Hardcore) | No risk/reward framing for hardcore players |
| G-14 | UI/UX, loot filter, controller & accessibility | Modern-standard requirement |
| G-15 | Performance targets & world tech (isometric streaming) | Feasibility depends on it |

---

## 2. Conflict, Ambiguity & Risk Register *(revised v1.1)*

> **Typed.** Each item is classified as one of: **Conflict** = the document contradicts itself and cannot be implemented as written. **Ambiguity** = two or more valid readings, all implementable. **Gap** = information absent. **Design risk** = implementable but likely to harm the player experience. **Underdevelopment** = directionally sound but too thin to build.

### 2.1 Typed Register (with v1.0 correction log)

| ID | Item | Type | Location | v1.0 treatment | Corrected treatment |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **C-01** | Epic 4-affix skew | **RETRACTED — reviewer error** | §3.1 | Claimed the rule was mathematically impossible | **Withdrawn.** The rule is 3P+1S / 1P+3S — legal under the 3/3 cap. Corrected classification in §2.2. |
| **C-02** | Unique "fixed" vs rarity-scaled rolls | **RESOLVED (author ruling, v1.4)** | §3.3 | Called a contradiction; re-typed Ambiguity in v1.1 | **Closed.** "Fixed" qualifies affix **selection**, not values: a unique's affix *identity* is locked (it cannot roll a different affix), while its *value* rolls within a defined range. Formal rule in **§2.2.1**. |
| **C-03** | Grade F = 80% floor / downgrade-on-craft | **CLOSED (author-approved, v1.6)** | §4.1, §4.2 | Claimed "Legendary worse than an Uncommon" | **Over-claimed** (ignored affix count 5–6 vs 1–2 and tier pool T5–T10 vs T0–T10). Resolution: brick risk is **kept by design** (genre-core, cf. PoE) and made safe via the **two-anvil structure** (Purified/Calamity) + **mitigation ladder** (**Appendix E**). F↔B floor asymmetry **confirmed intentional**. **B-07** closed. |
| C-04 | Act 7 "20% Breach" | **CLOSED (author definition, v1.7)** | §1.1 | Called a corruption inversion | Was a **Gap**, not an inversion. **Closed:** **Breach** = the % of Calamity corruption that has physically penetrated the island **barrier** before the Sieve activates (`0.0–100.0%`; Act 7 starts at `20.0%`, reduced to `0.0%` by relic activation → World Sieve purge). Formal spec + schema in **Appendix F**. **B-05** closed; **B-21** logged; **B-06** remains open. |
| C-05 | Campaign (≤70) vs tree (≤100) | **CLOSED (author-approved, v1.10)** | §1.1, §2.1 | Called a conflict | **Not a conflict** — points legitimately span campaign + endgame, and Act side quests occur *during* the campaign. **Closed:** the missing **Act × Level × Points map** (**B-13**) is now authored — **level bands shrink as the campaign deepens** (14/12/11/10/9/8/5 = 69) and **quest points front-load** (6/5/5/4/4/3/3 = 30), all **30 quest points in-campaign**. Full map in **Appendix H**. |
| C-06 | Dual vs Single mastery parity | **CLOSED (author-approved, v1.11)** | §2.2 | Called a conflict | Both paths award **2 point-units**, but the *distribution* differs: Dual = `P` into each of 2 trees (independent pools); Single = `2P` into 1 Empowered tree. Because a tree (**~150 nodes / ~200 TP**) is **never completed**, depth is the true differentiator: **Dual reaches Tier-3 Keystones ×2; Single reaches the Tier-4 Apex + Empowered-exclusive capstones**. Parity model + depth gates + schema in **Appendix I**. **B-23** and **Q-10** logged. |
| C-07 | "Elemental" vs "Radiant" | **RESOLVED (author ruling, v1.3)** | §5, §3, §2.4 | Called a "confirmed conflict" | **Closed.** Radiant is a first-class damage type and **not** elemental; Elemental ≡ {Fire, Lightning, Ice}. Formal definition in **Appendix B**. Its resolution immediately exposed three new items — **B-18**, **B-19**, **B-20**. |
| C-08 | Fusion-skill matrix size | **CLOSED (author-approved, v1.12)** | §2.3 | Called a conflict | Not a conflict; **scope risk only**. **Closed:** the open matrix (≈`15S² + 3S(S−1)` → ~1,128 abilities at S=8) is replaced by a **curated exact table**. The C-06 parity constraint (**App. I.6**) sets a hard **floor of 21** — **15 class-pair recipes + 6 single-class apexes**. Full spec in **Appendix J**. **B-24** / **Q-11** logged. |

### 2.2 Corrected Item Affix Classification (author-confirmed)

**The rule (Epic-exclusive):** an **Epic** item with **4 affixes** may use *only two* splits — **3 Prefixes + 1 Suffix** or **1 Prefix + 3 Suffixes**. A **2P + 2S** split is *never* Epic, because a 2/2 item is **definitionally Rare**. The "3 Prefixes OR 3 Suffixes" clause applies **exclusively to Epic**; the Rare row of §3.1 uses "mixed", not "skewed", for its 3–4-affix items.

**Resulting legal matrix:**

| Rarity | Affix count | Legal splits |
| :--- | :--- | :--- |
| Rare | 2 | 2P+0S or 0P+2S ("skewed") |
| Rare | 3–4 | mixed (2P+1S, 1P+2S, 2P+2S) |
| Epic | 3 | 3P+0S or 0P+3S ("skewed") |
| Epic | 4 | **3P+1S or 1P+3S** |
| Epic | 5–6 | mixed |
| Legendary | 5–6 | mixed ("standard high-tier mix") |
| Mythic | 6 | fixed 3P+3S |

**Assessment:** the revised rule set is internally coherent and elegant — **Rare = balanced, Epic = skewed**, with the 2/2 split as the exact boundary between them. No remaining conflict. One generation-ordering question remains (**Q-03**).

### 2.2.1 Unique Item Roll Semantics (author-confirmed, v1.4)

**The rule:** for a **Unique** item, "fixed" qualifies **affix selection**, not **affix value**:

```text
FIXED    → the affix IDENTITY.  A unique defined to carry "Fire Resistance 30–60"
           can ONLY roll Fire Resistance for that slot — never a different affix.
ROLLED   → its VALUE.           The magnitude rolls within the unique's defined
           range (e.g. 30–60).  Rarity widens/shifts that range (§3.3 "expand
           numerical roll ranges"); the grade multiplier (§4.1) then applies on top.
```

**Consequences:**
- A unique is **deterministic in shape, variable in magnitude** — a "good roll" chase exists, but never a "wrong affix" outcome.
- Uniques still carry **no random affix identity** (the source's "No Random Affixes" clause holds).
- The generator needs, per unique: a locked affix list `[ {stat, minByRarity, maxByRarity} ]`, plus `gatedAffixes[]` unlocked by drop rarity.

**Still open:** the *ordering* question **Q-03** (is rarity rolled before value-range selection?) and the missing per-tier/baseline value tables (**B-03**). Neither blocks this rule.

### 2.3 Errata — Reviewer Misreadings (v1.0 → v1.1)

Disclosed in full so the register can be trusted:

| ID | v1.0 claim | What was wrong |
| :--- | :--- | :--- |
| A-01 | C-01 "impossible skew rule" | Read "(3 Prefixes OR 3 Suffixes)" as a *total purity* requirement instead of "*at least* 3 on one side within a 4-affix item". **Withdrawn.** |
| A-02 | C-03 "Legendary worse than Uncommon" | Compared a multiplier in isolation, ignoring that Legendary carries 5–6 affixes from T5–T10 vs Uncommon's 1–2 from T0–T10. **Unsupported.** |
| A-03 | C-04 "corruption inversion 95%→20%" | Collapsed "Corruption" and "Breach" into a single metric; the doc uses different words. **Withdrawn.** |
| A-04 | C-05 "side quests unreachable post-Act-7" | Side quests occur *during* the campaign; nothing makes them unreachable. **Unsupported.** |
| A-05 | C-06 and C-08 labelled "conflicts" | Both are design risks / underdevelopment, not contradictions. **Retyped.** |
| A-06 | §1.3 "§7.3 reconciles against §2.1 exactly ✔" | True for the *per-point conversion* only; the aggregate contradicts itself (**B-01**). **Corrected.** |
| A-07 | §6.3 "Vampiric Taint already named as an elite affix in §6.1" | §6.1 names it as a **rift modifier**, not an elite affix. Conflation. |
| A-08 | §3.2 "base resistance cap 75%" | Presented as if from the doc; the **base cap is not in the document** (only the Vigil "+2% Max Resist Cap" is). Assumption stated too firmly. |

### 2.4 Additional Inconsistencies & Unclear Points Not Flagged in v1.0

| ID | Issue | Location | Impact |
| :--- | :--- | :--- | :--- |
| **B-01** | **Vigil point accounting contradicts itself.** `totalVigilPointsEarned: 42` (Lv 142 − 100) but the three nodes allocate `15 + 210 + 50 = 275` points. | §7.3 | **CLOSED (v1.13)** — `42` was the error, not the nodes. Ratified fix: **1 Vigil Point per level past 100**, earned total = allocated total. Corrected example → `characterLevel: 375, totalVigilPointsEarned: 275`. See **Appendix K**; **Q-07** answered. |
| B-02 | **Affix schema omits implicits**, even though §4.1 says the grade multiplies "implicits". No `implicit` field exists in §7.1. | §4.1 vs §7.1 | **CLOSED (v1.15):** `implicits[]` added to the schema; grade multiplier applies. See **Appendix M.5/M.7**. |
| B-03 | **No `itemLevel` / `requiredLevel` / affix `min`–`max` range / tier table** in the item schema; §3.2 promises T0–T10 but no values exist. | §3.2, §7.1 | **CLOSED (v1.15):** shared **tier ladder** + per-stat anchor, `maxTier(ilvl)`, `requiredLevel = ilvl − 4`. See **Appendix M.4/M.5**. |
| B-04 | **Relic activation timing unclear.** Relics are recovered in Acts 2/3/5, but the favor block is labelled "(Act 7+)" and §5 says they are "socketed into the World Sieve". Unclear whether favor is live on pickup or only after socketing. | §5, §1.1 | **CLOSED (v1.18):** favor is **live on pickup** — each relic self-activates the act it is recovered (Aegis 2 / Hearth 3 / Astral Key 5). "(Act 7+)" re-scopes to the *Sieve's operation*, so socketing is a numeric no-op. See **App. N / Q-05**. |
| B-05 | **"Breach" is never defined** (Act 7 "20% Breach"). | §1.1 | **CLOSED (v1.7)** — defined by author as a zone-level **barrier-penetration** metric (0–100%); see **Appendix F**. |
| B-06 | **Corruption % has no stated mechanical effect** — 10/25/45/60/75/95 are labels only. | §1.1 | **CLOSED (v1.14):** Corruption formalised as the campaign's **master difficulty scalar** — drives enemy HP/damage/ailment-chance/rare-pack density, and yields **item rarity** (two-sided). See **Appendix L.7**; **Q-06** answered. |
| B-07 | **Grade-cap behaviour undefined** — §4.2 defines Success/Neutral/Failure but not what happens on Success at max grade (S / SSS). | §4.2 | Low — **CLOSED (v1.5):** at the cap a Success roll is a **no-op** (materials not consumed); at the floor a Failure is likewise a no-op. See **Appendix E.5**. |
| B-08 | **Crit scope unclear** — a T10 affix grants 8% crit (§7.1) while Vigil hard-caps crit at +3% (§2.1). Different scopes, but no stated global crit cap. | §2.1, §7.1 | **CLOSED (v1.14):** different scopes — Vigil **+3%** is a *node-track* cap; proposed **global character crit cap 60%**. See **Appendix L.5**. |
| B-09 | **Number of skill specialization slots undefined** (§2.4 "slot active skills"). | §2.4 | Medium |
| B-10 | **Rarity↔affix-count determination order undefined.** Rarity ranges overlap (Uncommon 1–2, Rare 2–4, Epic 3–6), so a 2- or 3-affix item is ambiguous between tiers. | §3.1 | **CLOSED (v1.15):** **rarity-first** — rarity is authoritative and the count is derived, never inferred. See **Appendix M.2**. |
| B-11 | **Legendary 5–6 split rules absent** — Rare/Epic have explicit split constraints; Legendary only says "standard high-tier mix". | §3.1 | **CLOSED (v1.15):** 5 ⇒ `3P+2S`/`2P+3S`; 6 ⇒ `3P+3S`. See **Appendix M.3**. |
| B-12 | **Uncommon vs Rare 2-affix overlap** — a 2-affix item fits both Uncommon (1–2) and Rare (2-affix skewed). | §3.1 | **CLOSED (v1.15):** `1P+1S` = Uncommon; `2P+0S`/`0P+2S` = Rare. See **Appendix M.3**. |
| B-13 | **No Act × Level × Points map** — the 99 level points + 30 quest points are not distributed across the 7 Acts / 70 campaign levels. | §1.1, §2.1 | High — **CLOSED (v1.10):** full **Act × Level × Points** distribution authored in **Appendix H**. |
| B-14 | **"points" vs "Rank" terminology drift** — §2.1 says "Past **Rank** 200"; §7.3 uses `points` and `softCapRank`. | §2.1, §7.3 | Low |
| B-15 | **CONFIRMED (v1.3):** the §5 total mis-states Radiant — it prints `+8% Fire/Radiant`, but under the author's ruling Fire = 8% and **Radiant = 5%**. | §5 | **CLOSED (v1.17):** corrected copy adopted — `+3% Fire/Lightning/Ice Resistance (+8% Fire, +5% Radiant)`; the undefined "All Resistances" scope is retired (B-19). Applied in GDD §10.1 and **App. B.5**. |
| B-16 | **`maxPoints` semantics inconsistent** — the hard-capped node carries `maxPoints: 30`; uncapped nodes carry none. | §7.3 | Low |
| B-17 | **Sieve-favor ↔ Outer Ward relationship unstated** — the World Sieve sits on the now-inaccessible island, yet the endgame operates from the Ward. | §1.1, §5 | **CLOSED (v1.18):** the **Sieve Mirror** (portable focus) channels the socketed relics' favor to the hero at the Ward — favor is **continuous** across the Rejection; no post-campaign power drop. See **App. N**. |
| **B-18** | **Orphan damage types (v1.3):** Lightning, Ice and Radiant have **zero damage sources** anywhere in the spec — no affix, skill, enemy or item produces them. Only Fire and Physical are sourced. | §3, §6, §7 | **CLOSED (v1.16):** taxonomy expanded to **six** types (adds **Umbral**); sources are guaranteed by the **class-coverage rule** (≥3 damage types per class) plus the **conversion channel** (tree node + glyph). See **Appendix B v2.0**. |
| **B-19** | **"All Resistances" scope undefined (v1.3):** the §5 total uses a scope that matches no defined grouping (the Aegis says "All **Elemental**"). | §5 | **CLOSED (v1.14):** term **retired**; the only legal collective scope is **"All Elemental Resistance(s)"** ≡ Fire + Lightning + Ice. See **Appendix L.4**. |
| **B-20** | **Vigil "Max Resist Cap +2%" scope undefined (v1.3):** with 4 resistance types now defined, it is unstated whether the bonus covers Radiant. | §2.1 | **CLOSED (v1.14):** applies to the **full percentage-resistance set** (incl. Radiant — and Umbral after v1.16) → **77%** cap. See **Appendix L.4**. |
| **B-21** | **Breach underflow / double-source (v1.7):** the relic reductions sum to exactly `20.0` (5+5+10) and fully deplete the initial Act 7 value, yet the definition also credits "sub-objectives" with reducing Breach — so Breach could fall **below 0.0%**. | §1.1 (Act 7), App. F | Low |
| **B-22** | **Hero taint mechanics undefined (v1.8):** taint is now *narratively* defined (the Hero is corrupted by the campaign → drives the Rejection), but unstated: how it **accumulates**, whether it is **reducible**, whether it has **gameplay effects**, and whether a **narrative floor** guarantees rejection regardless of play. | §1.1, App. G | **CLOSED (v1.9)** — hybrid model (Act floor + exposure) ratified; mechanical/visible tradeoff ratified. See **Appendix G**. |
| **B-23** | **Absolute Talent-Point budget unstated (v1.11):** §2.2 fixes only the *ratio* (Single = 2× Dual) and never the base per-tree award, so neither path's power can be evaluated. | §2.2 | Medium — **[Proposed]** `P = 60`/tree (both paths = 120); see **Appendix I**. Pending **Q-10**. |
| **B-24** | **Actives-per-class (`S`) undefined (v1.12):** §2.4 describes slotted actives but never states how many actives a class has, so the size of *any* open fusion matrix is incomputable. | §2.3, §2.4 | Medium — moot for the **curated** table (App. J), but it still gates the class skill lists. |

### 2.5 Open Questions Requiring Author Clarification

| ID | Question | Blocks |
| :--- | :--- | :--- |
| Q-01 | ~~**Epic 3-affix**: confirm it is 3P+0S or 0P+3S (the spec's "3 & 4-affix … skewed" implies yes).~~ **ANSWERED (v1.15):** yes — `3P+0S` / `0P+3S` (**Appendix M.3**). | — *(closed)* |
| Q-02 | ~~**Rare definition**: is Rare strictly the 2P/2S (4-affix) family, or does it still include the 2-affix and 3-affix cases in the §3.1 Rare row?~~ **ANSWERED (v1.15):** the **2–4 family** — 2 ⇒ skewed, 3 ⇒ `2P+1S`/`1P+2S`, 4 ⇒ `2P+2S` (**Appendix M.3**). | — *(closed)* |
| Q-03 | ~~**Roll order**: is rarity rolled first (then affix count within range), or is affix count + split rolled first (then rarity mapped)?~~ **ANSWERED (v1.15):** **rarity first** → count → split → stat → tier → value (**Appendix M.2/M.6**). | — *(closed)* |
| Q-04 | ~~**Legendary 5–6 affixes**: any split constraints, or genuinely free "mixed"?~~ **ANSWERED (v1.15):** constrained — 5 ⇒ `3P+2S`/`2P+3S`; 6 ⇒ `3P+3S` (**Appendix M.3**). | — *(closed)* |
| Q-05 | ~~**Relic favor**: active on pickup, or only once socketed into the Sieve (Act 7)?~~ **ANSWERED (v1.18): live on pickup** — each relic self-activates the act it is recovered; socketing at Act 7 is a narrative no-op (**Appendix N**; B-04). | — *(closed)* |
| Q-06 | ~~**Corruption %**: what does each step actually change (hp / dmg / ailment chance / rare-pack odds)?~~ **ANSWERED (v1.14):** all four, plus item rarity — the master difficulty scalar (**Appendix L.7**). | — *(closed)* |
| Q-07 | ~~**Vigil points**: is a node's `points` the *Vigil Points* budget or a separate "rank" track? Reconcile 42 vs 275.~~ **ANSWERED (v1.13):** a node's `points` **is** the Vigil Points budget (there is no separate rank track — `points` and `softCapRank` measure the same accumulated total). The `42` was a stale earned-total; the fix is 1 pt/level past 100 (App. K). | — *(closed)* |
| Q-08 | ~~Is Radiant an element?~~ **ANSWERED (v1.3): Radiant is NOT elemental** — it is a first-class damage type with its own resistance stat. Elemental ≡ {Fire, Lightning, Ice}. | — *(closed)* |
| Q-09 | ~~**Base resistance cap**: the doc only grants "+2% Max Resist Cap" via Vigil — is the base 75%?~~ **ANSWERED (v1.14):** base **75%** [Proposed] → **77%** with Vigil; floor **−100%** (**Appendix L.4**). | — *(closed)* |
| Q-10 | **Talent-Point budget `P`**: §2.2 gives only the *ratio*; ratify the absolute per-tree award (proposed `P = 60`, both paths = 120) and the **depth-gate values** (App. I.3). | Mastery parity (**B-23**) |
| Q-11 | **Fusion coverage**: ratify the **21-recipe floor** (15 pairs + 6 apexes) and whether alternates are wanted beyond it (proposed cap `~27`). | Fusion table (**C-08**) |

### 2.6 Underdeveloped Concepts (exist but too thin to build)

| System | What's missing |
| :--- | :--- |
| Classes (§2.2) | No fantasy, no resource system, no signature mechanic, no skill list, no attribute bias |
| Class talent trees (§2.2) | "Unlock Active Skills at depth thresholds" — **[PARTIAL v1.11]** the **depth-gate model** (Tier 1–4, gates 0/20/50/100) and the **parity budget** are now defined (**Appendix I**); the per-class **node lists, branch structure and skill-unlock thresholds** remain to be authored. |
| Mastery tree (§2.3) | **[PARTIAL v1.12]** the **fusion table structure + 21-recipe floor** are now defined (**Appendix J**); the per-class **passive list** and the **actual 21 recipes** (names, inputs, effects) remain to be authored. |
| Skill mini-trees (§2.4) | No node taxonomy; "behavioral shifts, elemental conversions, utility" is a category, not a design |
| Glyphs (§2.4) | 4 named examples; no socket-count rules, no rarity, no acquisition |
| Cleansing Meter (§6.1) | No mob count, no time pressure, no fail state |
| Rift modifiers (§6.1) | 3 named; no full pool, no stacking rules, no reward curve per modifier |
| Precursor Relics (§5) | 3 total for a whole campaign; no drop/upgrade path |

---

## 3. Targeted Suggestions — Core Loops, Combat, Progression, World

### 3.1 Core Gameplay Loops (`F-01`)

Define the loop at three nested timescales. The spec currently defines only the outermost.

| Loop | Duration | Content | Spec status |
| :--- | :--- | :--- | :--- |
| **Moment** | 2–8 s | Kill pack → loot filter pings → pick up → next pack | **Absent** |
| **Session** | 20–40 min | Enter area/rift → clear → boss → extract loot → respec/craft → repeat | Partially implied (§6) |
| **Meta** | Season | Level → gear → refine build → push keystone tiers → ladder | **Absent** |

**Suggestion:** Adopt a **"Calamity Cleansing" moment-loop** that ties the twist to gameplay: mobs drop *Calamity Motes* (§6.1 already defines this) that visibly corrupt the ground; the player must balance *collecting* (progress) against *cleansing* (safety). This makes the Cleansing Meter a skill expression, not a bar.

### 3.2 Combat Mechanics (`F-02`, `F-03`) — **charter authored (v1.14)**

The **Combat Formula Charter** is drafted in full in **Appendix L** (ordered 10-stage resolver, defense layer, crit rules, a worked DoD walkthrough, and Corruption as the master difficulty scalar). The bullets below are the earlier summary; **Appendix L supersedes them**. Every value remains a **[Proposed]** tuning constant pending sign-off.

- **Attributes (G-01):** 4 primary stats — **Might** (melee dmg, armor), **Agility** (crit, evasion, attack speed), **Insight** (spell dmg, mana, ailment chance), **Resilience** (life, resist cap). Each of the 6 classes has a primary + secondary bias. *(§7.3 already implies "Primary Stat" scaling at +0.5/point — keep that.)*
- **Accuracy/Evasion:** `HitChance = clamp(Accuracy / (Accuracy + Evasion × k), 0.05, 1.0)`, `k` tuned per level band.
- **Armor DR:** `DR = Armor / (Armor + 10 × EnemyLevel)`, hard cap 90%; ties into Vigil "+3% Armor/DR" (§5).
- **Resistance cap:** base **75%** *(proposal — the base cap is not stated in the source, only the Vigil "+2% Max Resist Cap"; see Q-09)*, +2% via Vigil → **77% max**. Display uncapped overage.
- **Crit:** `CritChance × CritMultiplier`, base 150% multiplier; Vigil caps crit chance at +3% (§2.1).
- **Ailments (G-04):** Ignite (Fire DoT), Chill/Freeze (Cold CC), Shock (Lightning dmg-taken amp), Bleed (Physical DoT on move), Corrupt (Calamity DoT that ignores a % of resist — thematic), Radiant (Burning + debuff cleanse interaction). This directly feeds §5's "+5% Fire & Radiant Resistance" and "-10% Debuff Duration."
- **CC budget:** enforce an internal **CC-immunity ramp** on bosses (diminishing returns per application) — required or every boss becomes cheeseable.

### 3.3 Progression (`F-04`, `F-05`)

- **Respec model (G-10) — decide now:** propose **passive respec = free during campaign, paid (currency) post-campaign; skill mini-tree respec = free; class/talent = locked per character**. This is table-stakes for player trust.
- **4-Layer clarity:** the layers currently read as parallel taxes on attention. Recommend a **single "Character Sheet → Plan" UI** that shows all four layers as one budget (like PoE's tree) rather than four separate screens.
- **Fusion skills (`F-06`) — CLOSED (C-08, v1.12):** the open matrix is replaced by a **curated exact table** with a **parity-driven floor of 21** recipes — **15 class-pair fusions + 6 single-class apexes**. Full spec + coverage validator in **Appendix J**.
- **Glyphs (`F-07`):** define rarity (Common→Mythic), a socket-count rule per skill (1 at skill Lv 1, +1 per 10 levels, max 3), and a **glyph drop pool gated by Act/rift tier**.

### 3.4 World-Building (`F-08`)

- Adds a **second narrative axis** so the campaign isn't a single "corruption %" gauge: **Corruption** (environmental/taint scalar) vs **Breach** (zone barrier-penetration). **Breach now ratified (v1.7 — C-04 closed, Appendix F);** Corruption mechanics remain open (**B-06 / Q-06**).
- Formalize **The Outer Ward / The Lonely Watch** as the permanent post-Act-7 hub *early*, so its art and systems are not a surprise at 95% completion (see G-08).
- Define **The Calamity** with explicit rules: it mutates space (explains rift modifiers), it is *selective* (explains why the hero is rejected but the island is purged — see §7 narrative), and it is *precursor-adjacent* (explains the World Sieve and relics).

---

## 4. Feasibility Assessments & Streamlining

Rating scale — **Complexity**: L/M/H (engineering effort). **Design Risk**: L/M/H (balance/QA surface).

| ID | Feature | Complexity | Design Risk | Adjustment to streamline |
| :--- | :--- | :--- | :--- | :--- |
| F-02 | Combat formula charter | M | M | **Charter authored (v1.14) — Appendix L.** Ship **spreadsheet-first**; implement in GDScript only after the tuning sheet passes. Structural rules (stage order, rounding, scope rulings) need sign-off. |
| F-03 | Ailments/CC | M | H | Cap to **6 ailments, 3 CC types** at launch; expand post-launch. |
| F-04 | 130-node passive web | H | H | Author as **data Resources** with an automated graph validator (connectivity, no orphan clusters, budget check). Do not hand-place in scene. |
| F-06 | Fusion skills | M | **M** *(was H)* | **Curated table (C-08 closed).** Floor **21** = 15 class pairs + 6 apexes; enforced by a **coverage validator** (App. J.5). Parity via App. I.6. |
| F-07 | Glyph sockets | M | M | Glyphs are **stat/behavior modifiers only**, never new code paths — implement via a modifier stack. |
| — | Vigil Power matrix | M | **L** | **Keep the design.** Per-point math verified (§1.3); the aggregate point-accounting defect (**B-01**) is **fixed** (1 pt/level past 100 → earned = allocated). Data-driven. |
| — | Item rarity/affix engine | H | H | Implement **inline in-game deserialiser** (validated deserialise of §7.1 schema) so bad data fails loudly at load. |
| — | Risk-based grade forging | L | **M** *(was H)* | **Kept by design (C-03), now mitigated.** Ship the **mitigation-currency ladder** (Appendix E: Tempering/Resonant Catalysts, Seer's Lens, Warden's Sigil, Grade Anchor, Restorative Catalyst) + optional **Controlled vs Ruinous Anvil** modes. Risk stays; it becomes opt-in. Still data-driven via a `ForgeRule` table. |
| — | Rift system | M | M | Reuse one `RiftGenerator` + modifier list; ship **10 modifiers** at launch, weighted. |
| — | Unique items | M | M | Fixed identity + rarity-scaled rolls (C-02 resolution). ~30 uniques at launch. |

### 4.1 Technical Architecture Adjustments

1. **Everything data-driven.** Itemization, passive trees, skill mini-trees, glyphs, fusions, rift modifiers, relics and Vigil nodes must all be `Resource`/JSON-driven — the spec's §7 schemas are the right instinct; extend them to *every* content type, not just items.
2. **Persistence spine first (G-11).** A single `SaveManager` with **item DB versioning** (migration hooks per schema version) is required before any content is authored, because ARPGs iterate on item schemas forever.
3. **Modifier stack (F-07 dependency).** One central `StatModifier` pipeline resolves: base → implicits → affixes (tier + grade) → relics → Vigil → rift modifiers. Without this, ordering bugs will be constant.
4. **Defer multiplayer (G-12).** Build **SSF-first**, architecture-ready for multiplayer but not networked at launch. Networking an ARPG late is expensive; committing early is riskier.
5. **Performance budget (G-15).** Set a target now (e.g. 60 FPS / 200+ concurrent AI on target hardware) — isometric ARPG perf is dominated by AI count and VFX, not draw calls.

---

## 5. Prioritized Development Roadmap

### Phase 0 — Pre-Production (Design Lock)

**Exit criteria:** every open register item closed; Combat Formula Charter signed off; Act×Level×Points matrix published.

1. Close the **open register**: **C-02 → C-08** (C-01 already withdrawn), the new findings **B-01 → B-17**, and the open questions **Q-01 → Q-09** (see §2).
2. ~~Author the **Combat Formula Charter** (§3.2) and the **damage-type taxonomy** (C-07)~~ — **taxonomy closed (v1.3); charter authored (v1.14, Appendix L)** — awaiting sign-off on the structural rules.
3. ~~Publish the **progression budget matrix** (C-05)~~ — **done (v1.10, Appendix H)**; the **respec model** (G-10) remains.
4. Define the **6 class identities** (fantasy, resource, signature mechanic, attribute bias).
5. Freeze the **item schema v1** (§7.1) + **skill/glyph schema v1** (§7.2), with versioning hooks.
6. Lock the **narrative bible**: hub, NPCs, Act beats, quest framework (G-08, G-09).

### Phase 1 — Prototyping (Vertical Slice)

**Goal:** prove the *moment loop* is fun before building the meta.

1. One class, 1 area, 3 enemy types, 1 boss.
2. Implement `StatModifier` pipeline + 1 fully functional item with the §7.1 schema.
3. Implement the **Cleansing Meter** moment-loop (Motes balance) — this is the game's core novelty; validate it first.
4. Prototype **Vigil Power** UI on top of existing (verified) math.
5. Feel-test combat with the Charter numbers; iterate in the spreadsheet, not the engine.

### Phase 2 — Full Production

| Track | Content |
| :--- | :--- |
| Systems | Full affix engine, grade forging (revised), sockets, glyphs, fusion table (~21), 130-node web, 6 classes, 30 uniques, 10 rift modifiers |
| Content | 7 Acts, hub + Outer Ward, ~40 quests + side quests, bestiary (~25 enemy families), boss ladder (Act bosses + Apex Rift Guardians) |
| Meta | Season framework, ladder, SSF, difficulty modes, Hardcore |
| Polish | Loot filter, controller, accessibility, analytics, localization hooks |

### Phase 3 — Launch Readiness

Balance pass against live-metrics proxies, soak/performance testing, persistence migration drills, economy faucet/sink audit.

---

## 6. Balancing Recommendations

### 6.1 Character Classes (`F-09`)

| Class | Suggested fantasy | Resource | Signature | Attribute bias |
| :--- | :--- | :--- | :--- | :--- |
| Warrior | Duelist / raw physical | Rage (built by hits) | Whirlwind, Leap Slam | Might / Resilience |
| Rogue | Assassin / evasion | Combo points | Shadow Step, multishot | Agility |
| Sorcerer | Arcane artillery | Mana | Chain Lightning, Frost Nova | Insight |
| Vanguard | Shield bruiser / protector | Stamina | Shield Bash, Guard aura | Might / Resilience |
| Sage | Support / summoner / DoT | Focus | Ailment spread, wards | Insight / Agility |
| Artificer | Traps, constructs, elements | Charges (gadgets) | Turrets, mines, elemental infusions | Insight / Might |

**Parity rule:** each class must have ≥1 viable **melee-range** and ≥1 **ranged** archetype so no class is locked out of a fight pattern.

### 6.2 Loot System (`F-10`) — address R2 (double-variance)

The current design multiplies **three** variance sources: rarity (affix count), affix **tier**, and **grade multiplier**. This is how economies break.

- **Whiten the floor:** raise Legendary grade floor from F→**B** *or* guarantee a "reforge currency" drop on F–D (C-03).
- **Tier×Grade coupling:** consider that grade multiplies **base + implicits only**, while affix tiers handle affix variance — this halves the compounding.
- **Pity system:** after N rifts without a Mythic, escalate weighted probability (the spec's "weighted probability" language in §6.1 invites this).
- **Item filter:** mandatory (G-14). With T0–T10 × F–SSS × rarity, loot without a filter is unplayable.

### 6.3 Enemy Encounters (`F-11`)

- **Enemy families:** ~8 per Act, mixing melee packs, ranged, caster, charger, and a "Calamity-mutated" variant that interacts with the Cleansing Meter.
- **Elite affix pool:** introduce PoE-style elite modifiers (e.g. *Corrupting*, *Warding*, *Splitting*, *Volatile*). Elites are the primary difficulty lever between tiers. *(Note: the spec's "Vampiric Taint" is a **rift modifier**, not an elite affix — §6.1.)*
- **Boss ladder:** Act boss → Apex Rift Guardian (§6.1) with a **3-phase + enrage** template and CC-immunity ramp (§3.2).

### 6.4 Difficulty Curve

- Formalize **Corruption %** (§1.1) as the campaign's master difficulty scalar (enemy hp/dmg/ailment chance), and **keystone tier** (§6.1) as the endgame scalar. Two clean knobs.
- Add **campaign difficulty selection** (Normal/Cruel/Merciless-style) and **Hardcore** (G-13) for risk/reward framing.
- **Forbidden zone rule:** never let the difficulty scalar compound with untelegraphed rift modifiers to one-shot the player without visual warning (pending the existing "Hazard Damage" clarity in §5).

---

## 7. Narrative Enhancements

### 7.1 Fix the emotional core

The strongest idea in the document is the **Rejection** (§1.1): the hero saves paradise and is expelled for being tainted. That is a thesis statement, and it is currently one bullet point. **Elevate it to the campaign's spine.**

- **Foreshadow it.** Plant the taint-accumulation mechanic from Act 2 so the player *feels* the coming rejection. Make the hero's corruption track visible (visually corrupting armor/portrait).
- **Make the choice earned, not scripted.** Offer a late-Act-7 choice: *enter the sanctuary and die purified* vs *step back and become the Warden of the Ward*. The endgame (§6) should be the *consequence* of choices, not a cutscene.
- **Give the Ward a purpose.** The Lonely Watch is where the rejected heroes of previous cycles ended up — an order of exiled guardians. The player joins a lineage, not a dead-end.

### 7.2 Questlines & Lore (`F-12`, `F-13`)

| Questline | Hook | Ties to |
| :--- | :--- | :--- |
| **The Three Relics** | Each relic (§5) is recovered through a self-contained Act climax with an NPC that embodies its theme (Aegis = sacrifice, Hearth = preservation, Astral Key = passage) | §1.1, §5 |
| **The Sieve's Makers** | Precursor civilization that built the World Sieve — their fate explains why the Calamity exists | §1.1, §5 |
| **The Ward Cycle** | The order of exiled guardians on the Outer Ward and their unwritten history | §1.1, §6 |
| **Faction: Purifiers vs Symbiotes** | Post-campaign factions — purge the taint or wield it — driving rift objective variety | §6 |
| **Side-quest economy** | Formalize the 30 quest points (§2.1) as rewards from named NPC arcs, not invisible counters | §2.1 |

---

## 8. Quality Control — Modern ARPG Standards

### 8.1 Standards Checklist

| Standard | Expected by modern players | Spec status | Action |
| :--- | :--- | :--- | :--- |
| Loot filter | Yes (mandatory at this loot complexity) | ❌ Absent | Add (G-14) |
| Free/paid respec clarity | Yes | ❌ Absent | Define (G-10) |
| Endgame progression map (atlas-like) | Yes | ⚠️ Partial (§6) | Add rift atlas layer |
| Deterministic/pity crafting | Yes (post-2019 ARPG norm) | ⚠️ Risk-based only (§4.2) | **Mitigation ladder defined (v1.5)** — C-03 → Appendix E |
| Boss ladder with escalating rewards | Yes | ⚠️ Named only | Define ladder (F-11) |
| Seasonal model + ladder | Yes (for ARPG retention) | ❌ Absent | Add (G-12) |
| Controller support | Yes | ❌ Absent | Add (G-14) |
| Accessibility (colorblind, remap, text size) | Yes | ❌ Absent | Add |
| Account/character persistence & stash | Yes | ❌ Absent | Critical (G-11) |
| Trade or SSF clarity | Yes | ❌ Absent | Decide (G-12) |
| Build diversity / no single-skill metas | Yes | ⚠️ At risk (double-variance) | Balance pass (F-10) |
| Themed damage types & ailments | Yes | ⚠️ Named inconsistently | Taxonomy (C-07, F-03) |

### 8.2 Supplementary Concepts to Fill Critical Gaps

1. **Attribute system** (4 stats) — G-01.
2. **Combat Formula Charter** — G-02, G-04.
3. ~~**Damage-type taxonomy** — Physical, Fire, Cold, Lightning, Poison, Corrupt, Radiant — G-03, C-07.~~ **DONE (v1.14):** ratified taxonomy = **Physical, Fire, Lightning, Ice, Radiant, Umbral** (six types — **Umbral added v1.16** via B-18; see App. B / GDD §7.1). *(Stale list corrected in v1.15.)*
4. **Bestiary + elite affix pool + boss template** — G-05.
5. **Item base-type & implicit catalog + item level + drop tables** — G-06. *(Generator order/tables **done, App. M, v1.15**; catalog + drop rates pending.)*
6. **Crafting currency ladder** (Transmute-equiv, Alter-equiv, Chaos-equiv, Exalt-equiv, Protection, Reforge) — G-07.
7. **Hub, vendors, stash, waypoints** — G-08.
8. **Quest framework** — G-09; ~~Act×Level×Points matrix (C-05)~~ **done (App. H)**.
9. **Save/Persistence with schema versioning** — G-11.
10. **Season/SSF/trade stance** — G-12.
11. **Difficulty modes + Hardcore** — G-13.

### 8.3 Sign-off Gate

No content authoring begins until: **the open register (C-02→C-08, B-01→B-17, Q-01→Q-09) is closed**, **Combat Formula Charter approved**, **persistence spine specified**, and **Item/Skill schemas versioned**. These four are the load-bearing walls; everything else can proceed in parallel afterwards. *Status (v1.14): the charter is **authored** (Appendix L) and awaits sign-off; it is the closest of the four to done.*

---

## Appendix A — Resolved "Keep As-Is" List

These elements are strong and should be **protected from scope creep**:

- Vigil Power soft-cap **math** (§2.1) — per-point conversion verified correct (§1.3); fix only the B-01 accounting.
- Precursor Relic global-favor model (§5) — clean and thematic. Its printed total was numerically wrong under the author's Radiant ruling; the **copy is now corrected** (B-15, v1.17; B-19, v1.14), and its **activation timing + Sieve continuity are now specified** (B-04/B-17, App. N, v1.18). Fix the **copy/wording only** — the model itself is protected.
- Rarity → affix-count → prefix/suffix-split ladder (§3.1, §3.2) — now **verified sound** (see §2.2).
- Gear sockets vs skill-tree sockets separation (§3.4) — good clarity.
- The Rejection / Outer Ward endgame pivot (§1.1) — the game's best idea; expand, don't rewrite.

---

## Appendix B — Damage & Resistance System (Formal Definition, v2.0)

*Ratified from the author's rulings: **six** first-class damage types; `Radiant` is the cleansing/Beacon axis and **`Umbral`** its corruption/void antonym; "Elemental" = Fire + Lightning + Ice exclusively.*
*Note: v2.0 (v1.16) resolves **B-18**. It is **not a code audit** — this remains a specification definition.*

### B.0 What v2.0 Changes (and closes)

| Item | Question it answered | Resolution |
| :--- | :--- | :--- |
| **B-18** | Lightning/Ice/Radiant had **zero sources** | **Closed** — set expanded to **six** types (adds **Umbral**); every class must source **≥3** types (B.7); types are also **convertible** (B.6), so no enum member is dead. |
| G-03 / C-07 | "Elemental" vs "Radiant" drift | Closed (v1.3); extended here to the six-type set. |
| F-03 | Conversion mini-trees over a closed element set | **Closed** — conversion is now a first-class channel (B.6). |

### B.1 Damage-Type Enumeration (closed set — six types)

| # | Damage Type | Elemental? | Axis | Mitigated By |
| :-- | :--- | :--- | :--- | :--- |
| 1 | Physical | No | Material | Armor (DR) |
| 2 | Fire | **Yes** | Elemental | Fire Resistance |
| 3 | Lightning | **Yes** | Elemental | Lightning Resistance |
| 4 | Ice | **Yes** | Elemental | Ice Resistance |
| 5 | Radiant | **No** | **Cleansing / Beacon** | Radiant Resistance |
| 6 | **Umbral** | **No** | **Corruption / Void** | Umbral Resistance |

**The Radiant ↔ Umbral axis.** `Radiant` is the *cleansing* polarity (the World Sieve, the Beacon, the purging of Tameria Island); **`Umbral`** is its *corruption/void* opposite (the Calamity, taint, the Rejection). They are **mirror types**: both **non-Elemental**, both singled out wherever the spec speaks of "the cleansed" vs "the tainted," and neither is reachable by "All Elemental" modifiers.
> **Naming note.** "Umbral" was ratified over alternatives to read cleanly as `Umbral Damage` / `Umbral Resistance` and to avoid collision with the three existing threat scalars (Corruption, Breach, Taint).

**Non-damage channels** — must **not** be modelled as damage types:
- **Calamity** — a *foe* category (§5 "+3% Damage vs. Calamity Foes"), not a damage type.
- **Hazard** — an environmental *channel* (§5 "-10% Hazard Damage Taken"), separate from the resistance system.

### B.2 The Elemental Grouping — Formal Rule

```text
ELEMENTAL ≡ { Fire, Lightning, Ice }     // exclusive membership
Radiant   ∉  ELEMENTAL
Umbral    ∉  ELEMENTAL
Physical  ∉  ELEMENTAL
```

Any modifier worded "All Elemental Resistance(s)" resolves to **exactly Fire + Lightning + Ice** — it never touches Radiant, Umbral or Physical.

### B.3 Resistance Stats

- **Five** discrete resistance stats: **Fire, Lightning, Ice, Radiant, Umbral**; plus **Armor** for Physical. Together these are **six mitigation channels — exactly one per damage type** (Armor DR for Physical; a percentage resistance for each of the other five). *Ratified: Physical is mitigated by **Armor only** — no separate Physical Resistance stat (avoids double-dipping and stays faithful to the source's `Armor`/`ArmorPenetration`).*
- "All Elemental Resistance" is a **scope**, not a stat.
- The source's **"All Resistances"** (total line) is an **undefined scope** — **retired** (B-19); the only legal collective scope is **"All Elemental Resistance(s)"**.

### B.4 Mitigation & Caps

- Elemental + Radiant + **Umbral**: percentage reduction, capped at *base + Vigil bonus*.
  - Base cap: **75%**; with Vigil "Max Resist Cap +2%" (§2.1) → **77%**, and this applies to **all five** percentage resistances **including Radiant and Umbral** (see App. L.4 / B-20).
  - Floor: **−100%**.
- Physical: Armor DR; `DR = clamp(Armor / (Armor + 10 × EnemyLevel), 0, 0.90)` (App. L.4).

### B.5 Derived Correction to §5 (World Sieve Favor)

Unchanged by the six-type expansion — **no relic grants `Umbral` favor** (the relics are cleansing-aligned). The §5 total still misprints Radiant.

| Type | Aegis (+3% All Elemental) | Hearth (+5% Fire & Radiant) | **Derived Total** | §5 printed |
| :--- | :--- | :--- | :--- | :--- |
| Fire | +3% | +5% | **8%** | 8% ✔ |
| Lightning | +3% | — | **3%** | 3% ✔ |
| Ice | +3% | — | **3%** | 3% ✔ |
| Radiant | **0%** (not elemental) | +5% | **5%** | **8% ✘** |
| Umbral | **0%** (not elemental) | **0%** | **0%** | n/a |

**Defect (B-15):** §5's printed `+3% All Resistances (+8% Fire/Radiant)` mis-states Radiant (prints 8%, correct 5%) and uses the undefined "All Resistances" scope (B-19).
**Corrected text:** `+3% Fire/Lightning/Ice Resistance (+8% Fire, +5% Radiant)`.
**Status — CLOSED (v1.17 / B-15).** The corrected text above is the **adopted copy** (mirrored in GDD §10.1). No relic numbers change; only the wording of the aggregate total.

### B.6 Damage-Type Conversion (source of variety — the ratified "source" channel)

Damage types are not only *authored* on skills — they are **convertible**, so any type can be exercised by any build. **Two ratified channels:**

1. **Skill-tree node** (Layer 1 global web **or** Layer 4 skill mini-tree): a node that converts a stated portion of a skill's damage **from one type to another** (e.g. "100% of Physical converted to Umbral").
2. **Glyph** (Layer 4 socket): a glyph that converts a skill's damage type while socketed.

**Conversion rules (normative — mirrors App. L.3 stage 2):**
- Conversion happens at **pipeline stage 2** — **before** any increased / more / global scaling.
- It operates on the **flat base** of the source type; **`Σ converted_out ≤ 100%`** per source type (no over-conversion).
- Conversion is how the **global passive web** guarantees offensive type access to *any* build, independent of class.

### B.7 Class-Coverage Rule (ratified — closes B-18)

> **Every class must guarantee at least three (≥3) distinct damage types reachable through its skills.**

- The three may be any of the six; chosen types should reinforce each class's fantasy (e.g. an Umbral-aligned corruption caster vs. a Radiant-aligned purifier).
- This rule, plus the **conversion channel (B.6)**, is the ratified closure of **B-18**: no damage type in the enum is dead, because every class can *author* ≥3 and *convert* into the rest.
- **Enemies** mirror the taxonomy (each Act introduces foes dealing one or more of the five non-Physical types), so all five resistances have in-play relevance.

---

## Appendix C — Integration Audit (post-clarification)

### C.1 Audit Scope and Limitation (disclosure)

**No implementation exists.** A full workspace scan found **0** source files (`.gd`, `.cs`, `.tscn`, `.tres`, `.json`, `.cfg`, `.toml`, …); the only artifact present is this document. Therefore this is **not a code audit** — it is a *specification-vs-required-implementation* gap audit, and the "integration gaps" below are between the newly clarified damage system and the rest of the specification, not between code modules. There is no engine, no stat pipeline, and no data schema in the repository to test against.

### C.2 Findings Introduced or Confirmed by the Clarification

| Priority | ID | Finding | Impact on core gameplay |
| :--- | :--- | :--- | :--- |
| **P0** | **G-02** | **Damage-resolution pipeline undefined.** No ordered spec for how a damage event is computed (base → type → conversion → mitigation → resistance → ailments). Every stat just defined is inert without it. | **Total blocker** — blocks prototyping |
| **P0** | **B-18** | **Orphan damage types.** Lightning, Ice and Radiant had **zero damage sources** in the spec (no affix, skill, enemy, or item produces them). Only Fire and Physical were sourced. | **CLOSED (v1.16)** — six-type set + class-coverage (≥3) + conversion channel; App. B.6/B.7 |
| P1 | B-15 | §5 total **mis-states Radiant** (prints 8%, correct 5%). | Player-facing incorrect number |
| P1 | B-19 | **"All Resistances" scope undefined** — matches no defined grouping. | Item/relic copy + engine enum |
| P1 | B-20 | **Vigil "Max Resist Cap +2%" scope ambiguous** — covers Radiant or not? | Cap logic / build parity |
| P2 | G-04 | **Ailments per damage type undefined.** | Combat depth |
| P2 | F-03 | **Radiant conversion decision** — conversion mini-trees now have a closed element set. | Skill design |
| P2 | G-14 | **Tooltip/UX mapping** for 6 damage types + 5 resistances. | UX |

---

## Appendix D — Next Critical Problem and Immediate Steps

### D.1 The Next Critical Problem

**The damage-resolution pipeline is undefined (G-02).**

The clarification produced a clean, closed damage taxonomy — and simultaneously exposed that **nothing in the specification consumes it.** The document now says *what* damage types exist and *what* resists them, but nowhere defines *how a damage event is calculated*. Conceptually the type enums exist; there is no resolver that reads them.

### D.2 Why This Is Highest Priority

It is upstream of every other open item:

- Affix values (§7.1) cannot be balanced without mitigation formulas.
- "Armor/DR" (§5) and "Max Resist Cap +2%" (§2.1) are unenforceable without a cap formula.
- "Damage vs. Calamity Foes" (§5) has no defined multiplier stage.
- The orphan-type problem (**B-18**) was unsolvable until we knew what the pipeline needs each type to feed — now resolved via the six-type set + class-coverage + conversion (App. B.6/B.7).

### D.3 Immediate Next Steps (ordered)

1. **Ratify Appendix B** as Damage & Resistance spec **v1.0** (one-page sign-off).
2. **Author the Damage Resolution Pipeline spec (v0.1)** with these ordered stages:
   1. Source collection — base + flat + converted
   2. Type assignment & conversion (Physical / Fire / Lightning / Ice / Radiant)
   3. Global multipliers (incl. "Damage vs. Calamity")
   4. Accuracy / hit check
   5. Critical-strike roll
   6. Penetration
   7. Per-type mitigation — Armor DR (Physical) vs Resistance (others)
   8. Ailment-application roll
   9. Final damage application / death
3. ~~**Resolve B-18**~~ — **DONE (v1.16):** the taxonomy is expanded to **six** types and the "no sources" gap is closed structurally by the **class-coverage rule** (≥3 types per class) and the **conversion channel** (tree node + glyph). See **App. B.6 / B.7**.
4. ~~**Fix §5 copy** (B-15 / B-19)~~ — **DONE (v1.17):** corrected text adopted (`+3% Fire/Lightning/Ice Resistance (+8% Fire, +5% Radiant)`); supplied in B.5 / GDD §10.1.
5. **Resolve B-20** — state whether the Vigil resist-cap bonus covers Radiant.
6. **Re-run this audit** against the pipeline spec once written; it will introduce its own edge cases (penetration-vs-cap ordering, conversion + ailment interaction, immunity, over-cap handling).

### D.4 Definition of Done

The damage system is unblocked when a damage event can be fully resolved end-to-end for all six types against a target with mixed resistances and an over-cap value, and the result is **reproducible from the written spec alone** — with no code required to disambiguate intent.

---

## Appendix E — Crafting Risk, "Brick" Outcomes & Mitigation Currency (C-03 Resolution)

*Ratified from author direction (v1.5): the grade-forge "brick" risk is **retained as genre-core** and made safe via a mitigation ladder. Benchmarked against Path of Exile's crafting model.*

### E.1 Benchmark — how Path of Exile structures crafting risk

PoE does **not** make risk unstructured. It follows three rules:

1. **Destructive currency is opt-in and terminal.** A **Vaal Orb** corrupts an item with unpredictable outcomes — *nothing / an added implicit / extra sockets / a reroll* — and **corrupted items cannot be modified again**. It is, by design, "always the last step."
2. **The default crafting loop is value-preserving.** Transmutation / Alteration / Chaos / Exaltation / Divine **reroll or add**; a Divine rerolls numbers *within the tier band* but does not lower a mod's tier.
3. **A mitigation ladder exists.** **Fracturing Orbs** permanently lock one modifier; the Crafting Bench's **"Prefixes / Suffixes Cannot Be Changed"** protects a side during rerolls; **Hinekora's Lock** *previews* the result of the next currency use before it is committed.

### E.2 Design lesson & ruling

Brick risk is genre-appropriate **when (a) it is opt-in, (b) it is terminal, and (c) a mitigation ladder exists.** Tameria's §4.2 forge currently satisfies **(b) only**.

> **Ruling (author direction, v1.5): retain the risk; add the ladder.** C-03 is re-typed from *Design risk* → **Accepted (design decision)**.

### E.3 Mitigation-Currency Ladder *(proposed; addresses G-07 — applies to the **Calamity Anvil**)*

| Family | Item (proposed) | Effect | PoE analogue |
| :-- | :-- | :-- | :-- |
| **Odds-tip** | **Tempering Catalyst** | Next attempt: **Failure → Neutral** (no downgrade). One-shot. | "Cannot be changed" |
| **Odds-tip** | **Resonant Catalyst** | Next attempt: **+X% Success** chance. | Quality / lucky |
| **Preview** | **Seer's Lens** | Reveals the next forge outcome **before** committing; consumed on preview or on any modification. | Hinekora's Lock |
| **Guarantee** | **Warden's Sigil** | Next attempt: **guaranteed Success (+1)**. Rare, top-tier sink. | — (stronger than PoE) |
| **Anchor** | **Grade Anchor** | **Permanent:** the item's grade can never drop below its current value. | Fracturing Orb |
| **Recovery** | **Restorative Catalyst** | Restores the item to its **highest grade previously achieved** (one-time imprint). | Eternal Orb (legacy) |
| **High-risk** | **Ruinous Anvil** *(mode)* | Optional forge: may jump **+2** grades **or** strip the grade entirely; applies a **Calamity-Touched** flag blocking further forging. | Vaal Orb |

### E.4 Two-Anvil Structure — **APPROVED (v1.6)**

The forge splits along the game's central **Cleansed ↔ Corrupted** axis, mirroring the endgame *Purifier vs Symbiote* factions (§7.2):

| Anvil | Theme | Outcomes | Cost | Mitigation items |
| :-- | :-- | :-- | :-- | :-- |
| **The Purified Anvil** | Cleansed / Purifier | **Success / Neutral only** — no downgrade | **Higher** material cost | N/A (already safe) |
| **The Calamity Anvil** | Corrupted / Symbiote | **Success / Neutral / Failure (±1)** | Lower cost, higher ceiling | The §E.3 ladder applies here |

**Narrative tie-in:** the Purified Anvil is the sanctuary's method — *clean, slow, and costly*; the Calamity Anvil is *wielding the taint* — *fast power at the price of instability*. This is the crafting-layer expression of the same choice the Hero faces at the Rejection, and of the post-campaign Purifier/Symbiote split.

*(Optional terminal step at the Calamity Anvil: an **Overcharge** — a Vaal-analogue — that may jump **+2 grades** or **strip the grade**, applying a **Calamity-Touched** flag that blocks further forging.)*

### E.5 Edge-Case Rulings *(closes B-07)*

- **At the cap (S / SSS):** a Success roll is a **no-op**; materials are **not** consumed.
- **At the floor (F / B):** a Failure roll is a **no-op**; no underflow.
- **Grade Anchor at cap:** an anchored item simply never rolls a downgrade.

### E.6 The F↔B Floor Asymmetry — **CONFIRMED INTENTIONAL (v1.6)**

Legendary floor is **F (80%, sub-baseline)**; Mythic floor is **B (100%)**. **Author-confirmed: deliberate — *premium rarity ⇒ baseline-or-better floor*.** With the two-anvil structure the wider Legendary band is a risk the player **opts into** (Calamity Anvil) or avoids (Purified Anvil). **No change to the floor.**

### E.7 Definition of Done — **C-03 CLOSED (v1.6)**

All author decisions are made: risk retained, **two-anvil structure approved**, **floor asymmetry confirmed intentional**, **B-07 closed**. What remains is **implementation only** — author the §E.3 ladder and the two anvils into the item schema via the `ForgeRule` table (floor/cap/probabilities/protection flags).

---

## Appendix F — Breach: Zone Barrier-Penetration Metric (C-04 Resolution)

*Ratified from author definition (v1.7).*

### F.1 Definition

**Breach** = the percentage of Calamity corruption that has **physically penetrated the barrier** of Tameria Island before the World Sieve is fully activated. It is a **zone-level** metric — *not* the hero's taint (that axis is **Corruption**).

- **Type:** dynamic float, `0.0%`–`100.0%`.
- **Initial Act 7 state (`20.0%`):** an active invasion — Calamity forces have breached 20% of the perimeter defenses. Drives environment rendering (tainted ground vs. pristine marble), enemy spawn density, and active hazard spawns.

### F.2 State Machine

| Phase | Breach | Trigger |
| :-- | :-- | :-- |
| Act 7 start | `20.0%` | Zone load |
| Objective loop | ↓ dynamically | Sub-objectives + relic activation |
| Purge | `0.0%` | World Sieve fires → zone becomes 100% cleansed & impenetrable → **Hero rejected** (rejection keyed to the hero's **personal taint** — see B-06) |

**Relic reductions** (order-independent; sum = `20.0`):

| Relic | Δ Breach |
| :-- | :-- |
| Sunken Aegis | −5.0 |
| Hearth of Ignition | −5.0 |
| Astral Key | −10.0 |

Illustrative loop: `20.0 → 15.0 (Aegis) → 5.0 (Astral) → 0.0 (Hearth)`.

### F.3 Schema (author-supplied)

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

### F.4 New Finding — **B-21** (underflow / double-source)

The three relic reductions sum to **exactly `20.0`**, fully depleting the initial Act 7 value — yet §1.1 also credits "**sub-objectives**" with reducing Breach. If sub-objectives reduce it *in addition*, Breach can fall **below `0.0%`**.

**Recommended resolution:** (a) treat sub-objectives as **gating** the relic activations rather than reducing Breach independently, **and** (b) **clamp at `0.0`** unconditionally.

### F.5 Relationship to Corruption *(addressed — see Appendix G)*

**Breach** is the **zone barrier** axis; **Corruption** is the **environmental intensity** axis; **Taint** is the **Hero's** accumulated corruption. The Rejection is keyed to the Hero's taint, now formally modeled in **Appendix G** (B-22 resolved). Act Corruption's remaining open piece is its **enemy-scaling** effect (**B-06 / Q-06**).

### F.6 Definition of Done

**C-04 is closed:** the term is defined, the state machine is specified, and the schema is supplied. Remaining is implementation, plus resolving **B-21** (clamp/gating) and **B-06** (Corruption mechanics).

---

## Appendix G — Taint: The Hero's Accumulated Corruption (B-22 Resolution)

*Ratified from author direction (v1.9): **hybrid** accumulation (Act floor + exposure) and **mechanical + visible** effects.*

### G.1 Three-Axis Vocabulary

| Axis | Scope | Meaning |
| :-- | :-- | :-- |
| **Corruption** | Zone / Act | Environmental intensity (10/25/45/60/75/95%) |
| **Taint** | Hero | How corrupted the player character has become |
| **Breach** | Zone (Act 7) | Barrier penetration before the Sieve |

Causal chain: **Act Corruption → Hero Taint → Rejection (Act 7).**

### G.2 Accumulation — Hybrid Model **[Ratified]**

```text
Taint = clamp( max(ActFloor[act], Accrued), 0, 100 )

Accrued += exposure_rate(zone, act) × mitigation_multiplier × dt
```

- **ActFloor[act]** — an **unavoidable minimum** per Act. Guarantees the Rejection for *every* player.
- **Exposure** — accrues from time/distance in corrupted zones, hazard damage taken, Calamity kills, and rift exposure.
- **Mitigation** — gear / relics / resistances lower the *rate* (multiplier < 1).
- **Cleansing** — special events may reduce `Accrued` **toward** `ActFloor` but **never below it** (the floor is the story's guarantee).

**Proposed floors & threshold** *(numbers are proposals)*:

| Act | Corruption | Taint Floor |
| :-- | :-- | :-- |
| 1 | 10% | 5 |
| 2 | 25% | 15 |
| 3 | 45% | 25 |
| 4 | 60% | 35 |
| 5 | 75% | 50 |
| 6 | 95% | 65 |
| 7 | *(Breach)* | ≥ **Rejection Threshold (75)** |

### G.3 The Narrative Floor (why the story cannot be "beaten clean")

The **Rejection Threshold** `R` (proposed 75) is **≤ ActFloor[7]** by design. A maximally careful player still arrives at Act 7 tainted enough to be rejected — but their *excess taint above the floor* is the variable, and that is what the endgame build uses (**G.5**).

### G.4 Mechanical + Visible Effects — The Tradeoff **[Ratified]**

Taint is a **two-sided resource**, not a penalty. It is attuned to the **Calamity** (the player has partly become it) and repellent to the **cleansed** (hooking into the ratified damage taxonomy, **Appendix B**, where **Radiant** is the cleansed type).

| Taint band | Vs. Calamity | Vs. Cleansed | World |
| :-- | :-- | :-- | :-- |
| **0–19 Clean** | Baseline | Baseline Radiant taken | Purifier NPCs friendly |
| **20–39 Touched** | +5% damage | +5% Radiant taken | — |
| **40–59 Tainted** | +10% damage; −5% Calamity hazard dmg | +10% Radiant taken | Symbiote vendor appears |
| **60–79 Corrupted** | +15% damage | +15% Radiant taken | Ward NPCs wary |
| **80–100 Revenant** | +20% damage; Calamity allies non-hostile in rifts | +20% Radiant taken | Symbiote skill line unlocked |

*(All values are proposals.)* **Visibility:** armour/portrait corruption stages, keyed to the band — satisfying Pillar **P2** and avoiding the "purely cosmetic corruption" anti-pattern.

### G.5 Endgame Tie-In — Purifier vs Symbiote

Post-campaign (**§7.2**), the two factions become **build paths**:
- **Purifier** — scrub taint to the Act floor; maximise cleansed (Radiant) synergy.
- **Symbiote** — *lean in*; use high taint for Calamity-facing power.

This mirrors the **two-anvil** structure (Appendix E) — *Purified vs Calamity* — on the character axis.

### G.6 Schema

```json
{
  "hero_id": "player_01",
  "taint": {
    "value": 42.5,
    "act_floor": 35.0,
    "accrual_rate_modifier": 0.85,
    "band": "tainted",
    "rejection_threshold": 75.0
  },
  "taint_modifiers": {
    "damage_vs_calamity_pct": 10.0,
    "radiant_damage_taken_pct": 10.0,
    "calamity_hazard_damage_taken_pct": -5.0
  }
}
```

### G.7 Definition of Done

**B-22 is closed.** Remaining is **tuning only**: the floor curve, the exposure rates, the band thresholds, and the band-effect magnitudes above are proposals requiring a balance pass.

---

## Appendix H — Act × Level × Points Distribution (C-05 / B-13 Resolution)

*Ratified from author direction (v1.10). Closes **C-05** and **B-13**.*

### H.1 The Three Rulings

| # | Ruling | Consequence |
| :-- | :-- | :-- |
| 1 | **Fewer levels per Act as the campaign deepens** — leveling grows harder toward high levels | Level bands **shrink monotonically** from Act 1 → Act 7 |
| 2 | **Quest points front-load** — they have the highest impact early | Quest-point curve is **decreasing** (early Acts grant the most) |
| 3 | **All 30 quest points are earned in-campaign** | Nothing is deferred to the endgame (which keeps its **own exclusive systems**) |

Together these mean **power arrives early and the tail is deliberately thin** — the character is "assembled" while the player is still learning it.

### H.2 Level-Band Curve

The campaign spans **Lv 1 → 70** (**69** level-ups). Bands shrink as Act number rises, reflecting a rising XP-per-level cost:

```text
Lv per Act:   14 + 12 + 11 + 10 + 9 + 8 + 5 = 69   (strictly decreasing)
```

| Act | Level band | Levels gained | Delta |
| :-- | :-- | :-- | :-- |
| 1 | 2–15 | 14 | — |
| 2 | 16–27 | 12 | −2 |
| 3 | 28–38 | 11 | −1 |
| 4 | 39–48 | 10 | −1 |
| 5 | 49–57 | 9 | −1 |
| 6 | 58–65 | 8 | −1 |
| 7 | 66–70 | 5 | −3 |

> **Rationale.** Act 1 is the largest because it also carries onboarding; Act 7 is the shortest and sharpest because it is a single contiguous climax (Breach loop → Sieve). The final `−3` step marks the ramp into the endgame.

### H.3 Quest-Point Curve (front-loaded)

**30** quest points, distributed so early Acts carry more:

```text
Quest pts/Act:   6 + 5 + 5 + 4 + 4 + 3 + 3 = 30   (front-loaded, non-increasing)
```

| Act | Quest pts | Cumulative | Share |
| :-- | :-- | :-- | :-- |
| 1 | 6 | 6 | 20% |
| 2 | 5 | 11 | 37% |
| 3 | 5 | 16 | 53% |
| 4 | 4 | 20 | 67% |
| 5 | 4 | 24 | 80% |
| 6 | 3 | 27 | 90% |
| 7 | 3 | 30 | 100% |

> **Rationale (author intent).** The first half of the campaign yields **20 / 30 (67%)** of all quest points, so the tree's most impactful early nodes are reachable exactly when a new build most needs them. The curve is **moderate**, not cliff-edged, so mid-campaign does not starve.

### H.4 The Master Map

Level points = `1` (awarded at Lv 1) + one per level-up. Quest points per H.3.

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

### H.5 Properties (why this map is clean)

1. **Exact handoff.** The global tree reaches **130 / 130** at **Lv 100** — the very level where **Vigil Power** begins (§2.1 / §5.1). No tree points and Vigil points ever compete; the layer boundary is a clean line.
2. **Campaign = 77%.** Acts 1–7 deliver **100 / 130** points. The final **30** arrive in the endgame alongside the endgame-exclusive systems — so **nothing must be deferred** to keep the endgame from feeling empty, and **nothing is overloaded** onto it either (ruling H.1#3 is self-consistent).
3. **Front-loading is intentional and bounded.** Acts 1–3 grant **54 / 130 (42%)** of the whole tree; the rising XP curve keeps the *real-time* acquisition pace sane, but the *point count* is deliberately early-weighted per ruling H.1#2.
4. **No orphan points.** Every one of the 130 points has a defined source and an arrival Act; **B-13** is fully discharged.

### H.6 Schema

```json
{
  "progression_budget": {
    "global_tree_max_points": 130,
    "start_points": 1,
    "level_points_total": 99,
    "quest_points_total": 30
  },
  "campaign_acts": [
    { "act": 1, "region": "whispering_frontier", "level_band": [2, 15],  "levels": 14, "quest_points": 6 },
    { "act": 2, "region": "fallen_marches",      "level_band": [16, 27], "levels": 12, "quest_points": 5 },
    { "act": 3, "region": "iron_crags",          "level_band": [28, 38], "levels": 11, "quest_points": 5 },
    { "act": 4, "region": "shattered_coast",     "level_band": [39, 48], "levels": 10, "quest_points": 4 },
    { "act": 5, "region": "miasmic_voyage",      "level_band": [49, 57], "levels": 9,  "quest_points": 4 },
    { "act": 6, "region": "tempest_ring",        "level_band": [58, 65], "levels": 8,  "quest_points": 3 },
    { "act": 7, "region": "tameria_island",      "level_band": [66, 70], "levels": 5,  "quest_points": 3 }
  ],
  "endgame": {
    "region": "outer_ward",
    "level_band": [71, 100],
    "levels": 30,
    "quest_points": 0,
    "exclusive_systems": ["calamity_rifts", "vigil_power", "purifier_symbiote_faction_choice"]
  }
}
```

### H.7 Definition of Done

**C-05 and B-13 are closed.** Remaining is **tuning only**: the exact level-band splits and the quest-point curve are **proposals** and may be re-tuned against playtest pacing without reopening the finding (the *structure* — descending bands, front-loaded quests, all-in-campaign — is the ratified part).

---

## Appendix I — Dual vs Single Mastery Parity (C-06 Resolution)

*Ratified from author direction (v1.11). Closes **C-06**. Author rulings: (1) class trees are **deliberately larger than any budget** (≈150 nodes / ≈200 TP — a player *never* completes one); (2) **Single-Class gains Empowered-exclusive capstones**; (3) the parity axis is **Dual = breadth/ceiling, Single = depth/consistency**.*

### I.1 What C-06 Was

An **Underdevelopment**, not a conflict. §2.2 commits the *shape* of both paths — Dual = 2 trees with independent pools; Single = 1 Empowered tree at 2× points — but never a number, so parity was unverifiable. The author's clarification (**a tree is never completed**) reframes the problem: parity is not about whether a tree can *absorb* the points (it always can) but about the **opportunity cost of concentration**.

### I.2 The Design Fact That Resolves It

Because a tree (~200 TP / ~150 nodes) can **never** be cleared, **every point is exclusive**. A budget is therefore a *set of choices*, and the two paths differ only in how those choices are distributed:

```text
Dual   →  P  into tree A  +  P  into tree B     (independent pools; the source forbids merging them)
Single →  2P into ONE Empowered tree
```

Both award `2P`; **neither completes anything**. The only true differentiator is **depth** — and depth is exactly what reaches a tree's ultimate nodes.

### I.3 Depth Gating (the enabling mechanism)

Talent nodes sit behind **cumulative-investment gates** (points already spent in that tree). This makes the arithmetic **self-enforcing** — the paths diverge automatically, with no special-casing:

| Tier | Gate (points spent in tree) | Access | Content |
| :-- | :-- | :-- | :-- |
| **Tier 1 — Minor** | `≥ 0` | both paths | filler / stat nodes |
| **Tier 2 — Major** | `≥ 20` | both paths | notable passives |
| **Tier 3 — Keystone** | `≥ 50` | both paths | build-defining nodes |
| **Tier 4 — Apex** | `≥ 100` | **Empowered only (Single)** | ultimate + exclusive capstones |

> §2.2's **"higher cap thresholds"** (Single) is read **literally**: the Empowered tree's gates extend **past the Tier-3 cap that Dual hits**. That single sentence is the parity lever.

### I.4 Proposed Numbers

*(Numbers are proposals — see **B-23 / Q-10**.)*

`P = 60` per tree → **both paths award 120 TP**.

| Path | Trees | Points | Total | Deepest tier reached | Fusion |
| :-- | :-- | :-- | :-- | :-- | :-- |
| **Dual-Class** | 2 | `60 + 60` | **120** | **Tier 3 — Keystone ×2** | cross-class hybrid |
| **Single-Class** | 1 (Empowered) | `120` | **120** | **Tier 4 — Apex** + exclusive capstone | intra-class apex |

Result:
- **Dual** reaches **two Keystones** in **two themes** — but can *never* touch an Apex.
- **Single** reaches **one Apex** plus **1 of ~6 Empowered-exclusive capstones** — in **one theme** only.

### I.5 Parity Statement

| Condition | Check |
| :-- | :-- |
| **Budget parity** | `120 = 120` ✔ |
| **Absorption parity** | tree holds ~200 > 120, so **no point is wasted** on either path ✔ *(this is precisely why the author's "never complete a tree" ruling matters)* |
| **Value parity** *(design target)* | `1 Apex + 1 exclusive capstone` ≈ `2 Keystones + cross-theme synergy` |

**The ratified tradeoff:**

| | **Dual-Class** | **Single-Class** |
| :-- | :-- | :-- |
| Axis | **breadth** | **depth** |
| Ceiling | higher — *if* the two themes synergise | bounded, but **guaranteed** |
| Floor | lower (anti-synergy pairs, e.g. Warrior + Sorcerer) | higher (always coherent) |
| Reach | 2 × Tier-3 Keystones | Tier-4 Apex + exclusive capstone |
| Flexibility | adapts to gear drops across two themes | committed to one identity |

### I.6 Fusion Parity (§2.3)

Both paths produce one high-impact fused ability. The source already differentiates the **source** of the fusion, so parity is **equal power budget, different expression**:

- **Dual** → Class A active + Class B active → *hybrid utility* (e.g. **Storm Gale** = Whirlwind + Chain Lightning).
- **Single** → two same-class actives → *apex magnitude* (e.g. **Tectonic Cataclysm** = Leap Slam + Earthquake).

Matrix size is handled separately (**C-08**).

### I.7 Schema

```json
{
  "talent_tree": {
    "tree_id": "warrior",
    "node_count": 150,
    "nominal_capacity_points": 200,
    "depth_gates": {
      "tier_1_minor": 0,
      "tier_2_major": 20,
      "tier_3_keystone": 50,
      "tier_4_apex": 100
    }
  },
  "mastery_path": {
    "mode": "dual_class",
    "trees": ["warrior", "sorcerer"],
    "points_per_tree": 60,
    "total_points": 120,
    "deepest_tier": 3,
    "fusion_mode": "cross_class"
  },
  "mastery_path_empowered": {
    "mode": "single_class_empowered",
    "tree": "warrior_empowered",
    "points": 120,
    "total_points": 120,
    "deepest_tier": 4,
    "apex_unlocked": true,
    "exclusive_capstones": 6,
    "fusion_mode": "intra_class_apex"
  }
}
```

### I.8 New Findings & Questions

- **B-23** — the **absolute** Talent-Point budget is unstated (§2.2 gives only the 2× ratio).
- **Q-10** — ratify `P` and the depth-gate values (I.3 / I.4).

### I.9 Definition of Done

**C-06 is closed.** The **structure** (independent pools, depth gating, Empowered-only Tier 4, breadth-vs-depth axis) is ratified. Remaining is **tuning only**: `P`, node count, the gate values, and the count/power budget of the Empowered-exclusive capstones.

---

## Appendix J — Fusion-Skill Matrix: Curated Table (C-08 Resolution)

*Ratified from author direction (v1.12). Closes **C-08**. Author-approved the **curated exact table**; the C-06 parity constraint (**App. I.6**) sets the coverage floor.*

### J.1 What C-08 Was

A **Design risk** (scope / QA surface), not a conflict — already retyped from "conflict" in **A-05**. §2.3 defines fusion *semantics* and supplies 2 examples but leaves the matrix **open** ("fuses two active skills"). Read literally, that is combinatorial, and it is the direct cause of headline risk **R3**.

### J.2 The Explosion (why an open matrix is infeasible)

With **6 classes** and `S` actives per class (`S` is itself undefined — **B-24**):

| Matrix | Formula | `S=6` | `S=8` | `S=10` |
| :-- | :-- | :-- | :-- | :-- |
| Dual (Class A × Class B) | `C(6,2) × S² = 15S²` | 540 | 960 | 1,500 |
| Single (2 actives, one class) | `6 × C(S,2) = 3S(S−1)` | 90 | 168 | 270 |
| **Total** | | **630** | **1,128** | **1,770** |

~1,100 abilities to design, art, VFX, and balance at `S = 8`, each expanding the QA surface **quadratically**. Rejected.

### J.3 The Parity Constraint Sets the Floor

**App. I.6** ratifies that **both mastery paths receive a fusion at equal power budget**. That is not merely a balance note — it *forces minimum coverage*:

- A Dual player may pick **any** of the `C(6,2) = 15` class pairs → **every pair needs ≥ 1 recipe**, or some builds get no fusion while others do → **parity broken**.
- A Single player picks 1 of 6 classes → **each class needs ≥ 1 apex**.
- **Hard floor = 15 + 6 = 21 recipes.**

> The v1.1 recommendation of "~15–20" recipes was therefore **1–6 short of parity**. Corrected target: **21 minimum**, `~21–27` with optional alternates.

### J.4 The Table — 15 Dual Pairs + 6 Apexes

**Dual (15 class-pair recipes; each class appears in 5):**

| # | Dual pair | # | Dual pair | # | Dual pair |
| :-- | :-- | :-- | :-- | :-- | :-- |
| 1 | Warrior × Rogue | 6 | Rogue × Sorcerer | 11 | Sorcerer × Sage |
| 2 | **Warrior × Sorcerer** ✅ | 7 | Rogue × Vanguard | 12 | Sorcerer × Artificer |
| 3 | Warrior × Vanguard | 8 | Rogue × Sage | 13 | Vanguard × Sage |
| 4 | Warrior × Sage | 9 | Rogue × Artificer | 14 | Vanguard × Artificer |
| 5 | Warrior × Artificer | 10 | Sorcerer × Vanguard | 15 | Sage × Artificer |

**Single (6 apex recipes — one per class):** Warrior ✅, Rogue, Sorcerer, Vanguard, Sage, Artificer.

✅ = already exemplified in the source (§2.3: *Storm Gale*, *Tectonic Cataclysm*). The remaining 19 slots are **authoring work**, not design gaps.

### J.5 Coverage Validator (the QA guarantee)

A build-time rule, in the same spirit as the **F-04** passive-web validator. Fail loudly if:

1. any of the `C(n,2)` class pairs has **0** dual recipes → a legal Dual build loses its fusion;
2. any class has **0** apex recipes → a legal Single build loses its fusion;
3. any recipe's `power_budget ≠ 1.0` → **parity (App. I.6) broken**;
4. any recipe references a skill not in that class's declared active list.

Rule 3 is what keeps the curated table honest: it makes "equal power budget" a **checked invariant**, not a promise.

### J.6 Recipe Structure & Schema

```json
{
  "fusion_id": "storm_gale",
  "mode": "dual_class",
  "pair_key": "warrior+sorcerer",
  "inputs": [
    { "class": "warrior",  "skill": "whirlwind",       "tags": ["melee", "aoe", "physical"] },
    { "class": "sorcerer", "skill": "chain_lightning", "tags": ["projectile", "chaining", "lightning"] }
  ],
  "result": {
    "damage_types": ["physical", "lightning"],
    "tags": ["melee", "aoe", "chaining"],
    "power_budget": 1.0
  }
}
```

```json
{
  "fusion_id": "tectonic_cataclysm",
  "mode": "single_class_apex",
  "apex_class": "warrior",
  "inputs": [
    { "class": "warrior", "skill": "leap_slam" },
    { "class": "warrior", "skill": "earthquake" }
  ],
  "result": {
    "damage_types": ["physical"],
    "tags": ["slam", "aoe", "empowered"],
    "power_budget": 1.0
  }
}
```

Both modes resolve to `power_budget = 1.0`, which is exactly the parity statement in App. I.6.

### J.7 Rejected Alternative — Tag-Based Fusion (Option B)

Fuse by **mechanic tags** rather than exact class pairs (e.g. `{Projectile, Fire}` × `{Melee, Physical}`), yielding a small tag-combination table from which any pair derives a result. **Fewer authored recipes**, but: unintended combos, weaker per-fusion polish, and harder balance. **Not adopted** — but recorded as the **scalability fallback** if the class roster ever grows past 6 (where `C(n,2)` becomes unmanageable).

### J.8 Findings & Questions

- **B-24** — actives-per-class (`S`) is unstated; moot for the curated table, but it still gates the class skill lists.
- **Q-11** — ratify the **21-recipe floor** and whether alternates beyond it are wanted (proposed cap `~27`).

### J.9 Definition of Done

**C-08 is closed.** The **structure** (curated exact table, floor of 21 = 15 pairs + 6 apexes, coverage validator, equal `power_budget`) is ratified. Remaining is **authoring only**: the names, inputs, effects and VFX of the 19 unwritten recipes.

---

## Appendix K — Vigil Power Accounting (B-01 Resolution)

### K.1 What B-01 Was

The **§7.3 Vigil Power Matrix** worked example is a teaching block: it shows a high-level character crossing the **Rank-200 soft cap** on an uncapped node. The block is *internally contradictory*:

```json
{ "characterLevel": 142, "totalVigilPointsEarned": 42,
  "nodes": {
    "conquest_crit_chance":   { "points": 15,  "maxPoints": 30,  "currentBonus": 0.015 },
    "conquest_primary_stat":  { "points": 210, "softCapRank": 200, "currentBonus": 102.5 },
    "resiliency_max_health":  { "points": 50,  "softCapRank": 200, "currentBonus": 100 } } }
```

The three nodes spend **`15 + 210 + 50 = 275`** points, but the block declares only **`42`** earned. A character spending 275 points from a 42-point pool cannot exist. **B-01** is therefore real, not a rounding artifact.

> **Disclosure (unchanged from §1.3):** there is **no engine or code** in this project — the workspace is Markdown only. This is a **documentation/design defect**; there is no stack trace and no runtime symptom. "Symptoms" here means the example is unusable as written.

### K.2 Locating the Error — `42 = 142 − 100`

The spec pays **1 point per level** in the example: `characterLevel 142 − soft-cap 100 = 42`. That is **consistent with the doc's own arithmetic**, and it is exactly the problem — the faucet (1/level) is too small to fund the demo. So the defect is one of two things:

1. the **earned total** is wrong (too small), or
2. the **node points** are wrong (too large).

K.3 and K.4 resolve which.

### K.3 Node Audit — every `currentBonus` is correct

| Node | `points` | Type | Check | `currentBonus` | ✔ |
| :--- | ---: | :--- | :--- | :--- | :-- |
| `conquest_crit_chance` | 15 | HardCapped (`maxPoints 30`) | `15 × 0.1% = 0.15%` | `0.015` | ✔ |
| `conquest_primary_stat` | 210 | Uncapped, cap 200 | `200 × 0.5 + (210 − 200) × 0.5 × 0.5 = 100 + 2.5` | `102.5` | ✔ |
| `resiliency_max_health` | 50 | Uncapped, cap 200 | `50 × 2 = 100` | `100` | ✔ |
| **Total points** | **275** | | | | |

All three values reconcile exactly against the per-point rules in §2.1. **The nodes are not wrong.**

### K.4 Proof the Nodes Cannot Shrink — §2.1's Rank-200 Soft Cap

The *entire purpose* of the §7.3 block is to demonstrate a **soft-cap crossing**: `conquest_primary_stat` sits at rank **210**, i.e. **10 ranks past the Rank-200 soft cap** fixed in §2.1. To sit past a 200-rank cap you must have spent **at least 200 points in that single node**. Therefore:

- `conquest_primary_stat ≥ 200` — **forced by §2.1**, not a free choice.
- The other two nodes then add `15 + 50`, so the minimum viable total is `≥ 265`.

You cannot shrink the nodes to fit `42` without **deleting the example's teaching function** (the soft-cap demo) and rewriting §2.1's ratified Rank-200 rule. Both are out of scope. **⇒ The `42` is the error.**

### K.5 The Ratified Fix

**Faucet rule (author-ratified):** *Vigil Points are earned at **1 point per level past 100**; there are no additional Vigil faucets.* Therefore the invariant is:

```text
totalVigilPointsEarned  ==  characterLevel − 100
```

To fund the verified 275-point node set, the example must show a character at **Lv 375**:

```text
corrected characterLevel : 375
corrected earned         : 375 − 100 = 275  ==  15 + 210 + 50  ✔
```

**Corrected §7.3 / A.3 example:**

```json
{ "characterLevel": 375, "totalVigilPointsEarned": 275,
  "softCapRank": 200,
  "nodes": {
    "conquest_crit_chance":   { "type": "HardCapped", "points": 15,  "maxPoints": 30,  "currentBonus": 0.015 },
    "conquest_primary_stat":  { "type": "Uncapped", "points": 210, "softCapRank": 200, "currentBonus": 102.5 },
    "resiliency_max_health":  { "type": "Uncapped", "points": 50,  "softCapRank": 200, "currentBonus": 100 } },
  "pointsSpent": 275, "pointsUnspent": 0 }
```

### K.6 Why This Option (the rejected alternatives)

| Option | What it changes | Verdict |
| :--- | :--- | :--- |
| **A — 1 pt/level, bigger example (Lv 375)** *(adopted)* | Nothing except the example's level. §2.1's post-100 "exponentially scaling XP" rule is untouched; the soft-cap demo is preserved; **no new system** is introduced. | **Ratified.** This is the minimal change that makes the example true. |
| B — raise points-per-level (e.g. 2/level) | Would rescale *all* post-cap pacing and every future Vigil demo. | Rejected — collides with the intentional infinite-XP curve (§2.1). |
| C — add a second Vigil faucet (quests, rifts) | Introduces a new system to satisfy an *example*. | Rejected — over-engineering; the block only needs a truthful level. |
| D — shrink the nodes | Deletes the soft-cap demo (§2.1 Rank 200). | **Impossible** (K.4). |

The choice is **levels only**, matching the author's ruling: *"Levels only, 1 pt/level."*

### K.7 Distinct From §2.1's 130-Point Tree

Do **not** confuse two separate budgets:

- **Global Passive Tree** (§2.1): **130 points**, earned `1 (Lv 1) + 99 (Lv 2–100) + 30 (quests)`, and the tree **completes at Lv 100** (Appendix H). This is **finite** and unaffected by B-01.
- **Vigil Power Matrix** (§7.3): **infinite**, post-100 only, `1 pt/level`. B-01 is entirely within this second budget.

The two were conflated in the original `42` (a *tree-style* "levels above 100" figure in a statement about a *Vigil* budget that must equal its spend).

### K.8 Schema (per-node spend invariant)

An authoring-time validator should reject any Vigil snapshot where the spend exceeds earnings:

```json
{
  "vigil_power": {
    "characterLevel": 375,
    "earned": 275,
    "faucet": { "rule": "1_per_level_above_100", "threshold": 100 },
    "spent": 275,
    "unspent": 0,
    "invariant": "spent + unspent == earned  &&  earned == max(0, characterLevel - 100)"
  }
}
```

### K.9 Definition of Done

**B-01 is closed.** The node math is verified (K.3), the `42` is proven to be the error (K.4), and the faucet is ratified as **1 Vigil Point per level past 100** with the corrected example `characterLevel: 375, totalVigilPointsEarned: 275` (K.5). **Q-07** is answered (the node's `points` **is** the Vigil budget; there is no separate rank track). **§2.1 and its Rank-200 soft cap are untouched.** Remaining is **mirroring the correction into the GDD (§5.1 note, A.3 schema, change log)** — a transcription task, not a design decision.

---

## Appendix L — Damage Resolution Pipeline & Combat Formula Charter (G-02 / F-02 Resolution)

> **Status: [Proposed] — requires author sign-off.** This appendix is the **Combat Formula Charter**. Every numeric constant is a *tuning proposal*; every *structural* rule (ordering, clamping, rounding, scope) is what the pipeline actually needs ratified, because it is the ordering that makes the math reproducible. Develop **spreadsheet-first**; implement in GDScript only after the sheet passes tuning.

### L.1 What G-02 Was

**G-02 (Damage & defense formulas, hit/crit, armor DR)** is the **P0 blocker** and headline risk **R1**: itemization (§7.1), affixes (§3.1–§3.2) and the whole loot loop are defined **in a vacuum** — they roll values into a system that had **no formula to consume them**. §7.4 named the stage order but stopped there: no per-stage formula, no rounding rule, no clamping, no worked result. This appendix supplies them.

Two DoD statements govern:

- **§3.2:** *"a damage event resolves end-to-end for all six types against a target with mixed resistances and an over-cap value, reproducibly from the written spec alone."*
- The doc's rule that all content must be **data-driven** → the pipeline must be expressed as ordered, testable stages, not prose.

### L.2 Boundaries — What Is Already Ratified (and therefore *frozen*)

These are inputs the pipeline **must obey**; it does not re-open them.

| Frozen rule | Source |
| :--- | :--- |
| Exactly **6 damage types**: Physical, Fire, Lightning, Ice, Radiant, **Umbral** | App. B.1 / GDD §7.1 |
| **Elemental ≡ {Fire, Lightning, Ice}**; Radiant ∉ Elemental; **Umbral ∉ Elemental**; Physical ∉ Elemental | App. B.2 |
| Mitigation: **Armor (DR)** for Physical; a **resistance** for each of the other five | GDD §7.2 |
| **Grades** multiply base damage/defense, implicits, and all affix values | GDD §3.3 (grades) |
| **Vigil caps**: Crit **+3%**, Max Resist Cap **+2%**, CDR **+5%**, Move Speed **+5%** | §2.1 |
| **"Damage vs. Calamity"** is a **foe category**, not a damage type | GDD §7.1 |
| **Hazard** is an **environmental damage-taken channel**, not a resistance | GDD §7.1 |
| Three threat axes: **Corruption** (zone/Act), **Taint** (hero), **Breach** (Act 7 zone) | App. F / G |

### L.3 The Ordered Pipeline (10 stages)

> **Ordering is the design.** Moving any stage changes the result; the order below is the ratified proposal. Stages are evaluated **per damage type**, in the fixed type order `[Physical, Fire, Lightning, Ice, Radiant, Umbral]` (order matters only for conversion, stage 2).

```text
 STAGE 0  Snapshot          gather all inputs into one immutable attack record
 STAGE 1  Source collection base (per type) + added flat (per type)
 STAGE 2  Conversion        move damage between types (before any scaling)
 STAGE 3  Increased / More  additive "increased" then multiplicative "more"
 STAGE 4  Global multipliers "vs Calamity", grade, conditional global "more"
 STAGE 5  Accuracy / hit    miss -> 0 damage, no ailments
 STAGE 6  Critical strike   roll; if crit, apply CritMultiplier
 STAGE 7  Penetration       reduce target's effective resistance (this type)
 STAGE 8  Mitigation        Armor DR (Physical) or Resistance (other five)
 STAGE 9  Ailment roll      per-ailment apply (never on a miss; crits guarantee)
 STAGE 10 Application       round once, subtract life, death check
```

**Detail per stage:**

- **01 · Source collection.** For each type `t`: `flat[t] = base[t] + Σ added_flat[t]`. `base[t]` comes from the skill/weapon (already grade-scaled, L.2). `added_flat` is any "+X–Y <type> damage" affix.
- **02 · Conversion.** Apply the conversion map **once, before scaling**, and **only on `flat`**. Order: Physical → (Fire/Lightning/Ice) first, then elemental → elemental. Converted amount leaves the source type and joins the target type. Conversion fractions are **clamped so `Σ out ≤ 100%`** per source type (no double-dipping).
- **03 · Increased / More.** For each type: `dmg[t] = flat[t] × (1 + Σ increased[t]) × Π (1 + more[t])`. `increased` is **additive with itself** (all "%increased" sources summed, then applied once); `more` is **multiplicative with itself**. Passive-tree/affix "*% increased Fire Damage*" → `increased[Fire]`; support/gem "*25% more*" → `more[t]`.
- **04 · Global multipliers.** `dmg[t] ×= Π global_more`, applied uniformly to every type. This is where **"Damage vs. Calamity Foes"** enters — it is a single global stage, **not** a type. Grade multiplier (L.2) also resolves here if not already expressed in `base`.
- **05 · Accuracy / hit check.** `HitChance = clamp(Acc / (Acc + Evasion`<sub>target</sub>` × k), 0.05, 1.0)`; roll once for the whole attack. **On a miss: all types resolve to 0 and stage 9 is skipped.** `k` is a per-level-band tuning constant (proposed `k = 1.0` in-campaign). Accuracy/Evasion never affects ailment *spread* from an already-applied ailment.
- **06 · Critical strike.** `CritChance = clamp(base + Σ crit_chance, 0, crit_cap)`; roll once. `CritMultiplier = 1.50 + Σ crit_mult` (the base 1.50 is **additive** with gear crit-multi). On crit: `dmg[t] ×= CritMultiplier` for every type. See L.5 for the B-08 scope ruling.
- **07 · Penetration.** `eff_res[t] = raw_res[t] − pen[t]`. Penetration is applied **before** the cap test (L.4) and **cannot** push a target below its resistance floor.
- **08 · Mitigation.** Per type:
  - **Physical:** `applied = dmg × (1 − DR)`, with `DR = clamp(Armor / (Armor + 10 × EnemyLevel), 0, 0.90)`.
  - **Fire / Lightning / Ice / Radiant:** `applied = dmg × (1 − eff_res[t])` where `eff_res[t]` is clamped to `[−1.00, cap]` (L.4).
  - **Hazard (taken side only):** if the incoming damage is flagged `hazard`, apply `× (1 − hazard_reduction)` **after** stage 8. Hazard is a channel flag on the *damage event*, never a type.
- **09 · Ailment roll.** For each ailment whose type matches a damage type that **actually applied > 0**: roll `AilmentChance[ailment]`. A **critical hit guarantees** the crit type's matching ailment (e.g. a crit Fire hit guarantees Ignite). A miss applies nothing. Boss/CC targets resolve the **CC-immunity ramp** (GDD §7.5).
- **10 · Application.** Sum `applied` across types, **round once** (round-half-up to integer life), subtract from life, run death/on-death hooks. **No intermediate rounding anywhere.**

**Rounding & precision rule (normative):** carry `float64` through **all** stages; round **exactly once**, at stage 10. Never round between stages. Display formatting is a UI concern only.

### L.4 The Defense Layer

| Property | Proposal | Note |
| :--- | :--- | :--- |
| **Base resistance cap** (per type) | **75%** | **[Proposed]** — the source states only the Vigil "+2% Max Resist Cap" (**Q-09** answered by this proposal). |
| **Resistance floor** | **−100%** | A fully-exposed target takes at most **2×** damage; keeps debuff math bounded and legible. |
| **Vigil "+2% Max Resist Cap"** | applies to **all five** percentage resistances **including Radiant & Umbral** | **[Proposed]** — Radiant & Umbral are first-class resistances (App. B.3); the bonus is a *cap* stat, so it extends to the full resistance set (**B-20** resolved). → **77%** max with Vigil. |
| **Armor DR cap** | **90%** | Consumes Vigil "+3% Armor/DR". |
| **Over-cap values** | **displayed, not applied** | A resistance rolled above its cap is shown as overage (a chase target for builds that raise the cap via Vigil). **[Proposed] optional QoL:** over-cap reduces enemy penetration **1:1**, up to the overage. |
| **"All Resistances" scope** | **term retired** | The only permitted collective scope keyword is **"All Elemental Resistance(s)"** ≡ Fire + Lightning + Ice. Any relic/affix total must list types explicitly (**B-19** resolved). |

**Cap-test order (normative):** `eff_res = clamp(raw_res − pen, −1.00, cap)`. That is, penetration is subtracted **first**, then the result is floored at −100% and capped at the (possibly Vigil-raised) cap. This single line is what makes the over-cap DoD case resolve deterministically.

### L.5 Critical Strike — Closing B-08

**The defect:** a **T10 affix grants 8% crit** (§7.1) while the **Vigil node hard-caps crit at +3%** (§2.1) — two numbers that *look* contradictory.

**Ruling ([Proposed]):** they are **different scopes**, and the spec must name them so:

- `CritChance` (global character stat) has a proposed **global cap of 60%** — it governs the *character*, not a node.
- The **Vigil "+3%"** is a **node-track cap**: it limits *how much crit chance the Vigil node itself may contribute*. It is **not** a global ceiling and does **not** cap gear/affix crit.
- Therefore a T10 `+8% Crit` **affix** and the Vigil node's `+3%` **coexist**; total = `node(+3%) + affix(+8%) + … ≤ 60%`.

This removes the ambiguity without nerfing either system. *(Rename the §2.1 node stat to **"Crit Chance (Vigil node, max +3%)"** in authoring to prevent recurrence.)*

### L.6 Worked Walkthrough — the DoD Proof

A single damage event, resolved end-to-end with **mixed resistances** and an **over-cap** target value. All stage outputs shown.

**Attacker (Lv 70):** skill base `200 Physical`; **50% Physical → Fire**; affix `+40–40 Fire`; `+80% increased Fire`, `+30% increased Physical`; one `25% more` multiplier; foe is **Calamity** (`+3% vs Calamity`); `Acc 2,000`; `35% crit` (0% from Vigil, 35% gear), `+40% crit multi`.

**Target:** `Evasion 200` ⇒ `k=1.0`; `Armor 2,000`; `EnemyLevel 70`; **Fire raw resist 80%** (cap 75% → **over-cap**); attacker **Fire pen 15%**.

```text
STAGE 1  flat   = { Physical: 200 }
STAGE 2  convert 50% Phys -> Fire:  Physical 100,  Fire 100
         affix +40 Fire:             Fire 140
STAGE 3  Fire  ×(1+0.80) ×1.25  = 140 × 1.80 × 1.25 = 315.00
         Phys  ×(1+0.30) ×1.25  = 100 × 1.30 × 1.25 = 162.50
STAGE 4  ×1.03 (vs Calamity):    Fire 324.45, Phys 167.375
STAGE 5  HitChance = 2000/(2000+200×1.0) = 0.909  → roll: HIT
STAGE 6  Crit roll: HIT (35%).  CritMult = 1.50+0.40 = 1.90
         Fire 616.455, Phys 318.0125      (crit Fire ⇒ Ignite guaranteed)
STAGE 7  Fire pen 15%:  eff_res_raw = 0.80 - 0.15 = 0.65
STAGE 8  Fire:  clamp(0.65, -1.00, 0.75) = 0.65  -> 616.455 × 0.35 = 215.75925
         Phys:  DR = clamp(2000/(2000+10×70), 0, 0.90) = 2000/2700 = 0.740741
                318.0125 × (1-0.740741) = 82.44769
STAGE 9  Ignite applied (crit Fire).   Other ailments: none sourced.
STAGE 10 total = 215.75925 + 82.44769 = 298.20694  ->  round  = 298
```

**Result: 298 damage** (216 Fire + 82 Physical), Ignite applied. The **over-cap** value (80% raw vs 75% cap) is exercised, **penetration order** is exercised (pen before clamp), and the **armor formula** is exercised — reproducible from this appendix alone. ✔

### L.7 Corruption as the Master Difficulty Scalar — Closes B-06 / Q-06

The source prints per-Act Corruption as **labels only** (10 / 25 / 45 / 60 / 75 / 95). **B-06/Q-06 asked what each step changes.** Proposal: Corruption `c ∈ [0,1]` is the campaign's **single master difficulty scalar**, feeding the enemy side of the pipeline. Each Act's value is fixed by §1.1; the effects are affine and **zero-based at Act 1** so the curve is monotone and extensible:

```text
c = Corruption as a fraction (Act1 = 0.10)
EnemyHP     ×= 1 + (c - 0.10) × 3.00
EnemyDamage ×= 1 + (c - 0.10) × 1.60
AilmentChance ×= 1 + (c - 0.10) × 1.00
RarePackDensity ×= 1 + (c - 0.10) × 1.30
ItemRarity  += (c - 0.10) × 100      // percentage points
```

Resulting table (all values [Proposed]):

| Act | Corruption | Enemy HP × | Enemy Dmg × | Ailment × | Rare-pack × | Item Rarity |
| :-- | ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 10% | 1.00 | 1.00 | 1.00 | 1.00 | +0% |
| 2 | 25% | 1.45 | 1.24 | 1.15 | 1.20 | +15% |
| 3 | 45% | 2.05 | 1.56 | 1.35 | 1.46 | +35% |
| 4 | 60% | 2.50 | 1.80 | 1.50 | 1.65 | +50% |
| 5 | 75% | 2.95 | 2.04 | 1.65 | 1.85 | +65% |
| 6 | 95% | 3.55 | 2.36 | 1.85 | 2.11 | +85% |
| 7 | Breach axis | — | — | — | — | — |

**Why these levers:** HP + damage = the core threat curve; **ailment chance** = the *feel* of corruption (P2 "the taint you carry"); **rare-pack density** = encounter lethality; **item rarity** = the risk/reward hook that makes deep Corruption *worth* entering. Corruption is thereby a **two-sided** scalar (harder **and** more rewarding), consistent with the Taint tradeoff (App. G.4).

> **Act 7** does not use a Corruption label — its zone axis is **Breach** (App. F). The sanctuary's own corruption is purged to 0% at the climax (World Sieve).

**Levers deliberately *not* attached to Corruption** (avoid over-loading one scalar): enemy *elemental* bias, pack composition, boss modifiers — these belong to zone/rift modifiers, not to the Corruption number.

### L.8 Register Closures Accumulated by This Appendix

| ID | Was | Now |
| :--- | :--- | :--- |
| **G-02** | No damage/defense formula (P0) | **Specified** — 10-stage resolver (L.3) + defense layer (L.4) + DoD walkthrough (L.6). |
| **B-06 / Q-06** | Corruption had no mechanical effect | **Closed** — Corruption formalised as the master difficulty scalar (L.7). |
| **B-08** | Crit affix vs Vigil cap scope | **Closed** — different scopes: node-track cap (+3%) ≠ global character cap (60%); L.5. |
| **B-19** | "All Resistances" scope undefined | **Closed** — term retired; only "All Elemental Resistance(s)" is a legal scope (L.4). |
| **B-20** | Vigil "+2% Max Resist Cap" — Radiant? | **Closed** — applies to **all five** percentage resistances incl. Radiant & Umbral → 77% cap (L.4). |
| **Q-09** | Base resistance cap unspecified | **Answered** — base **75%** [Proposed] (L.4). |

**Still open after this appendix:** **B-18** (orphan damage types — *content*, not math) — **now CLOSED (v1.16)** in **App. B v2.0**; the active next items are **B-09** (skill slots), **B-14/B-16** (terminology), **B-21** (Breach clamp), **B-23/B-24** (+ Q-10/Q-11). *(**B-04/B-17** relic timing / Sieve↔Ward — **CLOSED v1.18**, App. N; **B-15** §5 Radiant misprint — **CLOSED v1.17**.)*

### L.9 Schema (resolver config + damage event)

```json
{
  "combat_constants": {
    "crit_base_multiplier": 1.50,
    "crit_global_cap": 0.60,
    "resistance_base_cap": 0.75,
    "resistance_floor": -1.00,
    "armor_dr_cap": 0.90,
    "armor_dr_const": 10,
    "accuracy_k": 1.0,
    "hit_chance_floor": 0.05,
    "rounding": "round_half_up_at_stage_10_only",
    "type_order": ["physical", "fire", "lightning", "ice", "radiant", "umbral"]
  },
  "damage_event": {
    "flat": { "physical": 200 },
    "conversion": [ { "from": "physical", "to": "fire", "fraction": 0.50 } ],
    "increased": { "fire": 0.80, "physical": 0.30 },
    "more": { "fire": 1.25, "physical": 1.25 },
    "global_more": { "vs_calamity": 1.03 },
    "penetration": { "fire": 0.15 },
    "is_hazard": false,
    "accuracy": 2000,
    "crit_chance": 0.35,
    "crit_multiplier_add": 0.40
  }
}
```

### L.10 Definition of Done & Sign-off Gate

**G-02 is specified** (not yet ratified): the resolver is ordered, every stage has a formula, rounding is normative, the defense layer is bounded, and a **damage event resolves end-to-end for all six types against a target with mixed resistances and an over-cap value** — the §3.2 DoD — from the written stages alone (L.6).

**Sign-off required on the *structural* rules** (these are design decisions, not tuning):

1. The **stage order** (L.3), in particular **penetration before the cap** (L.4) and **conversion before scaling** (stage 2).
2. The **single-rounding rule** (stage 10 only).
3. The **scope rulings**: resistance floor −100% (L.4), the **retirement of "All Resistances"** (B-19), and **Radiant inclusion** in the Vigil cap bonus (B-20).
4. **Corruption as the master scalar** (L.7) — and its **two-sided** nature.

**After sign-off:** freeze the constants into `combat_constants` (L.9), build the **spreadsheet model**, and only then implement in GDScript. **F-02 moves from "highest-priority gap" to "specified — pending tuning."**

---

## Appendix M — Item Generation Order, Rarity→Affix Table & Tier Ladder (B-02 / B-03 / B-10 / B-11 / B-12 + Q-01…Q-04)

> **Status: [Proposed] — requires author sign-off.** This is the **second load-bearing wall (R2, double-variance)**. The affixes that Appendix L now consumes have to be *generated deterministically*; this appendix is the generator's rule set.

### M.1 The Defect Cluster

| ID | Issue | Why it blocks |
| :--- | :--- | :--- |
| **B-10** | Rarity ranges **overlap** (Uncommon 1–2, Rare 2–4, Epic 3–6), so the affix count does not identify the rarity. | The generator cannot pick a rarity from a count, and the player cannot read one off the item. |
| **B-12** | A 2-affix item fits **Uncommon** *and* **Rare**. | Same root cause as B-10. |
| **Q-02** | Is **Rare** strictly the 2P/2S family, or does it include the 2- and 3-affix cases? | Rarity identity. |
| **Q-03** | **Roll order** — rarity first, or affix count first? | The generator's spine. |
| **Q-01** | Is an **Epic 3-affix** item `3P+0S` / `0P+3S`? | Split legality. |
| **Q-04** | **Legendary 5–6** split constraints. | Split legality. |
| **B-11** | **Legendary split rules absent** ("standard high-tier mix" is not a rule). | Same. |
| **B-02** | **Implicits** are referenced by §4.1's grade multiplier but absent from the §7.1 schema. | Schema incompatible with rules. |
| **B-03** | No `itemLevel` / `requiredLevel` / affix **`min`–`max` tier table**. | The generator has no values to roll. |

### M.2 The Ordering Ruling — **Rarity-First** (closes Q-03 / B-10 / B-12 / Q-02)

**The defect is an *inference* error, not a table error.** B-10 and B-12 only exist because the designer was trying to **infer rarity from the affix count**. Invert that:

> **Rarity is the authoritative, explicitly-rolled field. Affix count and prefix/suffix split are *derived* from rarity — never inferred back from them.**

```text
  roll RARITY (from drop table, modulated by Corruption's ItemRarity bonus)
        │
        ├─▶ rarity DETERMINES the legal affix-count set   (M.3)
        │        │
        │        ├─▶ pick count (weighted)
        │        │
        │        └─▶ pick split among the count's legal splits
        │
        └─▶ rarity DETERMINES the tier pool               (§3.2 / M.4)
```

**Consequences:**
- **Q-03 answered:** rarity **first**, then count, then split, then identities, then values.
- **B-10 / B-12 closed:** there is no "ambiguous 2-affix item". A 2-affix item's rarity is whatever was rolled and is **stored on the item**; the split merely follows. (Overlap between *rarity labels* for a given count is harmless once rarity is authoritative — exactly as an item's `baseRarity` field already is in §7.1.)
- **Q-02 answered:** **Rare** is the 2–4 family with the splits in M.3 — it is *not* "only 2P+2S". The **2P+2S** split is the **4-affix Rare** (and the exact boundary against Epic's 4-affix `3P+1S`).

### M.3 Canonical Rarity → Count → Split Table (closes Q-01 / Q-04 / B-11)

Derived from §3.1 + the author's §8.2 ruling (`2P+2S` is *never* Epic; Epic's 4-affix is `3P+1S`/`1P+3S`). Every legal `(count, split)` maps to exactly one rarity — **no gaps, no overlaps**.

| Rarity | Rolled count (weights) | Legal splits |
| :--- | :--- | :--- |
| **Common** | 0 (100%) | — |
| **Uncommon** | 1 (70%) · 2 (30%) | 1 → `1P+0S` / `0P+1S` · 2 → **`1P+1S`** |
| **Rare** | 2 (45%) · 3 (35%) · 4 (20%) | 2 → `2P+0S` / `0P+2S` (skewed) · 3 → `2P+1S` / `1P+2S` · 4 → **`2P+2S`** |
| **Epic** | 3 (20%) · 4 (40%) · 5 (25%) · 6 (15%) | 3 → **`3P+0S` / `0P+3S`** (skewed) · 4 → **`3P+1S` / `1P+3S`** · 5 → `3P+2S` / `2P+3S` · 6 → `3P+3S` |
| **Legendary** | 5 (55%) · 6 (45%) | 5 → `3P+2S` / `2P+3S` · 6 → `3P+3S` |
| **Mythic** | 6 (100%) | `3P+3S` (fixed) |

**Answers to the open questions:**
- **Q-01 — yes:** an Epic 3-affix item is `3P+0S` or `0P+3S` (the "3 on one side, 0 on the other" skew).
- **Q-04 / B-11 — Legendary rule:** 5 affixes ⇒ `3P+2S` or `2P+3S`; 6 affixes ⇒ `3P+3S`. **"Standard high-tier mix" is superseded by this explicit rule.**
- The discriminator is crisp: **Uncommon-2 = balanced `1P+1S`; Rare-2 = skewed `2P+0S`/`0P+2S`; Rare-4 = `2P+2S`; Epic-4 = `3P+1S`/`1P+3S`.**

> **Corroboration:** the spec's **own** §7.1 worked item is a **Legendary with `3P+2S`** (three Prefixes: T8, T10, "Legendary"; two Suffixes: T9, T10) — which is exactly the Legendary-5 rule above. The table is consistent with the document's existing example.

### M.4 Tier Value Ladder + Item-Level Gating (closes B-03)

§3.2 promises **T0–T10** but defines no values. Rather than enumerate every stat × 11 tiers, define **one ladder** and a **per-stat anchor** (data-driven, matching the "everything data-driven" rule):

```text
value(stat, T) = T10Anchor(stat) × R[T] × uniform(0.90, 1.00)

R (T0..T10) = [0.05, 0.08, 0.12, 0.17, 0.24, 0.32, 0.42, 0.55, 0.70, 0.85, 1.00]
```

`T10Anchor(stat)` is authored per stat (e.g. `FlatPhysicalDamage → 50`, `AttackSpeedPercent → 0.12`). The ladder is **strictly monotone with no overlap**: tier `T+1`'s minimum (`0.90 × R[T+1]`) always exceeds tier `T`'s maximum, because every adjacent ratio `R[T+1] / R[T] ≥ 1.17 > 1.111`.

**Item-level gating:**
```text
maxTier(ilvl) = clamp(idiv(ilvl, 6), 0, 10)      // T10 unlocks at ilvl ≥ 60
minTier(rarity) = { Uncommon/Rare/Epic: 0, Legendary: 5, Mythic: 9 }
affixTier = uniform_choice( minTier(rarity) .. maxTier(ilvl) )
```

So a **Legendary** always rolls T5–T10 and a **Mythic** T9–T10 — exactly §3.2 — while the `minTier`/`maxTier` structure keeps low-level drops from producing high tiers.

### M.5 Base Types, Implicits, `itemLevel` & `requiredLevel` (closes B-02)

- **Implicits:** each base type carries **exactly one implicit modifier** (its identity). Add an `implicits[]` array to the schema. §4.1's grade multiplier **does apply** to implicits (it says so) — so an implicit's `finalValue = value × gradeMultiplier` for Legendary/Mythic.
- **`itemLevel` (`ilvl`):** the drop's level; gates `maxTier` (M.4) and the affix pool.
- **`requiredLevel`:** `max(1, itemLevel − 4)` [Proposed] — a small grace window so a fresh drop is usually equippable.
- **Base-type catalog** per slot (sword, axe, wand, body armour, …) with its implicit and its socket capacity — authoring task, schema field reserved here.

### M.6 The Generation Algorithm

```text
1. roll RARITY      from the drop table (Corruption ItemRarity bonus shifts it — §7.6)
2. pick COUNT       weighted, from rarity's allowed counts              (M.3)
3. pick SPLIT       among the count's legal splits                       (M.3)
4. reserve SLOTS    P and S exactly as the chosen split specifies       (M.3)
5. for each affix slot:
     a. pick STAT   from the tier pool legal for the slot + rarity       (§3.2)
     b. pick TIER   in [minTier(rarity), maxTier(ilvl)]                  (M.4)
     c. roll VALUE  = T10Anchor(stat) × R[tier] × U(0.90, 1.00)          (M.4)
     d. reject duplicate stats within the item
6. attach IMPLICIT   (base identity, grade-scaled if Legendary/Mythic)    (M.5)
7. if Legendary/Mythic: roll GRADE, finalValue = value × gradeMultiplier  (§4.1/§9.1)
```

**Worked example.** Assume `ilvl 62` (⇒ `maxTier = 10`), rolled **rarity = Legendary**, `count = 5`, `split = 3P+2S`, `grade = A (1.10)`:

| Slot | Stat | Tier | `baseValue` | `finalValue` |
| :-- | :--- | --: | --: | --: |
| Prefix | PhysicalDamagePercent | 8 | 120 | **132** |
| Prefix | FlatPhysicalDamage | 10 | 50 | **55** |
| Prefix | ArmorPenetration *(Legendary affix)* | L | 0.15 | **0.165** |
| Suffix | AttackSpeedPercent | 9 | 0.12 | **0.132** |
| Suffix | CriticalStrikeChance | 10 | 0.08 | **0.088** |

This reconstructs the spec's §7.1 item **exactly** — the generator is consistent with the document's own example. (Note the T10 `CriticalStrikeChance = 0.08` is the affix referenced in **B-08**; per **Appendix L.5** it is gear crit and is unaffected by the Vigil node cap.)

**Rarity drop weights [Proposed]** (relative; absolute drop rates are the economy gap **G-06**, not this appendix):

| Rarity | Common | Uncommon | Rare | Epic | Legendary | Mythic |
| :-- | --: | --: | --: | --: | --: | --: |
| Base weight | 1000 | 400 | 140 | 40 | 8 | 1 |

Corruption's `ItemRarity` bonus (§7.6) shifts this distribution upward (deep Corruption = better rarity odds) — the mechanical payoff of the L.7 scalar.

### M.7 Corrected Item Schema (§7.1, extended)

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
  "sockets": { "maxCapacity": 2, "insertedComponents": [] },
  "affixes": [
    { "slot": "Prefix", "type": "Prefix", "tier": 8,    "stat": "PhysicalDamagePercent", "baseValue": 120,  "finalValue": 132 },
    { "slot": "Prefix", "type": "Prefix", "tier": 10,   "stat": "FlatPhysicalDamage",    "baseValue": 50,   "finalValue": 55 },
    { "slot": "Prefix", "type": "Prefix", "tier": "Legendary", "stat": "ArmorPenetration", "baseValue": 0.15, "finalValue": 0.165 },
    { "slot": "Suffix", "type": "Suffix", "tier": 9,    "stat": "AttackSpeedPercent",    "baseValue": 0.12, "finalValue": 0.132 },
    { "slot": "Suffix", "type": "Suffix", "tier": 10,   "stat": "CriticalStrikeChance",  "baseValue": 0.08, "finalValue": 0.088 }
  ]
}
```

**Added vs §7.1:** `itemLevel`, `requiredLevel`, `implicits[]`, and a per-affix `slot`. **`baseRarity` is authoritative** (M.2).

### M.8 Register Closures Accumulated by This Appendix

| ID | Was | Now |
| :--- | :--- | :--- |
| **B-10** | Rarity ranges overlap → count ambiguous | **Closed** — rarity-first; count is derived (M.2). |
| **B-12** | Uncommon vs Rare 2-affix overlap | **Closed** — rarity is authoritative; `1P+1S`=Uncommon, `2P+0S/0P+2S`=Rare (M.3). |
| **Q-01** | Epic 3-affix split | **Answered** — `3P+0S` / `0P+3S` (M.3). |
| **Q-02** | Rare definition | **Answered** — 2–4 family with M.3 splits; `2P+2S` is the 4-affix Rare. |
| **Q-03** | Roll order | **Answered** — rarity → count → split → stat → tier → value (M.2/M.6). |
| **Q-04** | Legendary 5–6 splits | **Answered** — 5 ⇒ `3P+2S`/`2P+3S`; 6 ⇒ `3P+3S` (M.3). |
| **B-11** | Legendary split rules absent | **Closed** — explicit rule (M.3). |
| **B-02** | Implicits missing from schema | **Closed** — `implicits[]` added; grade-scaled per §4.1 (M.5/M.7). |
| **B-03** | No tier values / ilvl / reqLevel | **Closed** — tier ladder + `maxTier(ilvl)` + `requiredLevel` (M.4/M.5). |

**Still open after this appendix:** **B-09** (skill slots), **B-14/B-16** (terminology), **B-21** (Breach clamp), **B-23/B-24** (+ Q-10/Q-11). *(**B-04/B-17** relic timing / Ward relationship — **CLOSED v1.18**, App. N; **B-18** orphan damage-type *sources* — **CLOSED v1.16**, App. B v2.0; **B-15** §5 Radiant misprint — **CLOSED v1.17**.)*

### M.9 Definition of Done & Sign-off Gate

**Sign-off required on the structural rules:**
1. **Rarity-first** generation (M.2) — rarity is authoritative, count/split derived.
2. The **canonical count/split table** (M.3), including the Legendary rule that replaces "standard high-tier mix".
3. The **tier ladder** form (M.4) — one shared ladder + per-stat anchor, `maxTier(ilvl)`.
4. **Implicits in the schema** and the `requiredLevel` rule (M.5).

**After sign-off:** author the **base-type catalog** and the **per-stat `T10Anchor` table**, then implement the generator as a single `ItemGenerator` with a seeded RNG (reproducible for QA). Absolute **drop rates** remain part of the economy gap (**G-06**).

---

## Appendix N — Precursor Relic Activation & Sieve Continuity

*Ratified by author ruling (v1.18). **Closes B-04 and B-17; answers Q-05.** The relic **numbers** are unchanged — **B-15** corrected only the copy (v1.17). This appendix fixes **when** the favor is live and **how** it survives the campaign → endgame transition.*

### N.0 What this closes

| Finding | Question it answered | Ruling |
| :--- | :--- | :--- |
| **B-04 / Q-05** | Is favor live **on pickup** or only after **socketing into the Sieve**? | **Live on pickup** — each relic self-activates the act it is recovered. |
| **B-17** | The Sieve is sealed on the inaccessible island, yet the endgame runs from the Ward — how does favor persist? | **The Sieve Mirror carries it** — the portable focus channels the relics' favor to the hero at the Ward; the total never drops. |

### N.1 Activation timing — favor is live on pickup **[Ratified]**

Favor applies from the moment a relic is **recovered**; there is no dormant period.

| Relic | Recovered | Favor live from | Favor |
| :--- | :--- | :--- | :--- |
| The Sunken Aegis | Act 2 | **Act 2** | `+5% Max Life` \| `+3% Armor/DR` \| `+3% All Elemental Resistance` |
| The Hearth of Ignition | Act 3 | **Act 3** | `+5% Fire & Radiant Resistance` \| `-10% Debuff Duration` \| `+3% Damage vs. Calamity` |
| The Astral Key | Act 5 | **Act 5** | `+3% Move Speed` \| `+5% CDR` \| `-10% Hazard Damage Taken` |
| **Full total assembled** | — | **Act 5** | All three in hand — the aggregate block is complete **two Acts before the finale** |

**Re-scoping the source's "(Act 7+)" label.** The label is **retained**, but it marks when the **World Sieve operates** (the Act 7 purge), *not* when favor turns on. "Socketing into the World Sieve" is the **narrative culmination** of the three relics — not an activation gate.

**Socketing is a numeric no-op.** Because favor is already live, the Act 7 socketing changes **fiction, not stats**. This avoids a hidden second power spike at the climax and keeps the Act 5 → 7 curve legible.

### N.2 Continuity across the Rejection — the Sieve Mirror carries favor **[Ratified]**

At the Act 7 climax the three relics are socketed into the Sieve to purge the sanctuary; the Rejection then seals the island. Favor **does not lapse**.

- The **Sieve Mirror** — already canonical as the device the hero uses to open *Calamity Rifts* from *The Lonely Watch* — is the **portable focus** that channels the socketed relics' favor to the hero.
- The relics stay physically at the sealed Sieve; their **favor travels with the Mirror**. Favor is therefore **continuous**: full total before the Rejection, full total after.
- **No re-acquisition, no post-campaign power drop.** The endgame opens at the same favor baseline on which the campaign closed (reinforcing Pillar **P4 — earned exile**: the cost is *home*, not *power*).

### N.3 Data-model implication

Relic favor is a **persistent global buff set** keyed by relic ID and gated by **recovery** — never by a Sieve socket state:

```json
{
  "relicFavor": {
    "source": "hero",              // char-scoped; delivered by the Sieve Mirror
    "activation": "onPickup",      // B-04 / Q-05 ruling
    "socketingGated": false,       // Act 7 socketing is a narrative no-op
    "survivesRejection": true,     // B-17 ruling — Sieve Mirror continuity
    "relics": [
      { "id": "sunken_aegis",       "recoveredAct": 2, "active": true },
      { "id": "hearth_of_ignition", "recoveredAct": 3, "active": true },
      { "id": "astral_key",         "recoveredAct": 5, "active": true }
    ]
  }
}
```

`active` is derived from `recoveredAct <= currentAct`. **Nothing** in the relic system reads the World Sieve's physical state, so the sealed-island state (B-17) can never strand or drop the favor.

### N.4 Definition of Done & Sign-off Gate

**Sign-off required on the two rulings:** (1) **favor live on pickup** (N.1); (2) **Sieve Mirror continuity** across the Rejection (N.2). Both are behaviour-defining but *zero-number* — no balance re-derivation follows.

**Cross-refs:** GDD **§10.2** (mirrors this ruling); **B-15** (copy, v1.17); **App. A** (relic model protected — this appendix specifies behaviour, not stats).
