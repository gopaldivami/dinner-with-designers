# Git: A Designer’s Quick Reference Guide

Navigating version control without losing your mind (or your work).

## Part 1: Mindset & Context (The "Why")

### Slide 1: The Mental Shift: Why Git Now? (Figma vs. Code)

- The Figma World:
  - Figma is a live graphical database. Multiple people look at the same artboard, see live cursors, and changes are visual and continuous.
  - If two people edit a component, Figma handles the layers instantly.
- The Code World:
  - Code consists of plain-text files. Computers are literal.
  - If Line 14 of a file says color: red in your version and color: blue in someone else's version, the computer doesn't know which one is right—it just breaks.
- Why Git + Claude Code?
  - Claude Code modifies physical files on disk at high speed.
  - Git acts as an immutable time-machine and safety net, tracking every change made by you, your teammates, or Claude so everyone can work simultaneously without accidentally overwriting each other. (Note: If you've ever used Figma's "Branching" feature for major redesigns, Git works on that exact same principle, but for text and code).

### Slide 2: Core Concepts Demystified (Branches & Lifecycles)

- What is a Branch?
  - The Analogy: A private working copy or an artboard duplicate.
  - The Definition: An isolated workspace off the main project (main).
  - Why use it: It lets you and Claude experiment, try out design tokens, or adjust layouts without breaking the stable, working version of the application that everyone else is using. Once your piece is working and tested, you merge it back.
- Branch Lifecycle: When to Start and How Long to Keep It:
  - When to start: Create a new branch every time you start a distinct task, design update, or experiment with Claude Code (e.g., feature/update-nav-spacing). Never work directly on main.
  - How long to keep it: Keep it short-lived (hours or a couple of days max).
  - The Rule of Thumb: Small branches mean small changes. Small changes mean zero merge conflicts. If a branch lives for two weeks, it will drift drastically away from what everyone else is building, leading to a painful merge later.

### Slide 3: Translating Concepts for the Prep Talk

- On Repositories and Main:
  "Think of main as the production file in Figma that the client or public sees. You never design directly on the live hand-off screen; you make a local copy or a playground page first. That playground is your branch."
- On Commits:
  "A commit is like hitting Command+S, but with a detailed description in the version history panel. Instead of generic saves, every commit should represent one complete thought or minor task (e.g., 'Fixed mobile navigation alignment')."
- On Pull Requests (PRs):
  "Think of a Pull Request like 'Request for Review' or handing off a frame to engineering/design lead for sign-off. It’s a dedicated URL where the team can look at your code changes, see what Claude generated, leave comments, and approve it before it touches the main app."

## Part 2: The Glossary & Navigation

### Slide 4: The Core Dictionary (Design vs. Git)

Git Term	Design Equivalent	Plain English Explanation
Repository (Repo)	The Design System / Project File	The central folder or "cloud file" containing all code, assets, and project history.
Commit	A Version Snapshot / "Save Version"	Taking a permanent snapshot of your work with a clear label explaining what changed.
Branch	A Draft / Artboard Duplicate	An isolated copy of the project where you can experiment safely without touching live code.
Stash	A Temporary Clipboard / Scratchpad	Hiding your current messy work temporarily so you can switch tasks or sync up cleanly.
Merge / PR	Hand-off & Review	Reviewing and fusing your approved draft back into the main project file.
Main	The Master Production File	The official, live, clean version of the app. Nobody edits here directly.

## Part 3: Practical Execution (The "How")

  ```
  Practice commands and avoid asking LLM to do git tasks
  Get this control over a period of time, this saves a lot of time down the lane
  ```

### Slide 5: Quick Commands — git status (Where am I?)

- Native Command: git status
- Ask Claude Equivalent: "Hey Claude, what branch am I on and do I have any uncommitted changes?"
- Plain English Meaning: Checks your current location and file states to make sure you aren't accidentally working in the wrong place.

### Slide 6: Quick Commands — git pull (Sync Up)

- Native Command: git pull origin main
- Ask Claude Equivalent: "Hey Claude, pull the latest updates from main."
- Plain English Meaning: Downloads the freshest version of the project to your computer so you are always building on top of current work.

### Slide 7: Quick Commands — git checkout -b (Create a Draft Branch)

- Native Command: git checkout -b feature/task-name
- Ask Claude Equivalent: "Hey Claude, create and switch me to a new branch called feature/update-spacing."
- Plain English Meaning: Creates your private sandbox workspace so any experiments or mistakes stay entirely contained.

### Slide 8: Quick Commands — git stash (The Emergency Scratchpad)

- Native Command: git stash (to hide) / git stash pop (to bring back)
- Ask Claude Equivalent: "Hey Claude, stash my current changes so I can switch branches, and bring them back when I'm ready."
- Plain English Meaning: Temporarily sets aside unfinished work when an urgent update forces you to switch context mid-way without losing your progress.

### Slide 9: Quick Commands — git commit (Save Snapshot)

- Native Command: git add . followed by git commit -m "Description"
- Ask Claude Equivalent: "Hey Claude, commit my current changes with the message 'Fixed hero image alignment'."
- Plain English Meaning: Packages your local progress into a permanent checkpoint with a readable description.

### Slide 10: Quick Commands — git push (Publish to Cloud)

- Native Command: git push origin feature/task-name (with first-time setup flags if needed)
- Ask Claude Equivalent: "Hey Claude, push my branch to GitHub."
- Plain English Meaning: Uploads your local draft branch up to the shared cloud repository so others can see it.

### Slide 11: The Designer’s Workflow & Care Points

- Phase 1: Syncing Up
  - Action: git pull origin main
  - ⚠️ Care Point: Always do this first. Never start a new task on old code.
- Phase 2: Branching Out
  - Action: git checkout -b feature/your-task-name
  - ⚠️ Care Point: Never write code or prompt Claude directly on main. Always verify your status first.
- Phase 3: Crafting & Managing Interruptions
  - Action: Prompting Claude Code / Using git stash if an emergency update forces a context switch.
  - ⚠️ Care Point: Keep branches short-lived. If you get blocked or need to jump to a different fix, stash your current work cleanly instead of abandoning it.
- Phase 4: Capturing & Publishing to Remote
  - Action: git commit and publishing the branch via git push origin feature/....
  - ⚠️ Care Point: When pushing a brand new local branch to GitHub for the first time, let Claude Code handle the exact push command syntax to avoid path typos. Write clear, human-readable commit messages.
- Phase 5: Handoff (The Pull Request)
  - Action: Opening a PR on GitHub.
  - ⚠️ Care Point: Treat this like a design critique handoff. Include screenshots or notes explaining the visual changes before merging into main.

## Part 4: Handling Roadblocks

### Slide 12: Conquering Merge Conflicts

- Why Am I Getting Into Merge Conflicts?
  - A merge conflict happens when two different sources change the exact same line of the same file in different ways, and Git can't figure out which version to keep.
  - Example: You and a teammate (or Claude working on two separate prompts) both edited the padding value in styles.css on different branches.
- What It Looks Like (Conflict Markers):
  ```
  <<<<<<< HEAD
  padding: 16px; (Your branch's version)
  =======
  padding: 24px; (The incoming branch's version)
  >>>>>>> feature/teammate-update
  ```
- How to Solve Merge Conflicts Without Panic:
  - Step 1: Don't panic. A conflict is just Git asking a human to make a final design or logic decision. It is not an error or a broken project.
  - Step 2: Choose or combine. Decide which value is correct, delete the visual markers (<<<<<<<, =======, >>>>>>>), and save the file.
  - Step 3: Leverage Claude Code (The Ultimate Cheat Code). Prompt Claude directly: "I have a merge conflict in styles.css, can you help me resolve it by keeping the updated padding?" Claude will read the markers and clean it up for you instantly.