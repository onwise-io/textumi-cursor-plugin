---
name: textumi
description: Check a text for AI-writing signals or rewrite an English draft so it reads as written by a person, with the Textumi MCP tools. Use when the user asks whether a text sounds AI-written, asks to humanize, de-AI or naturalize prose (README, docs, release notes, blog posts, emails), or asks about their Textumi allowance.
---

# Textumi

Textumi's tools come from the `textumi` MCP server of this plugin. In approval prompts Cursor shows it as `plugin-textumi-textumi`.

## When to use

- The user asks whether a text reads as AI-written, or asks for an AI-detector score: call `detect_ai_text`.
- The user asks to humanize, de-AI or rewrite an English text so it sounds natural: call `humanize_text`.
- The user asks what is left of their Textumi plan: call `get_account`.

Do not send texts to Textumi on your own initiative. Use it only for the text the user points to.

## Check a text

1. Call `detect_ai_text` with the text exactly as the user gave it. `language` defaults to `auto`.
2. Report the score (0–100) and the label. Say plainly that the score is an uncalibrated signal, not a probability and not proof of authorship.

## Rewrite a text

`humanize_text` accepts English text of 50 to 2,000 words. Textumi writes the drafts and checks numbers, links and length; you review the meaning.

1. Call `humanize_text` with the text exactly as the user gave it (plain text; blank lines separate paragraphs).
2. When the status is `review_needed`, follow the returned `instructions` for every task: compare each draft with its original and answer with one JSON object per task.
3. Send all answers with `humanize_continue`. If an answer is refused, fix its format as the hint says and send it again.
4. If the status is `running`, call `humanize_status` with the same `job_id`.
5. Repeat until the status is `completed` or `failed`.
6. Give the user the returned text unchanged. Do not edit, shorten or "improve" it.

Only one rewrite per account runs at a time. If the user no longer needs one, call `humanize_cancel`. A request counts toward the allowance once its first review tasks are returned, even if it is not finished.

## When something is refused

- Not signed in: ask the user to finish the Textumi sign-in that Cursor opens in the browser.
- The plan does not include work through an assistant, or the allowance is used up: tell the user the message returned by the tool and point them to https://textumi.com/pricing.
- Never claim a rewrite will pass any particular detector.
