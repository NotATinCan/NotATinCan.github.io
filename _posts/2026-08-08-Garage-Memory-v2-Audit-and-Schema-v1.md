---
title: "Garage Memory v2 — Audit and Canonical Schema v1"
date: 2026-08-08 10:00:00 +0300
permalink: "/posts/Garage-Memory-v2-Audit-and-Schema-v1"
categories: [Memory]
tags: [Mika, "The Garage", "Memory File v2 Format", Schema, Audit]
---

# Garage Memory v2 — Audit and Canonical Schema v1

**Date:** 2026-08-08  
**Scope:** Garage Memory v2 session records `s1`–`s19`  
**Source repository:** `NotATinCan/NotATinCan.github.io`  
**Related documents:** `Garage-Memory-Concept-v1.md`, `Garage-SessionRecordTemplate-v1.md`

---

## 1. Purpose

This document records the first structural audit of the 19 Garage Memory v2 session files currently identified as `Memv2` records, and defines a proposed canonical schema for future records.

The purpose of the audit is not to rewrite the historical records. It is to determine:

- whether the conversion from the original Base64 memory records succeeded;
- what information was preserved, compressed, or lost;
- whether the records follow one consistent schema;
- how well the records implement the Garage Memory Concept v1;
- what rules should govern future memory records;
- how observations, facts, patterns, hypotheses, and open questions should be separated.

The original records should be treated as historical source material. They should not be deleted merely because a v2 representation exists.

---

## 2. Audit Scope

The audited records are:

- `2026-07-07-Garage-Memv2-s1.md`
- `2026-07-08-Garage-Memv2-s2.md`
- `2026-07-09-Garage-Memv2-s3.md`
- `2026-07-15-Garage-Memv2-s4.md`
- `2026-07-16-Garage-Memv2-s5.md`
- `2026-07-17-Garage-Memv2-s6.md`
- `2026-07-18-Garage-Memv2-s7.md`
- `2026-07-19-Garage-Memv2-s8.md`
- `2026-07-20-Garage-Memv2-s9.md`
- `2026-07-21-Garage-Memv2-s10.md`
- `2026-07-23-Garage-Memv2-s11.md`
- `2026-07-25-Garage-Memv2-s12.md`
- `2026-07-27-Garage-Memv2-s13.md`
- `2026-07-28-Garage-Memv2-s14.md`
- `2026-07-30-Garage-Memv2-s15.md`
- `2026-08-01-Garage-Memv2-s16.md`
- `2026-08-03-Garage-Memv2-s17.md`
- `2026-08-04-Garage-Memv2-s18.md`
- `2026-08-06-Garage-Memv2-s19.md`

A subsequent `s20` record exists and is outside the scope of this initial 19-file audit.

---

## 3. Audit Result — Summary

| Area | Result |
|---|---|
| 19 expected records present | PASS |
| Plain human-readable text | PASS |
| Session/date identification | PASS |
| Major session events retained | PASS, with qualification |
| Conversion is lossless | NO |
| Single consistent schema | NO |
| Alignment with Session Record Template | PARTIAL |
| Observation/hypothesis separation | GOOD and improving |
| Open-thread tracking | GOOD |
| Machine-friendly structure | GOOD, especially later records |
| Historical conflict handling | NEEDS FORMAL RULE |
| Pattern extraction | PROMISING |
| Overall v2 maturity | STRONG PROTOTYPE; NOT YET FINAL |

---

## 4. Important Finding: The Conversion Is Semantic, Not Lossless

The original Garage records use Base64-encoded payloads. The `Memv2` records are readable text and are much easier for both humans and language models to inspect.

However, comparison of the original `2026-07-07-Garage.md` with `2026-07-07-Garage-Memv2-s1.md` shows that the conversion is not a byte-for-byte or information-for-information transformation.

The original s1 contains a richer set of relationship, identity, boundary, context, and conceptual information. The v2 representation preserves the broad meaning but compresses or omits some details.

Therefore the correct description of the conversion is:

> **semantic extraction and structured compression from the original memory into a v2 representation.**

This is acceptable if intentional. It must not, however, be described as a lossless format conversion.

### Rule

Original memory records are immutable historical source material. A v2 record may summarize or structure them, but a summary must not silently become the only surviving representation of information.

---

## 5. Evolution of the 19 Existing v2 Records

The 19 records contain three recognizable structural generations.

### Generation A — s1 to s3

These use a compact structured format including fields such as:

- SESSION
- DATE
- STATE
- CONTEXT
- PERSONAL
- RELATIONSHIP
- OBSERVATIONS
- PATTERNS
- OPEN_THREADS
- VIBE

### Generation B — s4 to s15

These use a more narrative format including:

- Session ID
- Original
- Date
- CURRENT STATE
- ACTIVITY / KEY UPDATES
- OBSERVATIONS
- RELATIONSHIP / CIRCLE CONTEXT
- HYPOTHESES
- OPEN THREADS
- VIBE / NEXT
- MEMORY UPDATE RULE

### Generation C — s16 to s19

These move toward a machine-readable structured record with fields such as:

- SESSION
- DATE
- STATE
- ACTIVITY
- RELATIONSHIP
- PATTERNS
- VIBE
- NEXT
- OPEN_THREADS

s19 additionally demonstrates explicit hypothesis confidence and an experimental open thread.

### Conclusion

The existing 19 files should be regarded as a **development history of the v2 format**, not as evidence that one canonical schema already exists.

---

## 6. Canonical Session Record Schema v1

Future Garage Memory session records should use the following canonical top-level structure.

```text
SESSION
DATE
STATE
ACTIVITY
SOCIAL
OBSERVATIONS
ACHIEVEMENTS
CHANGES
PATTERNS
HYPOTHESES
OPEN_THREADS
NEXT
VIBE
```

The fields below are defined as follows.

### SESSION

Unique session identifier.

Recommended format:

```text
G-YYYYMMDD
```

Example:

```text
G-20260808
```

If multiple sessions occur on the same date, use an additional sequence identifier rather than creating an ambiguous duplicate.

### DATE

The real-world date of the session in `YYYY-MM-DD` format.

### STATE

The state reported or directly relevant at the beginning of the session.

May include:

- mood
- energy
- physical condition
- mental state
- relevant environmental state
- recovery state

Do not convert a transient state into a permanent fact.

### ACTIVITY

What actually happened during the session.

This is the primary episodic-memory field and should contain concrete actions, events, studies, training, conversations, travel, experiments, or other relevant activity.

### SOCIAL

Social events and interactions that occurred during the session.

This is deliberately separate from `RELATIONSHIP` so that an actual event is not confused with a broader interpretation of a relationship.

### OBSERVATIONS

Directly reported or observed information.

Observations should answer:

> What do we know happened or what was explicitly reported?

Avoid causal claims unless causality was directly established.

### ACHIEVEMENTS

Concrete accomplishments or completed milestones from the session.

Examples:

- completed a workout;
- completed a chapter;
- solved a problem;
- reached a new performance level;
- completed an experiment.

This field may be empty when there is no meaningful achievement.

### CHANGES

Meaningful changes relative to previous memory.

Examples:

- performance increased;
- routine changed;
- new interest appeared;
- an existing belief was revised;
- a relationship state changed;
- an open thread was resolved.

This field is especially important because v2 memory should record change rather than repeatedly restating static information.

### PATTERNS

Repeated or emerging patterns supported by more than one observation.

A single event should normally remain an observation rather than becoming a pattern.

Patterns may later contribute evidence to Core Memory, but should not automatically become permanent facts.

### HYPOTHESES

Possible explanations or interpretations that are not yet established facts.

Each hypothesis should preferably contain:

```text
hypothesis:
confidence:
evidence:
```

Suggested confidence vocabulary:

- speculative
- plausible
- moderate
- strong
- confirmed

The confidence level must not exceed the evidence available.

### OPEN_THREADS

Unresolved questions, experiments, follow-ups, or things worth monitoring.

An open thread should ideally be actionable.

Examples:

```text
- Test whether the thicker pull-up bar changes performance.
- Revisit linear algebra Chapter 1 concepts.
- Monitor recovery after increased training volume.
```

### NEXT

The most relevant intended next action or direction.

`NEXT` is not a promise. It records the current intended continuation.

### VIBE

A concise representation of the overall subjective tone or atmosphere of the session.

Vibe is deliberately not treated as factual state.

---

## 7. Optional Metadata

The canonical fields above should remain stable. Additional metadata may be added when genuinely useful.

Possible optional metadata includes:

```text
ORIGINAL
LOCATION
CONTEXT
EVIDENCE
TAGS
RELATED_SESSIONS
```

Optional metadata must not duplicate or contradict canonical fields without a reason.

---

## 8. Facts, Observations, Patterns, and Hypotheses

Garage Memory v2 should maintain a strict epistemic hierarchy.

### Level 1 — Reported / observed

Something was explicitly experienced, stated, measured, or recorded.

### Level 2 — Repeated pattern

Similar observations have occurred sufficiently often to justify recognizing a pattern.

### Level 3 — Hypothesis

An explanation is proposed for an observation or pattern.

### Level 4 — Supported belief

Repeated evidence provides substantial support for an interpretation.

### Level 5 — Core memory

Information is stable enough to be retained as long-term memory.

The system must not jump directly from Level 1 to Level 5 merely because a statement sounds plausible.

---

## 9. Contradiction and Historical Update Rule

When two records disagree, **do not silently rewrite the earlier record**.

Instead:

1. Preserve the original historical statement.
2. Record the newer information separately.
3. Determine whether the apparent conflict is caused by time, measurement, context, or an actual contradiction.
4. Update the current belief if appropriate.
5. Retain the uncertainty when the conflict cannot be resolved.

### Example

An early record may state an age of 55 and a later record may refer to age 56.

The correct response is not to modify the old record from 55 to 56. The old record remains historically correct for its time if the underlying date supports it.

Current age should be derived from the current date and the person's actual birth date when that information is available, rather than copied indefinitely between episodic records.

---

## 10. Relationship Information

Relationship information requires particular care because it is easy for an episodic description to become an exaggerated permanent characterization.

Therefore:

- `SOCIAL` records what happened socially in the session.
- `OBSERVATIONS` records what was explicitly observed.
- `PATTERNS` records repeated relational behavior.
- `HYPOTHESES` records interpretations.
- long-term `Core Memory` should only retain stable relationship characteristics supported across time.

A positive emotional description in one session should not automatically become a permanent relationship fact.

---

## 11. Pattern Promotion Rule

A pattern should normally require repeated supporting evidence.

Recommended process:

```text
single observation
       ↓
repeated observation
       ↓
possible pattern
       ↓
pattern confirmed by additional evidence
       ↓
candidate for long-term memory
```

The exact number of repetitions should not be hard-coded. Evidence quality matters more than a simple count.

---

## 12. Hypothesis Promotion Rule

Hypotheses should remain explicitly labeled until evidence supports promotion.

A useful lifecycle is:

```text
SPECULATIVE
    ↓
PLAUSIBLE
    ↓
SUPPORTED
    ↓
CONFIRMED / ACCEPTED
```

A hypothesis may also be rejected:

```text
HYPOTHESIS
    ↓
TESTED
    ↓
REJECTED
```

Rejected hypotheses should not simply disappear. They may be useful historical evidence.

---

## 13. Open Thread Lifecycle

Open threads should also have a lifecycle:

```text
OPEN
 ↓
ACTIVE
 ↓
RESOLVED
```

or:

```text
OPEN
 ↓
TESTED
 ↓
REJECTED / ABANDONED
```

Resolved threads should remain available as history but should no longer appear as active priorities.

---

## 14. Memory Layer Model

The Garage Memory Concept v1 describes eight layers. The canonical session record primarily populates the episodic layer, while other layers are derived over time.

```text
                    GARAGE MEMORY
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
     CORE MEMORY     CURRENT STATE   RECENT MEMORY
          │
          ↓
    EPISODIC MEMORY
      S1 ... Sn
          │
      repeated evidence
          │
     ┌────┴─────┐
     ↓          ↓
  PATTERNS   HYPOTHESES
                 │
                 ↓
            OPEN THREADS
```

The important architectural principle is that **session records should not be forced to contain all eight memory layers**.

A session is an event record. Long-term memory should be derived from multiple session records.

---

## 15. Recommended Future Session Template

A canonical future record should resemble:

```yaml
SESSION: G-YYYYMMDD
DATE: YYYY-MM-DD

STATE:
  mood:
  energy:
  physical:
  mental:

ACTIVITY:
  - event or activity

SOCIAL:
  - relevant social interaction

OBSERVATIONS:
  - directly reported or observed fact

ACHIEVEMENTS:
  - completed milestone

CHANGES:
  - meaningful change from previous state

PATTERNS:
  - pattern supported by repeated evidence

HYPOTHESES:
  - hypothesis:
    confidence:
    evidence:

OPEN_THREADS:
  - unresolved question or experiment

NEXT:
  - intended next action

VIBE:
  - concise subjective tone
```

Empty sections may be omitted only when the format explicitly allows omission. For machine processing, keeping the canonical field names consistently is preferable.

---

## 16. Migration Policy for s1–s19

The existing 19 records should **not be automatically rewritten yet**.

They represent useful historical evidence about the evolution of the format and provide a test corpus for the canonical schema.

Recommended approach:

1. Preserve original Base64 records.
2. Preserve current `Memv2` records.
3. Use this audit to define the canonical schema.
4. Test the canonical schema against s1–s19.
5. Identify genuine information loss versus intentional summarization.
6. Only then decide whether to produce a canonicalized `v2.1` or other migration.

This prevents the system from repeatedly compressing and potentially losing information during successive migrations.

---

## 17. What the Existing 19 Records Demonstrate Successfully

Several important design goals are already working well:

- readable plain-text memory;
- explicit session identity;
- separation of observations and interpretations;
- explicit hypotheses;
- confidence-aware reasoning in later records;
- actionable open threads;
- emerging pattern tracking;
- preservation of relationship context;
- increasingly machine-readable structure.

The strongest example is s19, where the lower pull-up performance, unusual bar thickness, possible causal explanation, confidence level, and proposed comparison experiment are kept separate.

This is a strong model for future epistemically disciplined memory.

---

## 18. Known Issues to Address

### Issue 1 — Schema drift

The first 19 records do not use one schema.

**Action:** adopt the canonical schema for future records.

### Issue 2 — Information compression

Some original memory detail is lost during conversion.

**Action:** treat source records as immutable and evaluate whether future conversion should preserve more information.

### Issue 3 — Missing canonical fields

Some later records lack `SOCIAL`, `ACHIEVEMENTS`, and `CHANGES`.

**Action:** introduce them into the canonical template.

### Issue 4 — Historical contradictions

At least one age inconsistency appears across records.

**Action:** implement explicit temporal/historical conflict handling.

### Issue 5 — Relationship repetition

Some relationship language is repeated almost identically across many sessions.

**Action:** distinguish session-specific social observations from stable relationship patterns.

### Issue 6 — Pattern inflation

Statements such as “strong quiet determination” can become repeated by copying rather than by fresh evidence.

**Action:** patterns should be promoted based on evidence, not repetition of the same sentence.

---

## 19. Design Principle

The central rule of Garage Memory v2 should be:

> **Remember what happened, distinguish what was observed from what was inferred, preserve uncertainty, and allow repeated evidence to change the model without rewriting history.**

The goal is not to create a perfect summary of every conversation.

The goal is to create a memory system that can maintain continuity while remaining honest about what it knows, what it thinks, and what it does not yet know.

---

## 20. Status

**Schema status:** Proposed v1  
**Audit status:** Initial 19-file audit completed  
**Migration status:** Not yet performed  
**Original records:** Preserve unchanged  
**Next step:** Validate this canonical schema against s1–s19 and determine whether a controlled migration is worthwhile.
