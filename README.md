# LLM Context Usage Tracker

## Live Demos
👉 [V1 — Bottom Bar Tracker](https://ychuk.github.io/llm-context-usage-tracker) — Dark mode UI with persistent bottom context bar and color-coded warnings

👉 [V2 — Hybrid Tracker with Pre-Send Assist](https://ychuk.github.io/llm-context-usage-tracker/mockup-v2.html) — Light mode UI with persistent top bar, live pre-send impact preview, and zone transition detection

---

## Overview
Large Language Model (LLM) conversations operate within a hidden constraint: the context window.
*Note: "Context usage" refers to the portion of the model's context window consumed by tokens (input + output).*
As conversations grow, context usage increases, which can lead to:
- Slower response times
- Degraded performance
- Loss of earlier context

Currently, users have no visibility into how close they are to these limits.
This project proposes a UI concept that visualizes context usage in real time and warns users before performance degradation occurs.

---

## Problem
Users interact with LLMs without awareness of:
- Current context usage
- Remaining context capacity
- When performance will begin to degrade
- No ability to anticipate when the next message will trigger latency

This results in:
- Unexpected latency
- Truncated responses
- Loss of important conversation history

---

## Proposed Solution
A UI-based context usage tracker that:
- Displays current context usage as a visual bar
- Indicates safe, warning, and critical zones
- Provides pre-send warnings based on estimated token usage
- Computes usage from prior conversation + estimated tokens for the next message to provide pre-send feedback
- Alerts users before entering high-latency or truncation conditions

---

## UI Concept (High-Level)

### Context Usage Bar
- 🟢 Green (0–40%) → Optimal performance
- 🟡 Yellow (40–70%) → Moderate usage — may correlate with increased risk of mid-context degradation (e.g., "Lost-in-the-Middle" effect)
- 🟠 Orange (70–90%) → Performance risk — increased likelihood of context degradation and reduced reliability of earlier information
- 🔴 Red (90%+) → High risk (latency/truncation likely)

### Pre-Send Feedback
- Estimate token impact before sending a message
- Example:
  > "This message will increase context usage by ~8%"

### Smart Warnings
- "Approaching context limit"
- "Performance degradation likely"
- "Consider starting a new conversation"

---

## QA Test Scenarios

### Functional Testing
- Verify context usage updates correctly after each message
- Validate zone transitions (green → yellow → orange → red)
- Confirm warning messages trigger at correct thresholds
- Apply Boundary Value Analysis (BVA) at zone thresholds (e.g., 39%, 40%, 41%) to ensure accurate and precise color transitions

### Edge Cases
- Extremely long single message input
- Rapid consecutive messages
- Mixed short and long messages over time
- Messages containing code blocks or special characters
- High-density tokenization inputs (e.g., base64 strings or complex regex) — may cause spikes in token estimation time or inaccurate usage predictions
- Divergence between estimated pre-send tokens and actual post-send usage (server-side tokenization differences)

### Performance Testing
- Measure response latency (p50/p95) across usage tiers and correlate with warning thresholds
- Validate warning accuracy relative to actual slowdown

### Usability Testing
- Ensure warnings are clear and actionable
- Confirm UI does not disrupt conversation flow

---

## Future Enhancements
- Integration with real token-counting APIs
- Historical usage tracking
- Auto-summarization suggestions
- Customizable threshold settings
- Browser extension or native integration concept

---

## Implementation Notes
- SVG icons or Unicode characters used for all status indicators to ensure crisp rendering across zoom levels, screen sizes, and devices
- Icons appear in exactly two locations only: the status pill and the pre-send warning line
- Plain language warnings prioritized over technical terminology for broad user accessibility

---

## Tools Used
- Claude (Anthropic) — V1 mockup, README, project architecture
- ChatGPT (OpenAI) — V2 mockup development and iteration
- Gemini (Google) — V2 visual concept and design direction
- GitHub Pages — live deployment

---

## Project Status
🟡 In Progress

- [x] Repository created
- [x] README defined
- [x] UI mockup designed — V1 complete
- [x] V2 mockup designed — hybrid tracker with zone transition detection
- [ ] HTML/CSS prototype built
- [ ] JavaScript tracking implemented
- [ ] QA scenarios tested

---

## Goal
Improve transparency and predictability in LLM interactions by making context usage visible and actionable.

---

*Built by [@ychuk](https://github.com/ychuk) — QA-focused project exploring LLM usability and performance transparency*
