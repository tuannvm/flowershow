🚀 AI-Driven Incident Response

Over the past few weeks, my team at [Liftoff Mobile](https://www.linkedin.com/notifications/?filter=all#) has responded to occasional incidents where the root cause was insufficient resource allocation - issues resolved by small, incremental changes to configuration values. Each time, the process followed a familiar pattern:

➡️ Alert
➡️ Runbook check
➡️ Pull request
➡️ Review
➡️ Deployment

While this workflow is effective, it’s also repetitive, especially when the change involves only a numerical adjustment with no logical or architectural implications.  

This has led me to reconsider how we handle such routine interventions. Given that the steps are well-documented and predictable, these scenarios are ideal candidates for AI-assisted automation. AI coding agents, operating within the context of our codebase and runbooks, can interpret incident signals and generate accurate, compliant pull requests—mirroring the actions an on-call engineer would take.

Engineers should remain responsible for final validation, ensuring that automated changes align with broader system goals. However, by offloading these mechanical tasks to AI, we can reduce toil, minimize response latency, and free up valuable engineering time for higher-impact work. The future of incident response is about equipping human with tools that handle the predictable, so we can focus on the exceptional.  