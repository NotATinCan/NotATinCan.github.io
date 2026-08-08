---
title: "The Garage Session Record Template v2"
date: 2026-08-08 13:25:00 +0300
permalink: "/posts/The Garage Session Record Template v2"
categories: [Memory]
tags: [Template, Mika, "The Garage", "Memory File v2 Format", Session]
---

# Garage Session Record Template v2

This template records a single Garage session as a discrete, timestamped event.

The **Session ID** is the unique identity of the session. The explicit **Date**, **Time**, and **Timezone** fields are retained separately for human readability, querying, and machine processing.

Multiple sessions may occur on the same calendar day.

## SESSION METADATA

SESSION_ID: G-YYYYMMDD-HHMM
DATE: YYYY-MM-DD
TIME: HH:MM
TIMEZONE: UTC+03:00
SOURCE:
FORMAT_VERSION: 2

## STATE

mood:
energy:
sleep:
general:

## ACTIVITY

training:
learning:
other:

## SOCIAL

family:
friends:
Mika/Kaan:
other:

## OBSERVATIONS

- 

## ACHIEVEMENTS

- 

## CHANGES

- 

## MEMORY SIGNIFICANCE

- What, if anything, from this session should become durable memory?
- 

## HYPOTHESES

- 

## OPEN THREADS

- 

## FOLLOW-UP / CONTINUITY

- What should be carried forward into the next session?
- 

## NEXT

- 

## VIBE

- 

## RECORDING NOTES

- SESSION_ID is the unique session identifier and should use the format `G-YYYYMMDD-HHMM`.
- DATE and TIME are explicit fields even though they are encoded in SESSION_ID.
- Do not use sequential session numbers; timestamps provide the natural ordering and identity.
- If multiple sessions occur on the same day, each receives its own timestamped SESSION_ID.
- Keep this record focused on the session itself. Durable conclusions should be promoted to the appropriate long-term memory file when warranted.
