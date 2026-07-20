# Codex custom shortcuts

The installed Codex Windows app exposes Reasoning, Plan, and Fast as configurable commands, but does not list them in the Command Menu. The Loupedeck profile therefore sends these direct shortcuts:

| Codex command | Custom shortcut | Loupedeck controls |
|---|---|---|
| Decrease reasoning effort | `Ctrl+Alt+Shift+Down` | R1 left; wheel rotate left |
| Increase reasoning effort | `Ctrl+Alt+Shift+Up` | R1 right; wheel rotate right |
| Cycle reasoning effort | `Ctrl+Alt+Shift+R` | R1 press; wheel center |
| Toggle Plan mode | `Ctrl+Alt+Shift+P` | Skills page Plan; wheel left |
| Toggle Fast mode | `Ctrl+Alt+Shift+F` | Wheel right |
| Start Dictation (push-to-talk) | `Ctrl+Shift+D` | Physical keyboard only |
| Continue in New Chat | `Ctrl+Alt+Shift+N` | Agents position 7 |
| Copy as Markdown | `Ctrl+Alt+Shift+C` | Agents position 10 |

- Editable source: `src/codex-keybindings.json`
- Installed Codex file: `%USERPROFILE%\.codex\keybindings.json`

Codex reads these mappings when its shortcut state is loaded. After replacing the installed file outside Codex, restart the Codex app once, then open Settings > Keyboard Shortcuts and confirm all eight entries above.

Review uses Codex's built-in Toggle Review Panel shortcut `Ctrl+Alt+B`.

The installed Codex command ID for Dictation is `composer.startDictation`. It is assigned explicitly to `Ctrl+Shift+D` in `keybindings.json` for keyboard push-to-talk use. Physical testing confirmed that Codex listens only while this chord is held, whereas a Loupedeck shortcut is an atomic press/release. Commands position 11 and round button 8 therefore use Windows Voice Typing (`Win+H`) as a reliable press-on/press-off control. Restart Codex once only after installing or changing the native keybinding file; changing the Loupedeck `Win+H` mapping does not require a Codex restart. `Ctrl+Shift+V` is intentionally unused because it invokes paste-as-plain-text in this build.
