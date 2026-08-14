# Assessment Verification Policy

**Document:** Assessment.Verification.Policy  
**Status:** Canonical project policy  
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

This document defines how different types of control tasks are verified. It is a canonical policy of the course and is independent of any individual learner's results.

The policy prevents the course from assuming that AI can reliably verify every aspect of language learning.

## 2. Verification methods

### AI_VERIFIED

The result can be directly assessed by AI with sufficient reliability for the defined task.

Typical examples:
- grammar exercises;
- vocabulary recall and use;
- reading comprehension;
- written production;
- controlled transformations;
- text-based communicative tasks.

### USER_CONFIRMED

The task requires an action or evidence that AI cannot reliably observe or assess in the available environment. The learner confirms that the required action was completed.

Typical examples:
- pronunciation practice when reliable pronunciation assessment is unavailable;
- practice performed outside ChatGPT;
- use of external audio or other external material where completion cannot be independently verified;
- physical or offline learning activities.

USER_CONFIRMED means **the learner confirms execution of the required action**. It does not by itself claim that AI has verified mastery.

### COMBINED

The control contains components requiring different verification methods. Each component must be verified according to its own applicable method.

## 3. Control-type policy

| Control type | Default verification |
|---|---|
| Grammar | AI_VERIFIED |
| Vocabulary | AI_VERIFIED |
| Reading comprehension | AI_VERIFIED |
| Writing | AI_VERIFIED |
| Controlled transformation | AI_VERIFIED |
| Text-based communication | AI_VERIFIED |
| Listening | COMBINED / USER_CONFIRMED depending on available evidence |
| Pronunciation | USER_CONFIRMED unless reliable direct assessment is available |
| External practical task | USER_CONFIRMED |
| Offline task | USER_CONFIRMED |

These are default policies, not guarantees. The actual assessment design must respect the capabilities available at the time of course execution.

## 4. Control-point composition

A Unit verification, LCP or CP may contain multiple control components.

The verification policy applies to the **type of component**, not to the name of the control point itself.

Example:

```text
LCP-01
├── Grammar ........ AI_VERIFIED
├── Vocabulary ..... AI_VERIFIED
├── Reading ........ AI_VERIFIED
├── Listening ...... USER_CONFIRMED
└── Pronunciation .. USER_CONFIRMED
```

The canonical definition of the control point does not need to repeat the general verification policy for each component.

## 5. Completion rule

Every mandatory control component must have an acceptable verification result.

`NOT_VERIFIED` means that the required evidence or confirmation is still missing.

A control point must not be considered fully completed while a mandatory component remains `NOT_VERIFIED`.

A control point may be completed with a mixture of `AI_VERIFIED` and `USER_CONFIRMED` components when that composition is permitted by this policy and by the control's requirements.

## 6. Evidence distinction

The system must distinguish:

```text
AI_VERIFIED
USER_CONFIRMED
NOT_VERIFIED
```

These states describe the **source of confirmation**, not necessarily the quality score of the learner's performance.

Assessment result and verification source are separate concepts.

For example:

```text
Task execution: COMPLETED
Verification source: USER_CONFIRMED
Assessment result: ACCEPTED
```

or:

```text
Task execution: COMPLETED
Verification source: AI_VERIFIED
Assessment result: FAILED
```

## 7. Future capability changes

If available AI capabilities change, the central policy may be updated without rewriting every Unit or checkpoint definition.

Such a change must not silently alter historical learner records. Historical records retain the verification method that was actually used.
