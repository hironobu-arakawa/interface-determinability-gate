# Interface Determinability Gate

**Role**: Field (non-core)  
**Scope**: AI detachment guardrail  
**Primary Boundary**: Responsibility  
**Secondary Boundary**: Interpretation  
**Audience**: Human / AI  
**Stability**: Medium

---

## What this repository defines

This repository defines a **determinability guardrail** for AI-assisted systems.

> **If a state cannot be deterministically asserted from an interface or certified sensing,  
> AI must not infer or assume it.  
> In such cases, AI is explicitly detached from decision support.**

This rule exists to **protect responsibility boundaries**,  
not to limit sensing, analytics, or automation capabilities.

---

## What this is *not*

This repository does **not** define:

- Root cause analysis
- Physical or mechanical inference
- Safety or power-chain diagnosis
- Recovery decision logic
- Domain-specific procedures

Those concerns require **physical inspection, recurrence, or human judgment**,  
and are therefore **out of scope by design**.

---

## Core idea: Determinability over capability

Modern sensing continues to improve.  
However, **capability does not imply determinability**.

This guardrail uses a single criterion:

> **Can this state be asserted without physical assumption,  
> using only interface-observable facts or certified signals?**

- **Yes** → AI may reference and present it  
- **No** → AI must detach from decision support  

“Seems likely”, “probably”, or “usually” are explicitly disallowed.

---

## Optional: routing annotations (without changing the judgment)

Some environments mix evidence qualities (e.g., contract-trusted API vs computer vision)
and interaction weights (e.g., system display vs human input). In such cases,
**pass/block alone is insufficient for scalable review**.

This pattern allows *optional* **annotations** to be attached to gate outputs so that a downstream
approval layer (RP) can route items to:

- **batch approval** (low risk)
- **spot-check** (medium risk)
- **per-item review** (high responsibility / higher noise sources)

These annotations are **non-normative**: they must never change a determinability decision.
See `patterns/determinability_gate.yaml` for the vocabulary (`source_method`, `interaction_type`, `evidence_ref`, `quality_band`).

---

## What *is* included here

This repository provides **domain-agnostic building blocks**:

- A **determinability gate pattern**
- A **minimal interface operation log schema**
- Explicit **AI detachment rules**
- **Transparency requirements** explaining *why* AI is silent
- **Evaluation metrics** for overreach-free behavior

All contents are intentionally written without factory-specific,
medical-specific, or infrastructure-specific terminology.

---

## Domain usage (profiles & examples)

Domain-specific interpretations are intentionally separated.

- `profiles/`  
  Maps domain vocabulary (e.g. factory CI, medical devices, ops consoles)
  onto the generic interface concepts used here.

- `examples/`  
  Concrete scenarios demonstrating how the guardrail applies in practice.

This separation keeps the **core understandable across domains**,  
while allowing deep specialization where needed.

---

## Relationship to VCDesign (VCD)

This repository is **not VCDesign core**.

It is a **Field-level guardrail** that operates *under* VCD constraints:

- VCD defines **where meaning, judgment, and responsibility must stop**
- This gate defines **when AI must step out to preserve those boundaries**

Think of it as a **safety valve**, not a design center.

---

## Design intent (short)

- AI is evaluated not by how much it says  
- but by **when it correctly remains silent**
- and **whether that silence is explainable**

Silence here is not failure.  
It is a **designed outcome**.

---

## Start here

- Pattern: `patterns/determinability_gate.yaml`
- Schema: `schemas/operation_log_min.yaml`
- Domain mapping: `profiles/`
- Concrete scenarios: `examples/`

---

## Why this matters

Most AI failures in operational systems do not come from bad models,  
but from **overstepping responsibility boundaries**.

This repository exists to make that boundary **explicit, testable, and reviewable**.

---

## One-line principle (for designers)

> **If you cannot deterministically assert it,  
> you must not let AI imagine it.**

---

## Citation

If you reference or adapt this pattern in papers, designs, or systems,
please consider citing:

> Interface Determinability Gate (IDG) Pattern  
> Originally articulated by Hironobu Arakawa, 2025.  
> https://github.com/hironobu-arakawa/interface-determinability-gate
