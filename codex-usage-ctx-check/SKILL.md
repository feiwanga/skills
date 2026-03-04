---
name: codex-usage-ctx-check
description: Check OpenClaw codex API usage/quota and session context usage. Use when user asks about 用量, api用量, API用量, 额度, 剩余额度, 还剩多少额度, usage, quota, or asks about 上下文, 上下文使用, 上下文占用, 会话上下文, ctx, context, context usage, Tokens (ctx %), token占用.
---

# Intent routing
- If the request matches usage/quota keywords, run the Usage flow.
- If the request matches context/ctx keywords, run the Context flow.
- If both match, run both flows and return two lines: usage first, context second.

# Usage flow
1. Run `openclaw models status`.
2. Extract a line starting with `openai-codex usage:`.
3. If missing, run `openclaw models status` again until found, with a maximum of 3 total attempts.
4. If still missing after 3 attempts, return exactly: `没有usage`.
5. Return only the extracted usage line (no extra text).

# Context flow
1. Run `openclaw sessions`.
2. In the output table, select the first data row under the header (this is the newest session, with age closest to now such as `just now` or `1m ago`).
3. From that row, extract the `Tokens (ctx %)` value in shape like `167k/272k (61%)` (also allow decimal form like `9.8k/272k (4%)`).
4. Return only that extracted value (no extra text).

# Output rules
- Do not add explanation, labels, or punctuation.
- Return exact target fragment(s) only.
