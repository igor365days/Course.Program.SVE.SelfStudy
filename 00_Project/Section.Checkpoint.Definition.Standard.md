# Section Checkpoint Definition Standard

**Document:** Section.Checkpoint.Definition.Standard  
**Status:** Canonical project standard  
**Applies to:** `Course.Program.SVE.SelfStudy`

## 1. Purpose

A Section Checkpoint (CP) is the canonical control point at the end of each of the five course sections.

Its purpose is to verify integrated use of the important material accumulated across all source lessons belonging to the section and to determine readiness to enter the next section.

A CP is not a progress record and is not a collection of the preceding LCP results. It is a separate integrated assessment object.

## 2. Route position

For every section:

`Lesson → LCP → ... → final Lesson → LCP → CP → next Section`

The CP is conducted only after the LCP of the final lesson in the section has been successfully completed.

## 3. CP identity

Stable identifiers:

`CP-1` … `CP-5`

Each CP belongs to exactly one section and covers all lessons and Units assigned to that section.

## 4. Assessment purpose

The CP must determine whether the learner can integrate and independently use important material across the whole section.

It must not merely repeat the five/three/four preceding LCPs. At least one task must require transfer or integration across multiple lessons.

Depending on the section, a CP may assess vocabulary, grammar, transformation, reading comprehension, written production, text-based communication, listening practice, pronunciation practice, or combined use.

## 5. Assessment components

Each mandatory component must have:

1. a concrete task;
2. a defined expected evidence;
3. a verification mode;
4. a success criterion.

Verification modes follow `Assessment.Verification.Policy.md`:

- `AI_VERIFIED`;
- `USER_CONFIRMED`;
- `NOT_VERIFIED`.

A CP may use `COMBINED` as a design label when different components use different verification modes, but each component must still specify its actual verification mode.

## 6. Completion rule

A CP is successfully completed only when all mandatory components have acceptable evidence and the integrated section result meets the defined success criteria.

If the result is insufficient, the system identifies the deficient competencies, organizes targeted remediation and performs a CP recheck.

Failure of a CP does not automatically require repeating the whole section.

## 7. Canonical CP definition

Each CP definition should contain:

1. CP ID;
2. section;
3. covered Lessons;
4. covered Units;
5. assessment purpose;
6. required integrated competencies;
7. assessment tasks;
8. expected evidence and verification mode for each mandatory component;
9. success criteria;
10. remediation guidance;
11. recheck conditions;
12. canonical references.

## 8. Separation from learner state

The CP definition is canonical course content and belongs in GitHub.

Actual dates, scores, errors, attempts and completion states belong to the learning-state system and must not be stored in the canonical CP definition.

## 9. Relationship to LCP

`Unit verification → LCP → Section CP`

LCP verifies integrated use of one source lesson. CP verifies integrated use across the complete section and therefore has a higher transfer requirement.
