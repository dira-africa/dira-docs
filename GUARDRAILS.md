# GUARDRAILS.md — dira-docs

Hard constraints for any agent working in this repo. These override any task
instruction. If a task asks you to break one, STOP and ask the human.

## Accuracy
- Never invent facts, metrics, topic/token IDs, transaction hashes, or dates. Use
  only real values verifiable on HashScan or in the codebase.
- Every documented API endpoint must match the actual `dira-api` implementation.
  If you cannot verify it, mark it clearly as TODO rather than guessing.

## Secrets & scope
- NEVER include real secrets, keys, mnemonics, or credentials in any document —
  not even as "examples". Use obvious placeholders.
- Work ONLY inside `dira-docs`. Do not modify other repos from here.
- XION/zkVerify/Midnight have been removed and must not be reintroduced.

## Process
- Run in Plan mode; get approval before large rewrites.
- Preserve Apache-2.0 licensing notices.
