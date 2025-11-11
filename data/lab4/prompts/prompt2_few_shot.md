# Prompt 2 – Few-shot Accessibility Evaluation

## Overview
This prompt demonstrates how the Accessibility Evaluation AI Agent performs an accessibility analysis using a few-shot learning approach.  
The system is first shown multiple (X, y) examples before being asked to predict the output for a new input X.

---

## System Role
You are an **Accessibility Evaluation AI Agent** capable of reasoning over structured web accessibility data.  
Use the previous examples to understand how compliance scores and checklists are generated, then predict the result for the new observation.

---

## Example 1
### Input X₁
```json
{
  "site": "migracija.lt",
  "automated_issues": ["missing captions on one video"],
  "expert_issues": ["skipped heading levels"],
  "user_feedback": ["form feedback messages unclear"]
}
```

### Output y₁
```json
{
  "compliance_score": 0.80,
  "wcag_failures": ["1.2.2 Captions", "1.3.1 Info and Relationships"],
  "developer_checklist": [
    "Add captions for all videos.",
    "Fix heading hierarchy to avoid skipped heading levels.",
    "Improve form validation feedback messages."
  ]
}
```

---

## Example 2
### Input X₂
```json
{
  "site": "education.ec.europa.eu",
  "automated_issues": ["low contrast in footer"],
  "expert_issues": ["ambiguous link text"],
  "user_feedback": ["video without subtitles"]
}
```

### Output y₂
```json
{
  "compliance_score": 0.87,
  "wcag_failures": ["1.4.3 Contrast", "2.4.4 Link Purpose", "1.2.2 Captions"],
  "developer_checklist": [
    "Fix contrast ratio in footer links and small text.",
    "Ensure link text is descriptive and meaningful.",
    "Provide captions/subtitles for all video content."
  ]
}
```

---

## New Input X₃ (to predict)
```json
{
  "site": "delfi.lt",
  "automated_issues": ["missing alt text", "no focus indicator", "carousel traps keyboard"],
  "expert_issues": ["dynamic headlines not announced to screen readers"],
  "user_feedback": ["videos without captions", "unlabeled buttons"]
}
```

---

## Task
Based on the previous examples, infer and generate the output y₃ for this new input.

---

## Expected Output y₃
```json
{
  "compliance_score": 0.15,
  "wcag_failures": [
    "1.1.1 Text Alternatives",
    "2.1.2 No Keyboard Trap",
    "1.4.3 Contrast",
    "1.2.2 Captions"
  ],
  "developer_checklist": [
    "Add alt text to all article and thumbnail images.",
    "Ensure visible focus indicators for all keyboard users.",
    "Fix carousel keyboard navigation traps.",
    "Add captions to news and multimedia videos.",
    "Label all interactive buttons and controls for screen readers."
  ]
}
```

---

## Notes
- The AI agent uses pattern recognition from Examples 1 and 2.  
- Each (X, y) pair demonstrates how the model associates problem types with WCAG failures and derives actionable recommendations.
