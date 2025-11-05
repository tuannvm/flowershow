---
share: true
---

Anthropic published a technical postmortem on September 17, 2025, detailing three infrastructure bugs that intermittently degraded the response quality of Claude between early August and early September. The company emphasized that model quality is never intentionally reduced due to demand or server load; the incidents were caused solely by infrastructure errors.  

### Key Events and Findings
- **Investigation Trigger:** Initial user reports of degraded responses began in early August and escalated by late August, prompting a full investigation.  
- **Three Overlapping Bugs:**  
  1. **Context Window Routing Error (Aug 5 – Sept 18):**  
     - Some Sonnet 4 requests were misrouted to 1M-token context servers, peaking at 16% of traffic on Aug 31.  
     - Sticky routing caused repeated degraded responses for affected users.  
     - Fixed by correcting routing logic, fully deployed by Sept 18 across platforms.  
  2. **Output Corruption (Aug 25 – Sept 2):**  
     - Misconfiguration on TPU servers led to occasional nonsensical tokens, such as Thai characters in English responses.  
     - Affected Opus 4.1, Opus 4, and Sonnet 4 on the Claude API; third-party platforms unaffected.  
     - Resolved by rolling back the change and adding detection tests.  
  3. **Approximate Top-k XLA:TPU Miscompilation (Aug 25 – Sept 12):**  
     - A compiler precision bug caused token selection errors, sometimes dropping the most probable token.  
     - Impacted Haiku 3.5 and possibly Sonnet 4 and Opus 3.  
     - Fixed by reverting to exact top-k with enhanced fp32 precision and coordinating with XLA:TPU engineers.  

### Root Cause Complexity
- The bugs were hard to detect due to:  
  - Distributed model serving across AWS Trainium, NVIDIA GPUs, and Google TPUs.  
  - Privacy constraints limiting access to user interactions for debugging.  
  - Noisy evaluation metrics and inconsistent user-visible symptoms.  
- The XLA:TPU compiler bug was particularly elusive, triggered only under specific model configurations and batch sizes, with inconsistent reproduction.

### Improvements and Preventive Measures
- **More sensitive, production-level quality evaluations** to detect subtle degradations.  
- **Continuous monitoring on live systems** to catch platform-specific issues like routing errors.  
- **Enhanced debugging tools** that respect privacy but speed up problem isolation.  
- **Switch to exact top-k computations** despite minor efficiency tradeoffs to ensure response quality.  

Anthropic encourages users to continue submitting direct feedback, which remains vital to diagnosing and preventing similar issues.
Anthropic published a detailed postmortem on three infrastructure bugs that intermittently degraded Claude’s response quality between August and early September 2025. The company emphasized that model quality was never reduced due to demand or server load, and the issues stemmed solely from infrastructure problems.  

**Overview of Incidents:**  
1. **Context Window Routing Error (Aug 5 – Sep 18)**  
   - Some Sonnet 4 requests were misrouted to servers configured for a 1M-token context window.  
   - Initially affected 0.8% of requests, rising to 16% after a load balancing change on Aug 29.  
   - Misrouting particularly impacted Claude Code users due to “sticky” routing.  
   - Fully fixed across all platforms by Sep 18.  

2. **Output Corruption (Aug 25 – Sep 2)**  
   - Misconfiguration on TPU servers led to rare, high-probability selection of nonsensical tokens (e.g., random Thai or Chinese characters in English responses).  
   - Affected Opus 4/4.1 and Sonnet 4 only on the Claude API; third-party platforms were unaffected.  
   - Rolled back by Sep 2, with new tests added to catch unusual outputs.  

3. **Approximate Top-k XLA:TPU Miscompilation (Aug 25 – Sep 12)**  
   - A change to token selection exposed a latent XLA TPU compiler bug, causing incorrect probability calculations for certain models.  
   - Impacted Haiku 3.5 and likely some Sonnet 4 and Opus 3 users.  
   - Fixed via rollbacks, switching to exact top-k sampling, and collaborating with the XLA:TPU team on a long-term fix.  

**Detection Challenges:**  
- Symptoms varied across platforms and models, creating confusing and inconsistent reports.  
- Standard evaluations and canary deployments did not capture the degradations, partly because Claude often recovered from isolated errors.  
- Privacy protections limited engineers’ ability to directly examine problematic user interactions.  

**Improvements Implemented:**  
- **More sensitive and continuous evaluations** to better detect subtle quality drops.  
- **Expanded monitoring on true production systems** to catch platform-specific issues.  
- **Faster and privacy-conscious debugging tools** to respond more quickly to user feedback.  

Anthropic acknowledged the crucial role of direct community feedback in diagnosing the issues and encouraged continued user reporting via in-app tools or email. The company reaffirmed its commitment to maintaining consistent, high-quality model outputs and improving infrastructure reliability.