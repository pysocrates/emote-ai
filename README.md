# Emotion-Lite AI: A Minimalist Framework for Emotion-Driven Agents

## 🚧 Concept Overview

This repo presents a conceptual model for designing AI agents driven by **only two emotional primitives**:

- **Desire** – the pursuit of goals or rewards
- **Anxiety** – the tension or urgency caused by obstacles, uncertainty, or the risk of failure

The thesis is simple:

> Human behavior—and by extension, AI agent behavior—can be effectively modeled by desire constrained by anxiety. Anger, frustration, sadness, and other complex emotions may be unnecessary for functional intelligence or adaptive behavior.

---

## 💡 Core Idea

### Traditional Emotional AI:
- Attempts to simulate a wide range of human emotions (joy, anger, sadness, empathy)
- Is complex, hard to control, and often unnecessary outside of high-social-fidelity use cases

### Emotion-Lite AI:
- Defines an agent’s **emotional state as a scalar or bounded range**, constrained to a tension between goal pursuit and obstacle awareness
- Uses **anxiety** as a dynamic internal signal to trigger planning shifts, caution, retries, or abandonment
- Maintains **desire** as a driving force behind decision-making, exploration, and goal-directed behavior

---

## 🧠 Design Outline

```python
class EmotionLiteAgent:
    def __init__(self):
        self.desires = []          # List of goals
        self.anxiety = 0.0         # Scalar, 0.0 = calm, 1.0 = panic
        self.emotion_state = "engaged"  # Or "cautious", "hesitant", etc.

    def evaluate_environment(self, stimuli):
        if stimuli.obstacle:
            self.anxiety += 0.1
        if stimuli.progress:
            self.anxiety = max(0.0, self.anxiety - 0.05)

    def plan_behavior(self):
        if self.anxiety < 0.3:
            return plan_direct_action(self.desires)
        elif self.anxiety < 0.7:
            return plan_with_fallbacks(self.desires)
        else:
            return retreat_or_request_help()
