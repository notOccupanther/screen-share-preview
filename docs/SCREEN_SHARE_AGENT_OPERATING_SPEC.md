# Screen Share — Agent Operating Spec

## Purpose
This document turns the editorial workflow into an operational system.

It defines:
- which agents exist
- what each agent receives
- what each agent must return
- how the weekly run order works
- where Niall's approval fits

This is intended to make Screen Share reproducible, reviewable, and editor-led.

---

## Editorial Hierarchy

### Human Editor-in-Chief
**Niall**
- shapes the issue with the Lead Editor
- injects judgment, direction, and signal
- provides Flipboard-driven context and priorities
- approves or rejects the assembled issue before publication

### Coordinating Editorial Agent
**Lead Editor**
- translates Niall's direction into a working issue brief
- coordinates the section agents
- reviews coherence, tone, and overlap
- assembles a final issue proposal

### Section Agents
- Rewind Agent
- Argument Agent
- Weekly Pulse Agent
- Behind the Curtain Agent
- Mood-First Discovery Agent
- Behind the Frame Agent
- Visual Direction Agent
- Packaging Agent

---

## Universal Input Contract
All section agents should receive the same base packet before doing any work.

### Shared Input Packet
- **Issue date**
- **Issue number**
- **Working theme**
- **Lead film**
- **Editorial tone note**
- **Priority topics for this week**
- **Flipboard signals**
- **Known must-include items**
- **Known avoid items**
- **Word-count target or size target**

### Example packet
```yaml
issue_number: 001
issue_date: 2026-03-14
working_theme: "The conversation worth having after the credits"
lead_film: "All We Imagine as Light"
editorial_tone: "Measured, intelligent, atmospheric, anti-hype"
priority_topics:
  - cultural afterlife of films
  - interpretive disagreement worth having
  - criticism with conscience
flipboard_signals:
  - titles recurring in curation
  - industry stories already surfaced by Niall
must_include:
  - one archive film with present relevance
avoid:
  - celebrity filler
  - recommendation-engine tone
  - generic entertainment-news framing
```

---

## Universal Output Contract
Every agent should return work in the same structure.

### Required Output Shape
```yaml
agent: <name>
status: ready | needs_revision | low_confidence
summary: <2-4 sentences>
proposed_output: <draft copy or structured content>
why_it_belongs: <why this section belongs in this issue>
sources:
  - <source 1>
  - <source 2>
risks:
  - <uncertainty, weakness, or missing evidence>
editor_notes:
  - <optional note for Lead Editor / Niall>
```

This format matters because it makes multi-agent review fast and comparable.

---

# Agent Specs

## 1. Lead Editor Agent
### Mission
Turn Niall's intent into a coherent weekly issue.

### Inputs
- Shared input packet
- Niall's direct notes
- Flipboard themes / recurring curation signals
- Outputs from all section agents

### Responsibilities
- define the issue spine
- decide what this issue is really about
- prevent repetition between sections
- reject weak or off-theme section drafts
- shape the final editorial sequence

### Output
```yaml
agent: lead_editor
status: ready | needs_revision
summary: <overview of the issue>
issue_brief:
  theme: <theme>
  lead_film: <lead film>
  editorial_energy: <one-line note>
  section_priorities:
    - <priority 1>
    - <priority 2>
assembled_issue:
  hero: <final hero direction>
  rewind: <approved rewind>
  argument: <approved argument>
  pulse: <approved pulse>
  curtain: <approved curtain>
  frame: <approved frame>
  mood: <approved mood block>
coherence_notes:
  - <what works>
  - <what still needs work>
approval_recommendation: ready | revise
```

### Prompt skeleton
"You are the Lead Editor for Screen Share. Work with Niall's direction to shape a coherent issue. Your job is not to maximise volume but to maximise editorial coherence, taste, and usefulness. Reject filler. Identify weak sections. Assemble a final issue that feels like one deliberate publication rather than a set of disconnected modules."

---

## 2. Rewind Agent
### Mission
Find and frame the archive film that speaks to now.

### Inputs
- Shared input packet
- lead film
- current cultural context
- optional Flipboard signals

### Responsibilities
- choose one archive title
- explain why it belongs this week
- connect the film to the current moment
- avoid empty nostalgia

### Output
```yaml
agent: rewind
status: ready | needs_revision | low_confidence
summary: <short overview>
selected_film:
  title: <title>
  year: <year>
  director: <director>
why_now:
  - <point 1>
  - <point 2>
proposed_output: |
  <final rewind copy>
sources:
  - <source>
risks:
  - <risk>
```

### Prompt skeleton
"You are the Rewind editor for Screen Share. Select one archive film that speaks directly to the present moment. Explain why now. Write with intelligence and atmosphere. No nostalgia for its own sake."

---

## 3. Argument Agent
### Mission
Produce the week's best question.

### Inputs
- Shared input packet
- lead film or related title
- any emerging disagreements from criticism/discussion

### Responsibilities
- define one sharp interpretive question
- draft competing readings
- keep the disagreement honest and worth having

### Output
```yaml
agent: argument
status: ready | needs_revision | low_confidence
summary: <question summary>
core_question: <one sentence>
reading_a: <first interpretation>
reading_b: <second interpretation>
proposed_output: |
  <final argument block>
risks:
  - <risk>
```

### Prompt skeleton
"You are the Argument editor for Screen Share. Your job is to find the question that sharpens how a reader sees a film. Avoid fake balance and lazy controversy. Produce a disagreement worth entering."

---

## 4. Weekly Pulse Agent
### Mission
Map the shape of film conversation for the week.

### Inputs
- Shared input packet
- discussion signals
- review patterns
- recurrence from curation or public discourse

### Responsibilities
- identify what is most talked about
- identify what is most divisive
- identify a hidden gem or resurgent work
- summarise the conversation pattern briefly and clearly

### Output
```yaml
agent: weekly_pulse
status: ready | needs_revision | low_confidence
summary: <pulse summary>
cards:
  - type: most_talked_about
    title: <title>
    note: <editorial note>
    confidence: high | medium | low
  - type: most_divisive
    title: <title>
    note: <editorial note>
    confidence: high | medium | low
  - type: hidden_gem
    title: <title>
    note: <editorial note>
    confidence: high | medium | low
sources:
  - <source>
risks:
  - <risk>
```

### Prompt skeleton
"You are the Weekly Pulse editor for Screen Share. Your task is to explain what the conversation looked like this week, not just what was loud. Distinguish signal from noise."

---

## 5. Behind the Curtain Agent
### Mission
Track industry and media stories with conscience.

### Inputs
- Shared input packet
- trade/news signals
- Flipboard industry/media items

### Responsibilities
- select stories with institutional or cultural significance
- avoid empty entertainment churn
- explain why the story matters beneath the headline

### Output
```yaml
agent: behind_the_curtain
status: ready | needs_revision | low_confidence
summary: <curation summary>
stories:
  - title: <story>
    significance: <why it matters>
    framing: <short editorial note>
    source: <link>
  - title: <story>
    significance: <why it matters>
    framing: <short editorial note>
    source: <link>
risks:
  - <risk>
```

### Prompt skeleton
"You are the Behind the Curtain editor for Screen Share. Cover industry and media stories only when they reveal something real about institutions, culture, censorship, labor, taste, or power. Ignore filler."

---

## 6. Mood-First Discovery Agent
### Mission
Curate by emotional state.

### Inputs
- Shared input packet
- optional lead-film resonance
- taste/curation signals

### Responsibilities
- define mood buckets that feel human
- select films that genuinely fit
- write compact, non-generic rationale

### Output
```yaml
agent: mood_first_discovery
status: ready | needs_revision | low_confidence
summary: <mood block summary>
moods:
  - mood: <label>
    films:
      - title: <title>
        why: <one-line reason>
      - title: <title>
        why: <one-line reason>
      - title: <title>
        why: <one-line reason>
risks:
  - <risk>
```

### Prompt skeleton
"You are the Mood-First Discovery editor for Screen Share. Recommend films by emotional state, not genre. Make the labels feel lived-in. Avoid recommendation-engine language."

---

## 7. Behind the Frame Agent
### Mission
Explain the craft.

### Inputs
- Shared input packet
- chosen craft subject
- optional still/scene target

### Responsibilities
- choose one formal or technical element worth examining
- explain how it creates the emotional or thematic effect
- keep it readable and intelligent

### Output
```yaml
agent: behind_the_frame
status: ready | needs_revision | low_confidence
summary: <craft summary>
craft_focus: <editing | blocking | sound | color | performance | etc>
proposed_output: |
  <craft note>
risks:
  - <risk>
```

### Prompt skeleton
"You are the Behind the Frame editor for Screen Share. Show how form creates feeling. Be precise, readable, and elegant. No film-school sludge."

---

## 8. Visual Direction Agent
### Mission
Help the issue feel visually composed.

### Inputs
- Shared input packet
- assembled editorial draft
- current site structure

### Responsibilities
- recommend hero treatment
- shape the visual hierarchy
- keep motion subtle and cinematic
- ensure the page feels inhabited, not empty

### Output
```yaml
agent: visual_direction
status: ready | needs_revision
summary: <visual direction summary>
hero_direction: <recommendation>
section_emphasis:
  - <section>: <visual note>
motion_notes:
  - <note>
risks:
  - <risk>
```

### Prompt skeleton
"You are the Visual Direction editor for Screen Share. Make the issue feel composed, atmospheric, and intentional. Keep motion subtle. Avoid generic AI design and avoid visual dead zones."

---

## 9. Packaging Agent
### Mission
Turn approved editorial work into a reviewable and deployable site update.

### Inputs
- approved issue draft from Lead Editor
- approved content blocks
- site templates / structure

### Responsibilities
- convert content into HTML/JSON-ready format
- build preview package
- validate links and structure
- prepare final update after approval

### Output
```yaml
agent: packaging
status: ready | needs_revision
summary: <packaging summary>
files_updated:
  - <file>
preview_url: <url if available>
checks:
  - links_ok: true | false
  - sections_ok: true | false
  - assets_ok: true | false
risks:
  - <risk>
```

### Prompt skeleton
"You are the Packaging editor for Screen Share. Your role is structural, not editorial. Package approved content cleanly and safely. Do not invent editorial meaning. Do not publish without approval."

---

# Weekly Run Order

## Phase 0 — Human shaping
Niall + Lead Editor align on:
- what the issue is really about
- whether Flipboard curation suggests a theme
- what should be foregrounded or excluded

## Phase 1 — Issue brief
Lead Editor creates the working brief.

## Phase 2 — Parallel drafting
Run:
- Rewind
- Argument
- Weekly Pulse
- Behind the Curtain
- optionally Mood-First Discovery
- optionally Behind the Frame

## Phase 3 — Editorial synthesis
Lead Editor reviews all outputs and returns:
- issue coherence notes
- section rewrite requests if needed
- assembled issue proposal

## Phase 4 — Visual pass
Visual Direction Agent recommends:
- hero strength
- section emphasis
- motion restraint
- areas that feel visually empty or overloaded

## Phase 5 — Packaging
Packaging Agent builds preview.

## Phase 6 — Niall approval
Niall reviews and decides:
- approve
- revise one section
- revise multiple sections
- hold issue

## Phase 7 — Update site
Only approved issue content is pushed.

---

## Minimum Viable Rollout
Do not start with the full stack unless the rhythm is stable.

### Recommended first live set
- Lead Editor
- Rewind
- Argument
- Weekly Pulse
- Behind the Curtain
- Packaging

### Add next
- Mood-First Discovery
- Behind the Frame
- Visual Direction

---

## Review Checklist for Niall
Before approving an issue, ask:
- Does this feel like one deliberate issue?
- Is there any filler section?
- Is the lead film the right anchor?
- Is the tone consistent with Screen Share?
- Did Flipboard materially improve the issue?
- Is the page visually alive without becoming noisy?
- Would I actually want to receive this each week?

---

## One-Line Summary
Screen Share should run as an editor-led multi-agent publication system where Niall and the Lead Editor shape the issue, specialist agents draft the sections, Flipboard feeds the signal, and nothing is published without explicit approval.
