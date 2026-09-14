# Copilot mode (AI + developer)

**Mode 3:** you and an agent share **one** Glint Web board. The agent does not open a second editor.

## How pairing works

1. You open the editor (your project already loaded).
2. Click **Allow agent** - you get a short **board code** (e.g. `K7MP`). The tab title becomes `[Glint K7MP] …`.
3. Tell your agent: *use Glint board K7MP* (or paste the code).
4. The agent attaches with MCP `glint_editor_*` (or CDP / CLI) - it must **not** open a new Glint URL.
5. Watch the **agent cursor** move frame-to-frame; hit **Pause** anytime; **Close** (X) to disconnect.

Allow agent stays on across reload / hot refresh until you **Pause** (agent blocked) or **Close** (pair cleared). Closing the browser tab also clears it.

**Board pass:** one source frame’s transform is applied across the board left→right (shared scale/angle), so every screenshot updates in sequence under the agent cursor.

**MCP (preferred):** `glint_editor_list_boards`, `glint_editor_state`, `glint_editor_dispatch`, `glint_editor_board_pass`.

Chrome CDP required:

```bash
google-chrome --remote-debugging-port=9222 --user-data-dir=/tmp/glint-chrome-debug
# optional CLI from Glint-Web:
node scripts/copilot-attach.mjs --pair K7MP
```

If you have many tabs open: only boards with **Allow agent** on are attachable. Focused tab sorts first. If several are allowed, the agent uses your board code.

## Manual vs Headless vs Copilot

| Mode | What happens |
|------|----------------|
| **Manual** | You edit alone - leave Allow agent off |
| **Headless** | Agent builds ZIP offstage - no live board |
| **Copilot** | Agent drives **your** open board - you watch / take over |

## Agent tips

1. Prefer MCP: `glint_editor_list_boards` → `glint_editor_state` / `dispatch` / `board_pass`
2. Or in-page: `__GLINT_COPILOT__.listBoards()` / tab title `[Glint CODE]`
3. Confirm board with `isThisBoard` / MCP pairCode before mutating
4. On Pause / `stale_generation`, re-read state - do not open a new tab

## Related

- [Editor modes](../reference/editor-modes.md)
- [AI workflow](ai-workflow.md)
- [Glint-MCP](https://github.com/GlintShot/Glint-MCP)
