# Spaced Repetition System (SRS)

This document discusses the specific algorithm for SRS used in this application.

1. Memory of an item decays exponentially over time.
2. Right on the verge of forgetting, rate of forgetting slows


1. Stability ($S$)
2. Difficulty ($D$)
- Calculated based on the JLPT level
3. Retrievability ($0 \leq R \leq 1$)
- Probability of recalling item right now
- $R(t) = \exp(-\frac{t}{S})$