---
share: true
---
Rich Sutton’s **“The Bitter Lesson”** argues that the most important insight from 70 years of AI research is that **general methods leveraging massive computation** consistently outperform approaches that rely on human knowledge and domain-specific insights. This pattern stems from the continual exponential growth of computational power, making methods that scale with computation—primarily **search** and **learning**—dominant in the long run.

Sutton reviews historical examples across AI fields:

- **Computer Chess:** Early human-knowledge-based strategies gave way to brute-force deep search, culminating in Deep Blue defeating Kasparov in 1997. Researchers relying on human-style reasoning were disappointed as simpler, computation-heavy approaches prevailed.  
- **Computer Go:** After decades of human-centric methods, success came only with large-scale search and self-play learning (e.g., AlphaGo), demonstrating the same shift seen in chess.  
- **Speech Recognition:** 1970s systems using linguistic and phonetic knowledge were surpassed by statistical, computationally intensive methods like Hidden Markov Models, later superseded by deep learning, which depends even less on human input and more on large-scale computation.  
- **Computer Vision:** Early methods relied on handcrafted features (edges, SIFT, generalized cylinders), but modern deep-learning approaches with minimal human-knowledge encoding dramatically outperform them.

The **bitter lesson** is that:

1. AI researchers often try to embed human understanding into systems.  
2. This yields short-term gains and personal satisfaction.  
3. Over time, it plateaus and hinders progress.  
4. Breakthroughs come from general, computation-heavy methods that scale, rendering human-knowledge approaches obsolete.

Sutton concludes that AI should **avoid hardcoding human discoveries** about how we think or perceive. Minds and the world are **too complex** for simple representations. Instead, AI should be designed with **meta-methods—search and learning—that can autonomously discover and approximate the world’s inherent complexity**, allowing systems to scale with ever-increasing computational resources.