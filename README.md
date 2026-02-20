# Goal-Mode

Goal-aware browsing assistant that receives structured JSON requests from a browser extension orchestrator and returns structured JSON responses. It generates concise evaluation criteria, analyzes pages for criteria coverage, persists session state, and produces brief wrap-ups.

**Features**
- Dynamic goal-aware analysis: generate criteria, evaluate pages, update criteria, resume goals, and create session wrap-ups.
- Workspace persistence: every operation persists state into the workspace (session, criteria, events, wrap-ups).
- Structured JSON API: integrates with a browser extension using strict request/response JSON.
- Guardrails for reliability: coverage caps, confidence scores (0.0–1.0), concise findings, and non-fabrication.

**Critical rule**
- Final operation responses must be exactly one raw JSON object (no markdown fences or extra prose). See `goal-mode/SKILL.md` for full execution rules.

**Execution model (summary)**
1. Validate `operation` and required input.
2. Read the matching reference file in `goal-mode/references/` and `goal-mode/references/schemas.md`.
3. Compute the JSON result in memory.
4. Execute all required workspace `write` operations (persist session state and event files).
5. After all persistence completes, output the single JSON object as the final response.

**Workspace layout**
```
/home/ubuntu/.openclaw/workspace/
	goal-mode/
		active-goal.json
		{goal_slug}/
			session.json
			criteria.json
			wrap-up.json
			events/
				{timestamp}-evaluate-page.json

	memory/goal-mode/
		active-session.md
		latest-session.md
		history.md
```

**Supported operations**
- `generate_criteria` — produce a concise, specific criteria list for a goal.
- `evaluate_page` — score a page against criteria and emit an immutable event file.
- `update_criteria` — modify criteria and persist snapshots.
- `create_wrap_up` — produce a concise session summary and recommendation (or `null`).
- `resume_goal` — restore an active goal/session from workspace state.

**Quick start / usage**
- Read the full skill spec: [goal-mode/SKILL.md](goal-mode/SKILL.md)
- Reference operation behavior: `goal-mode/references/`
- Workspace root used by the skill: `/home/ubuntu/.openclaw/workspace/`

If you'd like, I can add example JSON requests for each operation and a small test harness to exercise the skill locally.

Goal-aware browsing assistant that generates checklists, evaluates page relevance, produces session wrap-ups, and persists session data to the workspace.

Features:
- Dynamic goal-aware analysis: generates criteria, evaluates pages, updates criteria, resumes goals, and creates wrap-ups.
- Strict execution model with required workspace persistence for all operations.
- Integrates with a browser extension using structured JSON requests and responses.

Quick links:
- Full skill spec: [goal-mode/SKILL.md](goal-mode/SKILL.md)
- Operation reference files: [goal-mode/references/](goal-mode/references/)

Supported operations:
- `generate_criteria`
- `evaluate_page`
- `update_criteria`
- `create_wrap_up`
- `resume_goal`

Note: The skill requires returning exactly one raw JSON object as the final output (no markdown fences or extra prose). See the full details in the skill spec above.
