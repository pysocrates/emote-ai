#Emote-AI 2.0

### A Minimal Framework for Agent Behavior Using Desire, Anxiety, and Confidence

**Author**: Cory R. Carlson
**Repo**: [github.com/pysocrates/emote-ai](https://github.com/pysocrates/emote-ai)

---

## Concept Update: Emote-AI 2.0

In the original Emote-AI framework, agent behavior was governed by just two emotional primitives:

* **Desire**: Goal-oriented motivation (the "pull" toward outcomes)
* **Anxiety**: Regulatory tension due to uncertainty, failure risk, or external obstacles

In **version 2.0**, we introduce a third primitive:

* **Confidence**: The agent's internal assessment of its ability to succeed based on past outcomes and current situational clarity

---

## Core Primitives

### 1. **Desire**

* Range: 0.0 (disinterest) to 1.0 (compulsion)
* Drives goal pursuit
* Increases when tasks are valuable or pressing

### 2. **Anxiety**

* Range: 0.0 (calm) to 1.0 (panic)
* Rises with uncertainty, obstacles, or repeated failure
* Modulates risk-awareness and caution

### 3. **Confidence** *(new in 2.0)*

* Range: 0.0 (no self-efficacy) to 1.0 (total certainty)
* Increases with successful task execution
* Decreases with failure, interruption, or insufficient feedback

---

## Behavioral Logic Grid

| Desire   | Anxiety  | Confidence | Resulting Behavior                               |
| -------- | -------- | ---------- | ------------------------------------------------ |
| High     | Low      | High       | Direct, assertive pursuit of goal                |
| High     | High     | Low        | Cautious action, fallback planning, info-seeking |
| Low      | Low      | Moderate   | Idle, or minimal energy task-switching           |
| High     | Low      | Low        | Reckless pursuit, may trigger failure loop       |
| Moderate | Moderate | High       | Maintain course, open to adaptation              |

Agents should adjust their behavioral plan dynamically based on shifts in these three state values.

---

## Implementation Sketch

```python
class EmotionLiteAgent:
    def __init__(self):
        self.desire = 0.6
        self.anxiety = 0.2
        self.confidence = 0.7

    def assess_context(self, success, obstacle, feedback):
        # Simulate learning and adaptation
        if success:
            self.confidence = min(1.0, self.confidence + 0.1)
            self.anxiety = max(0.0, self.anxiety - 0.05)
        if obstacle:
            self.anxiety = min(1.0, self.anxiety + 0.1)
            self.confidence = max(0.0, self.confidence - 0.05)
        if not feedback:
            self.confidence = max(0.0, self.confidence - 0.05)

    def choose_behavior(self):
        if self.desire > 0.7 and self.anxiety < 0.4 and self.confidence > 0.6:
            return "Pursue goal directly"
        elif self.anxiety > 0.6 and self.confidence < 0.4:
            return "Fallback plan or request help"
        elif self.desire < 0.3:
            return "Idle or passive state"
        else:
            return "Cautious pursuit with monitoring"
```

---

##  Design Goals

* Maintain **interpretable agent behavior**
* Avoid full emotion simulation while allowing **emotional realism**
* Enable **safe and predictable adaptation** to uncertainty and feedback

---

##  Future Directions

* Incorporate **memory** of prior outcomes to influence confidence decay
* Add optional fourth scalar: *Curiosity* or *Patience*
* Explore agent "mood drift" over time from uneven balance of primitives
* Apply to RL environments with real reward shaping and goal prioritization

---

##  Summary

Emote-AI AI 2.0 expands the original minimal framework by introducing **confidence** as a third scalar, giving agents the ability to adjust behavior based on self-assessed capability in dynamic environments. The goal remains clarity, safety, and low-complexity control over behavioral logic for intelligent agents in alignment-critical contexts.
