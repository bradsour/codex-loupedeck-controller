# Research and design rationale

Research was performed on 2026-07-20 and checked against the installed Codex application where possible.

## Codex workflow

The official Codex command reference was the source of truth for direct shortcuts such as new/quick chat, search, folder opening, review, panels, terminal, sidebar, dictation, and shortcut help: [Codex commands and keyboard shortcuts](https://learn.chatgpt.com/docs/reference/commands). The installed bundle confirms the Dictation command ID `composer.startDictation` with default `Ctrl+Shift+D`; the profile also assigns it explicitly in `keybindings.json`. Physical testing confirmed that this command behaves as push-to-talk and listens only while the shortcut is held. Loupedeck's atomic shortcut action cannot mirror that hold/release lifecycle, so its Dictate controls use toggle-style Windows Voice Typing (`Win+H`). The reference does not document a Codex Voice Mode shortcut, and `Ctrl+Shift+V` performs paste-as-plain-text in this build.

The installed Codex `app.asar` was also inspected. It confirms that `Continue in new chat` (`forkThread`) and `Copy as Markdown` (`copyConversationMarkdown`) are configurable shortcut commands but are not Command Menu entries in this Windows build. `Copy as Markdown` is explicitly described as a Keyboard Shortcuts settings row, and `forkThread` has application shortcut scope without the `commandMenu` flag. Reasoning increase/decrease/cycle, Plan mode, and Fast mode use the same direct-shortcut approach. The validator checks all eight command IDs and rejects unsupported Command Menu automation.

## Codex Micro inspiration

OpenAI and Work Louder describe Codex Micro around common Codex actions, voice, agent status, a reasoning control, a touch sensor, a rotary encoder, and a joystick. This profile translates that physical hierarchy to the larger CT: always-available reasoning controls, task/agent navigation, voice, common commands, and distinct mode pages. See [OpenAI × Work Louder: Codex Micro](https://openai.com/es-419/supply/co-lab/work-louder/).

Contemporary coverage also emphasized customization, push-to-talk, reasoning adjustment, and agent-status feedback. It raised the risk of overly easy physical approval, which informed the deliberate omission of an approval button: [Axios overview of Codex Micro](https://www.axios.com/2026/07/15/openai-keyboard-codex-agents) and [TechRadar explainer](https://www.techradar.com/ai-platforms-assistants/openai/what-is-the-codex-micro-openais-first-hardware-gadget-explained).

## Loupedeck CT structure

Loupedeck documents the CT as having six dials, 12 touchscreen buttons, a center wheel, eight round buttons including Home, and 12 square buttons. Its guidance treats touch pages as context-specific workspaces while round and square buttons suit broadly available actions. Those constraints drove the four 12-control pages, persistent dial layout, numbered workspace keys, and global round-button shortcuts: [CT control elements](https://support.loupedeck.com/control-elements-ct.html), [touch buttons](https://support.loupedeck.com/touch-buttons.html), [round and square buttons](https://support.loupedeck.com/round_and_square_buttons.html), [wheel](https://support.loupedeck.com/wheel.html), and [pages](https://support.loupedeck.com/pages.html).

The Commands page, wheel, and custom dial glyphs use the Lucide icon language used by shadcn/ui. Commands uses SquarePen, MessagesSquare, MessageCirclePlus, Search, FolderOpen, Command, PanelRight, SquareTerminal, PanelBottom, PanelLeft, Mic, and Keyboard. The wheel/dial set uses Lightbulb, BrainCircuit, Zap, Bot, ScrollText, Type, and PanelsTopLeft. Their editable SVG geometry is generated directly from the source manifest and build script. See the [Lucide icon library](https://lucide.dev/icons/).

## Recommendations incorporated

- Keep high-frequency, reversible actions on physical buttons.
- Put reasoning effort and task navigation on detented rotary controls.
- Separate commands, agent/task management, skill invocation, and reusable prompt patterns to reduce hunting.
- Preserve navigation and volume across every workspace.
- Use direct custom shortcuts for configurable actions. Do not infer Command Menu availability merely because a title string exists in the application bundle.
- Insert reusable text without submitting, allowing inspection and editing.
- Avoid physical permission approval.
- Prefer a separate foreground-matched application profile over modifying System.
