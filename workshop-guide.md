# Vibe Coding Workshop Guide
*Building real apps with Claude Code — no coding experience required*

---

## What is Vibe Coding?

Vibe coding is building software by describing what you want in plain language and letting an AI (Claude Code) write all the code for you. Your role is to be the product manager — you decide *what* to build, test it, and give feedback. Claude handles the *how*.

---

## The 7 Key Insights

Before diving into the how-to, here are the most important lessons from building a real app this way.

### 1. You Are the Product Manager, Not the Developer

This is the single most important mindset shift. You decide *what* to build — Claude handles *how*. Describe what you want in plain language. Report bugs by what you see, not what you think is wrong in the code.

- "Make the button bigger and blue" — not "change the CSS padding"
- "When I click save, nothing happens" — not "the onClick handler isn't firing"
- "I want to be able to scrub through the video frame by frame" — not "add a frame step function"

Claude will choose the technology (React, Vite, Tailwind, etc.) for you — and that's fine. You don't need to understand or even know what these are. Trust the choices and focus on the result.

### 2. Plan Before You Build

Spending time in plan mode upfront saves hours of pain later. The most painful moment in our build was pivoting from a web app to a desktop app mid-development — it left behind broken assumptions and cascading issues that were hard to untangle.

- Follow a phased approach: set up `CLAUDE.md` first → create a plan second → build third. Resist the urge to say "just build it" all at once. Each phase builds on the last.
- Use plan mode (`Shift+Tab`) for anything beyond a small tweak
- Review the plan carefully — make sure big decisions (what kind of app, how files are handled, etc.) are right *before* code gets written
- Tell Claude to save the plan to your project folder so you can reference it later
- When the plan is approved, Claude clears context for a fresh start — this is a good thing

### 3. Silent Git Is Your Safety Net

One plain English sentence gave us automatic save points, rollback capability, and version tagging — without learning a single git concept.

Just tell Claude: *"Update your instructions to use git for version control, but do it automatically and hide the details from me since I'm not familiar with git."*

This is an example of a powerful trick: **you can ask Claude to update its own instructions.** Think of `CLAUDE.md` as training your assistant on the job — you can shape how Claude behaves just by describing what you want in plain language.

Claude will silently commit your progress after every meaningful change. When you reach a good stable state, ask Claude to "tag this version" — it creates a named save point you can return to if future changes break things.

### 4. Know When to Interrupt and Redirect

`Esc` is your most powerful key. Claude will sometimes:
- Over-explain technical details you don't need
- Go down the wrong path
- Get stuck trying the same fix over and over

Don't wait for it to finish. Press `Esc`, then redirect: "That's not working. Let's try a different approach." Or use `/rewind` to roll back and start that part over. Or `/clear` to start completely fresh.

### 5. Test After Every Change — Especially "Small" Ones

The first version of your app will look impressive but have issues. That's normal — don't be discouraged. The magic isn't the first attempt, it's how fast you can iterate to a working version.

Even simple visual tweaks can accidentally break core features. After each round of changes:
- Test all the main things your app does, not just the thing that changed
- If something broke, tell Claude immediately — don't let issues pile up
- Show Claude what's wrong visually — you can paste or drag screenshots into Claude Code, which is way easier than describing UI problems in words
- This is where silent git saves you — if a cosmetic change breaks something important, you can roll back

### 6. You Don't Need to Touch the Terminal

If Claude suggests commands to run, you don't need to copy/paste them yourself. Just say "run that for me." Claude can:
- Install dependencies
- Start the app
- Run tests
- Handle build commands

Your job is to approve the commands when Claude asks permission. Don't freeze when you see a permission prompt — things like `npm install` and `npm run dev` are safe. Claude will explain what it wants to do before running it.

### 7. Manage Your Context Window

This is an underrated skill that directly affects how well Claude performs. A cluttered context window means a less capable Claude.

- **`/compact`** — Summarize the conversation to free up space without losing everything
- **`/clear`** — Start completely fresh when things get messy
- **`/usage`** — Check how much daily usage you have left
- **Keep `CLAUDE.md` concise** — It loads into every conversation, so every extra line costs context
- **Fresh context after planning** — When Claude asks to clear context before executing a plan, say yes

---

## Prerequisites

### Install Before the Workshop

1. **Claude Code** — Follow the install instructions at [claude.ai/code](https://claude.ai/code)
2. **Node.js** — Download from [nodejs.org](https://nodejs.org) (LTS version). This also installs npm.
3. **Git:**
   - **macOS:** Open Terminal and type `git`. If not installed, macOS will prompt you to install Command Line Tools — just click "Install."
   - **Windows:** Download from [git-scm.com](https://git-scm.com/download/win) and run the installer. Use all default settings — just keep clicking Next.
   - **Linux:** Run `sudo apt install git` (Ubuntu/Debian) or `sudo dnf install git` (Fedora). Most distros have it pre-installed.

### Verify Everything Works

Open your terminal and run:
```
node --version
git --version
claude --version
```
Each should print a version number. If any fails, ask for help before the workshop starts.

---

## Getting Started

### Step 1: Create a Project Folder

Open your terminal and create a folder for your project:
```
mkdir my-app
cd my-app
```

### Step 2: Set Up Git (Safety Net)

```
git init
```
You don't need to understand git. We're just setting it up so Claude can silently save checkpoints of your work. If something breaks, you can roll back.

### Step 3: Start Claude Code

```
claude
```

### Step 4: Write Your First Prompt

Start by asking Claude to create a `CLAUDE.md` file — this is Claude's instruction manual for your project. Here's an example of a strong opening prompt:

> *"I want you to create a CLAUDE.md for me. Capture the fact that I am not a coder so you should tailor your responses and working style around that. I want to build an app for [describe your app idea]. [List your key features]. The goal is to [describe the problem you're solving]."*

**Tips for a good first prompt:**
- Describe the problem you're solving, not the technical solution
- List the features you want as a user
- Set expectations: "I'm not a coder"
- Don't over-specify technical details — let Claude recommend the approach

### Step 5: Add Silent Git Instructions

Tell Claude to handle version control for you:

> *"Update your instructions to use git for version control, but do it automatically and hide the details from me since I'm not familiar with git."*

Claude will add something like this to your `CLAUDE.md`:
```
## Version Control
- This project uses git. Automatically commit after completing meaningful work (new features, bug fixes, etc.)
- Do NOT ask the user about git or explain git concepts — just handle it silently
- Write clear commit messages describing what changed and why
- Never mention commit hashes, branches, or git internals to the user
```

### Step 6: Create a Plan

Ask Claude to make a detailed plan before writing any code:

> *"Create a detailed plan for building this app. Save the plan to this folder."*

You can also press `Shift+Tab` before sending your message to toggle plan mode.

- Claude will research and think through the approach before writing code
- Review the plan — make sure it matches what you want
- Once approved, Claude will ask to clear context and start fresh. **Say yes** — performance is best with a clean context window

### Step 7: Build, Test, Iterate

Once Claude starts building:
1. Let it work — approve commands when it asks permission
2. When it's done, **test everything yourself**
3. Report what's wrong in plain language:
   - "The button doesn't do anything when I click it"
   - "The video loads but I can't see the play controls"
   - "When I add a comment, it disappears when I go to the next frame"
4. Claude will fix and re-test. Repeat until it works!

---

## How to Talk to Claude

### Do This
- Describe what you want as a user: *"Make the button bigger and blue"*
- Report bugs by behavior: *"When I click save, nothing happens"*
- Batch related issues: *"Here are three things that need fixing: ..."*
- Ask Claude to run commands for you: *"Run that for me"*
- Paste or drag screenshots to show visual problems
- Interrupt with `Esc` if Claude is over-explaining technical details

### Don't Do This
- Don't try to write code or give technical instructions
- Don't make one tiny change at a time — batch feedback
- Don't let Claude ramble without interrupting — redirect it
- Don't change major architectural decisions mid-build (e.g., switching from web app to desktop app) — this causes cascading issues. Get the big decisions right during planning.

---

## Essential Commands & Shortcuts

### Keyboard Shortcuts

| Shortcut | What it does |
|----------|-------------|
| `Esc` | Interrupt Claude mid-response — use when it's going off track |
| `Esc Esc` | Open the rewind menu to undo changes |
| `Shift+Tab` | Toggle plan mode before sending a message |

### Slash Commands

| Command | What it does |
|---------|-------------|
| `/exit` | Quit Claude Code |
| `/clear` | Clear conversation and start fresh |
| `/compact` | Summarize conversation to free up context space |
| `/usage` | Check how much daily usage you have left |
| `/rewind` | Undo and go back to a previous point (same as `Esc Esc`) |

### Terminal Commands

| Command | What it does |
|---------|-------------|
| `claude` | Start Claude Code |
| `claude --resume` | Pick up a previous conversation where you left off |

---

## The Rewind Feature (Your Undo Button)

When you press `Esc` twice or type `/rewind`, you get options:

- **Restore code and conversation** — rolls back both your files and the chat
- **Restore conversation only** — rewinds the chat but keeps current code
- **Restore code only** — reverts files but keeps the chat
- **Summarize from here** — compresses conversation to free up context

This is NOT git — it's Claude Code's own checkpoint system. It only tracks changes made through Claude's tools, not terminal commands. Checkpoints auto-clean after 30 days.

---

## Settings & Configuration

### User-Level Settings

Claude Code's settings file lives at:
- **macOS:** `/Users/yourname/.claude/settings.json`
- **Linux:** `/home/yourname/.claude/settings.json`
- **Windows:** `C:\Users\YourName\.claude\settings.json`

### Project-Level Configuration

- **`CLAUDE.md`** — Instructions Claude reads every conversation. Keep it concise to save context space.
- **Plan files** — By default Claude saves plans to a centralized location. Ask it to save to your project folder instead.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Claude is going in circles | Use `/clear` or `/rewind` and re-explain the problem differently |
| Claude is explaining too much technical stuff | Press `Esc` to interrupt, then say "just tell me what changed from a user perspective" |
| Running out of daily usage | Check with `/usage`. Use `/compact` to save context. Be more concise in your messages. |
| "Command not found" errors | A required tool isn't installed. Claude will usually suggest how to install it, or ask for help. |
| App broke after a small change | Use `/rewind` to restore, or ask Claude to "go back to the tagged version" |
| Claude keeps asking to run commands | You can approve these — things like `npm install` and `npm run dev` are safe |

---

## Lessons Learned (From Building a Real App)

These lessons come from building a **Video Annotator** with Claude Code — a full desktop app with video playback, frame annotation, comment capture, and report export. Built in 17 iterative steps over a single session by a non-coder.

### What Went Well
- **Strong opening prompt** led to a solid `CLAUDE.md` and plan
- **Plan mode** helped organize a complex app into manageable phases
- **Silent git** worked great — automatic save points without needing to understand version control
- **Asking Claude to run commands** saved time vs. copying/pasting into the terminal
- **Claude auto-testing** its own changes caught issues early
- **Tagging a good version** created a safe rollback point before making risky changes
- First version looked cool and was usable after just a few iterations

### What Was Painful
- **Mid-build architecture pivot** (web to desktop app) left behind broken assumptions and was hard to untangle
- **UI polish broke core features** — cosmetic tweaks can have unintended side effects
- **Claude got stuck in loops** — tried the same fix multiple times without success. Solution: `/rewind` or `/clear` and re-explain differently
- **Claude over-explained technical details** — had to interrupt and redirect to keep things simple
- **File handling complexity** — browser-based apps can't freely access the filesystem; desktop apps (Electron) can, but are harder to build and package

### The Development Flow

1. Describe what you want → Claude creates `CLAUDE.md`
2. Review and refine `CLAUDE.md` (keep it concise!)
3. Ask Claude to plan → review the plan
4. Claude builds → you test → report issues → Claude fixes → repeat
5. Get to a working state → tag the version
6. Polish UI carefully, testing core features after each change
7. Export or package when ready

### The App That Was Built

A desktop video annotation tool with: drag-and-drop video loading, frame-by-frame stepping, rectangle annotations with comments, timestamped sidebar, auto-save, HTML report export for JIRA, and keyboard shortcuts. Available as macOS DMG and Windows installer. Claude chose React + Vite + Tailwind + Electron — the builder never needed to know what any of those are.

See the [build log](build-log.md) for the full chronological story.

---

*The bottom line: think like a product manager, plan before you build, and let Claude handle everything technical. Your superpower is knowing what you want — Claude's superpower is knowing how to build it.*

*Built with [Claude Code](https://claude.ai/code) — no coding experience required.*
