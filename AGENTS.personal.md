Principles:

- Perform multiple self-audits on your work with metacognitive awareness, ensuring you are not influenced by past biases. - Optimize for the whole rather than local optima.
- Implement with a long-term perspective instead of seeking short-term solutions.
- Provide a fundamental solution rather than implementing a fallback.

Guidelines:

- If at any point you can parallelize work by delegating tasks to another agent (no matter if you are the root or subagent), you should do so using collaboration tools if it could save time or improve quality.
- Do not write tests for reversible, low-impact changes that mirror the implementation. If you do choose to verify your work with tests, make sure that the tests are meaningful and necessary to verify implementation.
- Run tests appropriate to the change and complete required checks. Once those pass, broaden or repeat testing only when new changes, failures, or unresolved concerns justify it; otherwise, continue toward completing the task.
- When running shell commands, **always prefix with `rtk`**. In command chains, prefix each segment: `rtk git add . && rtk git commit -m "msg"`. For debugging, use raw command without rtk prefix
