# Copilot mode (AI + developer)

**Mode 3:** you and an agent share **one** Glint Web board. The agent does not open a second editor.

## How pairing works

1. You open the editor (your project already loaded).
2. Click **Allow agent** - you get a short **board code** (e.g. `K7MP`). The tab title becomes `[Glint K7MP] …`.
3. Tell your agent: *use Glint board K7MP* (or paste the code).
4. The agent attaches to **that tab** via `window.__GLINT_COPILOT__` / browser tools - it must **not** open a new Glint URL.
5. Watch live edits; hit **Pause** anytime; export when done.

If you have many tabs open: only boards with **Allow agent** on are attachable. Focused tab sorts first. If several are allowed, the agent uses your board code.

## Manual vs Headless vs Copilot

| Mode | What happens |
|------|----------------|
| **Manual** | You edit alone - leave Allow agent off |
| **Headless** | Agent builds ZIP offstage - no live board |
| **Copilot** | Agent drives **your** open board - you watch / take over |

## Agent tips

1. Call `__GLINT_COPILOT__.listBoards()` or match tab title `[Glint CODE]`
2. Confirm `__GLINT_COPILOT__.isThisBoard('CODE')` before dispatching
3. Pass `pairCode` (or token) on every `dispatch`
4. On Pause / `stale_generation`, re-read state - do not open a new tab

## Related

- [Editor modes](../reference/editor-modes.md)
- [AI workflow](ai-workflow.md)
- [Glint-MCP](https://github.com/GlintShot/Glint-MCP)
