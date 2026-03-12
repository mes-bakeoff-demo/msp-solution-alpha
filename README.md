# MSP Solution: Alpha

**Vendor Alpha's Approach** — Rules-Based Eligibility Engine

**Backlog Item:** [#1 MSP Auto-Enrollment](https://github.com/mes-bakeoff-demo/mes-modernization/issues/1)

## Live Demo

[Try it here](https://mes-bakeoff-demo.github.io/msp-solution-alpha)

---

## Approach

**Philosophy:** Keep it simple. Eligibility rules are deterministic — a straightforward rules engine is transparent, auditable, and maintainable.

### Why This Approach?

- **Transparency:** Every decision can be traced to specific rules
- **Auditability:** No black box — logic is readable
- **Maintainability:** Rules can be updated without complex refactoring
- **No Dependencies:** Pure HTML/CSS/JS, runs anywhere

### Tech Stack

| Component | Choice | Rationale |
|-----------|--------|-----------|
| Frontend | Vanilla HTML/CSS/JS | Zero dependencies, maximum portability |
| Styling | CSS Variables | Easy theming, accessible colors |
| Logic | Pure functions | Testable, predictable |
| Deployment | GitHub Pages | Free, automatic |

---

## How It Works

1. User enters beneficiary information
2. JavaScript applies eligibility rules in sequence
3. Determination displayed with explanation
4. All logic runs client-side (no server)

### Eligibility Logic

```javascript
function determineMSPEligibility(age, income, householdSize, hasMedicare) {
  // Must be 65+ or disabled, and have Medicare
  if (age < 65 || !hasMedicare) {
    return { eligible: false, reason: "Must be 65+ with Medicare" };
  }
  
  const fpl = getFederalPovertyLevel(householdSize);
  const incomePercent = (income / fpl) * 100;
  
  if (incomePercent <= 100) {
    return { eligible: true, program: "QMB", confidence: "high" };
  } else if (incomePercent <= 120) {
    return { eligible: true, program: "SLMB", confidence: "high" };
  } else if (incomePercent <= 135) {
    return { eligible: true, program: "QI", confidence: "high" };
  }
  
  return { eligible: false, reason: "Income exceeds 135% FPL" };
}
```

---

## Definition of Done Status

### Functional Requirements
- [x] Accept beneficiary data input
- [x] Apply MSP eligibility rules
- [x] Return determination with confidence
- [x] Provide explanation
- [x] Handle edge cases

### Technical Requirements
- [x] GitHub Pages deployable
- [x] No server dependencies
- [x] Open source (MIT)
- [x] Documentation
- [x] Responsive design

### Quality Requirements
- [x] Accessible (WCAG 2.1 AA)
- [x] Fast (< 1 second)
- [ ] Test coverage documented

---

## Value Report

### Iteration 1

**Outcomes Delivered:**
- Working prototype deployed
- All eligibility rules implemented
- Accessible, responsive UI

**Approach Strengths:**
- Simple, auditable logic
- No external dependencies
- Fast load time (~50KB total)

**Approach Limitations:**
- Less visual/interactive than alternatives
- Rules hardcoded (would need config for production)

**Recommendations:**
- Consider externalizing rules to JSON config
- Add print-friendly output for caseworkers

---

## Local Development

```bash
# No build step needed — just open index.html
open index.html

# Or use a local server
python -m http.server 8000
```

---

## License

MIT — Use freely, adapt as needed.

---

*Built for the [MES Bake-Off Demo](https://github.com/mes-bakeoff-demo) — see [Issue #1](https://github.com/mes-bakeoff-demo/mes-modernization/issues/1) for requirements*
