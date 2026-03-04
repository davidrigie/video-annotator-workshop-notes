# Vibe Coding Workshop Notes
*For non-coders*

---

## Cool Things to Teach

- **`claude --resume`** — Lets you pick up a previous conversation right where you left off. Great for when you close your terminal or want to continue a project later without re-explaining everything.
- **Keep `CLAUDE.md` concise** — The `CLAUDE.md` file is loaded into context every conversation, so keeping it short saves valuable context window space. Don't be afraid to ask Claude to trim it down.
- **Plan mode (`Shift+Tab`)** — Press `Shift+Tab` before sending a message to toggle into plan mode. Claude will research and think through an approach before writing any code. Great for bigger tasks where you want to review the plan first. You can also trigger it by asking Claude to "make a detailed plan."
  - Tip: By default, Claude writes the plan file to a centralized location. Tell it to save the plan to your project folder so you can easily reference it later.
  - Once the plan is approved, Claude will ask to clear context and start executing with a fresh conversation. This is important — performance is optimal with a clean context window rather than one cluttered with all the back-and-forth from planning.
- **Testing & feedback loop** — After the first version runs, your job becomes a tester. Try everything, and when something doesn't work, describe clearly what you expected vs. what actually happened. You don't need to know *why* it's broken — just explain the behavior. Think of yourself as a product manager filing bug reports.
  - Claude does a good job automatically running the app to test its own changes — you don't have to manually launch it every time.
  - If Claude gives you commands to run, you can just ask it to run them for you — no need to copy/paste into the terminal yourself.
- **Avoid major pivots mid-build** — Changing fundamental architecture (e.g. web app to local app) mid-development can leave behind a mess of leftover code and assumptions. Better to get the direction right upfront during planning. If you do need a big pivot, consider starting fresh rather than retrofitting.
- **UI polish can break things** — Be warned that even "simple" visual tweaks can accidentally break core features. When refining the UI, test core functionality after each round of changes. This is where having git (silent commits) really helps — you can roll back if a cosmetic change breaks something important.
- **"Tag" a good version** — When your app reaches a nice stable state, ask Claude to "tag this version." You don't need to know what that means technically — Claude will create a git tag as a save point you can return to if future changes break things.
- **`Esc` to interrupt** — Press `Esc` to stop Claude mid-response if it's going off track, explaining things you don't need, or doing something you didn't ask for. Don't wait for it to finish — just interrupt and redirect.
- **`/exit`** — Type this to quit Claude Code when you're done.
- **`/clear`** — Clears the conversation and starts fresh. Useful when Claude starts going in circles or the context gets cluttered.
- **`/compact`** — Summarizes the conversation to free up context space without losing everything.
- **`/usage`** — Check how much of your daily usage allowance you have left so you know if you're at risk of running out.
- **`/rewind`** — Lets you undo and go back to a previous point in the conversation (also triggered by pressing `Esc` twice). When you rewind, you get options:
  - **Restore code and conversation** — rolls back both files and chat
  - **Restore conversation only** — rewinds chat but keeps current code
  - **Restore code only** — reverts files but keeps chat
  - **Summarize from here** — compresses conversation to free up context
  - Note: This is NOT git — it's Claude Code's own lightweight checkpoint system. It only tracks changes made through Claude's tools, not bash commands like `rm` or `mv`. Checkpoints auto-clean after 30 days.

---

## Misc. Helpful Notes

- **User-level settings location (`settings.json`):**
  - **macOS:** `~/.claude/settings.json` (e.g. `/Users/jane/.claude/settings.json`)
  - **Linux:** `~/.claude/settings.json` (e.g. `/home/jane/.claude/settings.json`)
  - **Windows:** `%USERPROFILE%\.claude\settings.json` (e.g. `C:\Users\Jane\.claude\settings.json`)

- **Dev dependency gotcha** — Things like Python, npm, Node.js, etc. need to be installed for Claude to actually build and run apps. Developers usually already have these. Non-coders won't — need to see how smoothly installation goes for attendees and whether to include a pre-workshop setup guide.

- **Cross-platform local app building** — If attendees try to build a locally installable app (e.g. with Electron or Tauri), building for different operating systems can be tricky. You can typically only build for the OS you're running on without extra setup.

- **File handling is tricky either way** — Browser-based apps are sandboxed and can't freely access the filesystem. Even with a local server, files loaded through the browser frontend still go through sandboxed file APIs — large files (like 30-60 min videos) can be slow or hit memory limits. True desktop apps (Electron/Tauri) have full filesystem access but are harder to build and package. No perfect answer — just be aware this is a common pain point.

- **Installing git:**
  - **macOS:** Open Terminal and type `git`. If it's not installed, macOS will prompt you to install the Command Line Tools — just click "Install" and follow the prompts.
  - **Windows:** Download from [git-scm.com](https://git-scm.com/download/win) and run the installer. Use all default settings — just keep clicking Next.
  - **Linux:** Run `sudo apt install git` (Ubuntu/Debian) or `sudo dnf install git` (Fedora). Most Linux distros have it pre-installed.

- **Silent git setup (TESTED — works well!)** — Have attendees run `git init` as a setup step without explaining git in depth. Gives a safety net for reverting mistakes. Tell Claude to handle git silently and not mention it in responses, so it doesn't confuse non-coders. Example `CLAUDE.md` instruction:
  ```
  ## Version Control
  - This project uses git. Automatically commit after completing meaningful work (new features, bug fixes, etc.)
  - Do NOT ask the user about git or explain git concepts — just handle it silently
  - Write clear commit messages describing what changed and why
  - Never mention commit hashes, branches, or git internals to the user
  ```
