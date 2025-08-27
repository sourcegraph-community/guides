# **How to Best Prompt Amp**

*A practitioner’s guide to turning an AI agent into your most reliable teammate*



## **1. Think of Amp as a *Senior* Engineer, Not a Search Box**

Amp is not Chat-GPT with a code index bolted on. \
It is an **agent** that can:



* read your repo
* open your editor
* run tests, migrations, or even deploy
* remember every step in a thread (and resume later)

Therefore, the first rule is: **prompt *tasks*, not *questions***.



```
❌ "What is the AutoScroller doing?"
✅ "Open AutoScroller.ts, summarise its responsibilities, and draw me a Mermaid diagram that shows the data flow to ViewUpdater."
```




## **2. The Four-Layer Prompt Formula**

`Role` + `Context` + `Task` + `Exit Criteria`


<table>
  <tr>
   <td><strong>Layer</strong></td>
   <td><strong>Example</strong></td>
  </tr>
  <tr>
   <td><strong>Role</strong></td>
   <td>“Act as a senior React engineer who cares about accessibility.”
   </td>
  </tr>
  <tr>
   <td><strong>Context</strong>
   </td>
   <td>“We are on a Next 14 / TypeScript / Tailwind monorepo. The staging URL is https://staging.example.com.”
   </td>
  </tr>
  <tr>
   <td><strong>Task</strong>
   </td>
   <td>“Refactor the <code>UserList</code> component so that keyboard navigation works with arrow keys and screen-reader labels are correct.”
   </td>
  </tr>
  <tr>
   <td><strong>Exit Criteria</strong>
   </td>
   <td>“Finish with two artifacts: 1) a working branch, 2) a deployable that can be pushed to production.”
   </td>
  </tr>
</table>


Copy-paste the template, change the variables, and you’ll rarely get a vague answer.


## **3. Keep It Atomic: One Thread = One Deliverable**

Amp keeps an ever-growing history inside every chat. If you keep piling unrelated tasks into the same thread, later prompts get diluted by earlier noise, and you’ll hit the context-size ceiling sooner.

The fix is to treat each logical deliverable as its own **fresh chat**. Open one chat for the initial spike, another for the refactor, a third for the deployment pipeline, and so on.

Amp also gives you two built-in tools to stay tidy when a single deliverable is still too big:


## **4. Deep-dive: The oracle & Subagents**

Use these tools to keep your main thread tidy by handling tasks that are too heavy or repetitive for the default agent.

**4.1. The oracle – The “Senior Staff Engineer on Call”**

A powerful, read-only agent for deep analysis. Use it for complex bug hunts, architectural reviews, or strategic planning.


* **Prompt Pattern:** Use the oracle to `<goal>`. Be concise and return only the key findings.
* **Pro-tip:** Because the oracle is slower, add “summarise in ≤5 bullets” to your prompt.

<table>
  <tr>
   <td><strong>Purpose</strong></td>
   <td><strong>Exact Prompt</strong></td>
  </tr>
  <tr>
   <td><strong>Regression check</strong>
   </td>
   <td>“Use the oracle to review the last commit’s changes and confirm the idle-notification audio logic is unchanged.”
   </td>
  </tr>
  <tr>
   <td><strong>Refactor design</strong>
   </td>
   <td>“Ask the oracle to analyse <code>"foobar"</code> and <code>"barfoo"</code>, find duplication, and propose a backwards-compatible refactor.”
   </td>
  </tr>
  <tr>
   <td><strong>Bug hunt</strong>
   </td>
   <td>“I’m getting <code>"TypeError: Cannot read properties of undefined"</code> when I run <code>"npm run dev"</code>. Use the oracle as much as possible to find the root cause.”
   </td>
  </tr>
</table>


**4.2. Subagents – The “Parallel Interns”**

Lightweight agents that run tasks in parallel, each with a fresh context. Ideal for work that can be split into independent chunks, like converting batches of files or adding tests to multiple modules.



* **Prompt Pattern:** Spawn one subagent per &lt;unit-of-work>. Give each the same exit checklist.
* **Pro-tip:** Subagents can’t talk to each other. If tasks need to be coordinated, use the main agent or Oracle.

<table>
  <tr>
   <td><strong>Purpose</strong></td>
   <td><strong>Exact Prompt</strong></td>
  </tr>
  <tr>
   <td><strong>Batch refactor</strong>
   </td>
   <td>“Convert these 5 JavaScript files to TypeScript. Spawn one subagent per file. Each should: add strict types, fix lint errors, and write a short JSDoc summary.”
   </td>
  </tr>
  <tr>
   <td><strong>Test generation</strong>
   </td>
   <td>“For every public method in UserService, spawn a subagent to create a Jest test that covers happy-path + two edge cases.”
   </td>
  </tr>
  <tr>
   <td><strong>Migration scripts</strong>
   </td>
   <td>“Generate reversible SQL migrations for each table mentioned in the diff. Use a subagent per table and return only the final SQL.”
   </td>
  </tr>
</table>


By combining fresh chats for top-level deliverables with subagents or Oracle for internal branching, you keep every conversation laser-focused and easy to revisit or share.


## **5. Give Amp *Executable* Feedback Loops**

Instead of “make it faster,” tell Amp *how* to measure success.


```
✅ "Run npm run bench:render and tell me the median frame time. If it's above 16 ms, try memoising ExpensiveChart."
✅ "Use the Playwright MCP, screenshot /dashboard, and ensure the cumulative layout shift is < 0.1."
```


Amp can invoke tools; the clearer the command, the faster the iteration.


## **6. Adopt a Workflow Mindset (flexible, not rigid)**

Approach your work in the same sequence great teams already follow:


<table>
  <tr>
   <td><strong>Phases</strong></td>
   <td><strong>Typical Prompt Starter</strong></td>
  </tr>
  <tr>
   <td><strong>PLAN</strong>
   </td>
   <td>“Analyse the codebase and list the top three tech-debt risks.”
   </td>
  </tr>
  <tr>
   <td><strong>BUILD</strong>
   </td>
   <td>“Generate unit tests for the uncovered paths in <code>auth.ts</code>.”
   </td>
  </tr>
  <tr>
   <td><strong>DEPLOY</strong>
   </td>
   <td>“Create a canary deployment plan that rolls out to 5 % of traffic first.”
   </td>
  </tr>
  <tr>
   <td><strong>SUPPORT</strong>
   </td>
   <td>“Scan the last 7 days of logs for error spikes and open a Linear ticket for each new pattern.”
   </td>
  </tr>
</table>


These labels are **guidelines, not handcuffs**. Feel free to:

* break a single phase into smaller sub-phases (e.g., split BUILD into “refactor”, “type-check”, “tests”);
* merge phases when the change is trivial (e.g., a one-line bug fix may skip PLAN and jump straight to BUILD + DEPLOY);
* rename or reorder phases to match your team’s rituals (Shape-Up, Kanban, Git-Flow, etc.).

The goal is a shared vocabulary that keeps everyone aligned, while still letting you adapt the flow to the size, risk, and style of the actual task.


## **7. Leverage MCP Servers for Superpowers**

Amp can talk to *anything* that exposes a [Model Context Protocol](https://modelcontextprotocol.io/) server: Docker, AWS, Stripe, Slack, Postgres…

**Mini-cookbook:**

* `"With the Docker MCP, build a multi-stage image for the Next.js app and push it to ghcr.io."`
* `"With the AWS MCP, spin up an RDS Postgres 15 instance in the staging VPC and print the connection string."`

If a tool exists, you can prompt Amp to drive it.



## **8. Guardrails & Security Prompts**

A single prompt can drop tables *and* open a PR. \
Add guardrails explicitly:

*“Always validate user input before database operations.”*

*“Before running destructive SQL, ask for confirmation.”*

**Secret Protection Built-In:** Amp automatically detects and redacts secrets before they reach the LLM or get stored anywhere. When found, secrets are replaced with descriptive markers like [REDACTED:aws-access-key-id], protecting API keys, tokens, and credentials without any manual intervention required.

You can even create an `AGENTS.md` file at repo root that Amp reads automatically:

Amp follows it like a contributing guide. \
 \
*For complete details on Amp's secret redaction capabilities, see the* [Amp Security Reference](https://ampcode.com/security#secret-redaction).


## **9. Thread Re-use & Knowledge Hand-off**

Need to loop in a teammate?

*“Share this debugging thread with <code>@alice</code> in Slack channel #frontend, and create a Linear ticket linking the thread URL.”*

Amp’s thread history is portable; you never have to paste Slack screenshots again.


## **10. Common Anti-patterns (and Quick Fixes)**


<table>
  <tr>
   <td><strong>Anti-pattern</strong></td>
   <td><strong>Fix</strong></td>
  </tr>
  <tr>
   <td>Wall-of-text prompt
   </td>
   <td>Break into numbered sub-tasks.
   </td>
  </tr>
  <tr>
   <td>“Make it better”
   </td>
   <td>Provide metric or acceptance criteria.
   </td>
  </tr>
  <tr>
   <td>Mixing languages mid-thread
   </td>
   <td>Stick to one language per thread (or explicitly switch).
   </td>
  </tr>
  <tr>
   <td>Forgetting context
   </td>
   <td>Tell Amp to “re-read <code>AGENTS.md</code>” if it drifts.
   </td>
  </tr>
</table>


## **11. Copy-Paste Starter Prompts**

Below are 100 % ready snippets you can paste into Amp today.


### **PLAN**

```
You are a staff engineer.  
Context: React monorepo, PNPM workspaces.  
Task: Identify every usage of the legacy `useAxios` hook and draft a migration plan to React Query.  
Exit criteria: Markdown file `MIGRATION-useAxios.md` with timeline, risk, and rollback steps.
```

### **BUILD**

```
Refactor `UserCard.jsx` to TypeScript, add JSDoc, and achieve 100 % branch coverage with Jest.  
Before/after screenshots via Playwright MCP.  
Open a PR titled “refactor(UserCard): migrate to TS + tests”.
```

### **DEPLOY**

```
Create a GitHub Action workflow that deploys to Vercel on every push to 
`develop`and runs Cypress e2e against the preview URL.
```

### **SUPPORT**

```
Scan all `*.log` files in `/var/log/app` created in the last 7 days.  
Generate a CSV of top 10 error messages, then open a Linear ticket for each new pattern.
```

## **Final Thought**

Prompting Amp is less about “AI magic” and more about **project management with a very fast senior partner**. \
Give it **clear goals, guardrails, and feedback loops**, and it will ship code faster than any intern you’ve ever had.

Happy prompting!

*For more information about Amp, please visit the *[Amp Homepage](https://ampcode.com).