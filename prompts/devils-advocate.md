---
description: Adversarial review - get a devil's advocate opinion on a decision or plan using the adversary subagent
---
Use the subagent tool with the single agent "adversary" to produce a rigorous devil's advocate review of: $@

Pass the full context of the decision or plan being reviewed (relevant facts, constraints, alternatives already considered, and any code or files it depends on). Ask it to verify factual claims against the codebase where applicable, and return its structured verdict (steelman, attack, what would change its mind, base rates, and the one unanswered question).

After it responds, present the adversary's verdict to the user and note where the original position should be revised, defended, or tested further. Do not simply agree with either side - weigh the specific evidence the adversary produced.
