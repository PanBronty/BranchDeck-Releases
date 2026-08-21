<div align="center">

<img src="./assets/branchdeck-icon.png" width="120" height="120" alt="BranchDeck">

# BranchDeck

**A graph-first desktop Git client for Windows.**

Review, stage, commit, branch, investigate, and recover —
without ever losing sight of your history.

<p>
  <a href="https://github.com/PanBronty/BranchDeck-Releases/releases/latest"><img alt="Download the latest release" src="https://img.shields.io/github/v/release/PanBronty/BranchDeck-Releases?display_name=release&style=for-the-badge&label=Download&color=43c9ed"></a>
  <img alt="Windows 10 and 11, x64" src="https://img.shields.io/badge/Windows-10%20%7C%2011%20x64-36318f?style=for-the-badge&logo=windows11&logoColor=white">
  <img alt="Free evaluation licence" src="https://img.shields.io/badge/Licence-Evaluation-6f62d9?style=for-the-badge">
</p>

</div>

![The BranchDeck workspace: repository sidebar, multi-lane commit graph, and the working-changes panel with its commit composer](./assets/workspace.jpg)

<div align="center"><sub><i>Branches, history, and the working tree in one view — the graph never leaves the screen.</i></sub></div>

<br>

## Download

Grab a build from the **[latest release](https://github.com/PanBronty/BranchDeck-Releases/releases/latest)**.

| | Build | Best for | How it works |
| :-: | --- | --- | --- |
| 📦 | **`BranchDeck-…-setup.exe`** | Most people | Guided install into a folder you choose, Start menu shortcut, clean uninstall, and in-app updates on demand. |
| 🎒 | **`BranchDeck-…-portable.exe`** | Trying it without installing | One executable, run it from anywhere. Replace it by hand when a newer version appears. |

**Requirements:** Windows 10 or 11 (x64) and [Git for Windows](https://git-scm.com/download/win) — BranchDeck
drives your existing Git rather than shipping its own. No account and no administrator rights are needed.

<br>

## What it does

<table>
<tr>
<td width="50%" valign="top">

### 🕸️ The graph stays on screen

Paginated, virtualized, multi-lane history in topological order, every branch and tag labelled on its own row. Search runs in Git across every ref — not just the page in front of you.

</td>
<td width="50%" valign="top">

### 🔬 Stage exactly what you mean

Unified or side-by-side diffs with syntax highlighting, and staging by file, hunk, or a single line. Word-level marking, so a one-character edit stops looking like a rewritten line.

</td>
</tr>
<tr>
<td valign="top">

### 🧰 The hard operations, without a terminal

Interactive rebase, cherry-pick, revert, reset, bisect, blame, file history across renames, patch import, and three-way conflict resolution — each behind a confirmation that says what it is about to do.

</td>
<td valign="top">

### ↩️ Mistakes are recoverable

Undo and redo of application operations, plus reflog, stashes, and worktrees. A hard reset is a separate choice behind its own confirmation.

</td>
</tr>
<tr>
<td valign="top">

### 🌍 Every provider you actually use

GitHub (and Enterprise Server), GitLab (SaaS and self-managed), Bitbucket Cloud, and Azure DevOps: clone, push, create repositories, and open pull requests — plus Azure's review actions where they exist.

</td>
<td valign="top">

### 🗂️ Many repositories at once

Clone everything an account has that this machine does not, and fast-forward every saved repository's default branch in one run. Anything with local work in the way is reported, not touched.

</td>
</tr>
<tr>
<td valign="top">

### 🔒 Local-first, by design

No telemetry and no BranchDeck cloud service. Tokens live in Windows' encrypted credential storage, and never enter the renderer process.

</td>
<td valign="top">

### ✍️ Commit messages from a local model

Optional and off until you fetch the model — a one-time ~2.1 GB download, checksum-verified on arrival. After that it runs on your machine: the diff never leaves it.

</td>
</tr>
</table>

<br>

## Verify your download

Every executable ships with a matching `.sha256` file. Download both, then run this in PowerShell from the
folder they landed in:

```powershell
Get-ChildItem BranchDeck-*.exe | ForEach-Object {
    $expected = ((Get-Content "$($_.Name).sha256") -split ' ')[0]
    $actual   = (Get-FileHash $_ -Algorithm SHA256).Hash
    if ($actual -eq $expected) { "OK        $($_.Name)" } else { "MISMATCH  $($_.Name)" }
}
```

Every line should say `OK`. A `MISMATCH` means the download is damaged or was tampered with — fetch it again
rather than running it.

> [!IMPORTANT]
> **BranchDeck is not code-signed yet**, so Windows SmartScreen shows **"Windows protected your PC"** the first
> time you run the installer. That means Windows does not recognise the publisher — not that anything is wrong
> with the file. Verify the checksum above, then choose **More info → Run anyway**.

<br>

## Updates

Installed builds check this feed quietly at startup and speak up only when a newer version exists — nothing
downloads until you approve it, and a current version or a network failure stays silent. The notice opens the
update controls at the end of **Settings › General**, and your repositories and settings survive an update.

Portable builds are updated by replacing the executable.

<br>

## Questions

<details>
<summary><strong>Does BranchDeck send anything anywhere?</strong></summary>

<br>

No telemetry, no analytics, no BranchDeck server. Four things reach the network, and that is the whole list:

1. **Git talking to your own remotes** — the same fetches and pushes your `git` command line would make.
2. **The hosting providers you sign in to**, for cloning, pushing, and pull requests.
3. **A version check against this releases page** at startup.
4. **The commit-message model, once**, if you switch that feature on.

Generating a commit message afterwards runs entirely on your machine. The diff is never uploaded.

</details>

<details>
<summary><strong>What exactly gets downloaded for the local commit-message model?</strong></summary>

<br>

A single quantised [Qwen2.5-Coder-3B-Instruct](https://huggingface.co/Qwen/Qwen2.5-Coder-3B-Instruct-GGUF)
file, about **2.1 GB**, fetched from Hugging Face only when you turn the feature on. BranchDeck checks its size
and SHA-256 before using it and refuses a damaged download. The runtime that executes it ships inside the
installer, so once the file is there the feature works offline. Leave it off and nothing is downloaded.

</details>

<details>
<summary><strong>Where is the source code?</strong></summary>

<br>

In a separate private repository. This one is only the download page — GitHub's automatically generated source
archives here contain this page, the licence, and the images, not the application.

</details>

<br>

## Evaluation release

BranchDeck is distributed under a free [evaluation licence](./LICENSE). Use the official GitHub release to
evaluate it, and point other evaluators here rather than forwarding the executable.

Found a bug? **Help → Copy diagnostics** inside the application, then email the result — with a note about what
you were doing — to **[pavel.p.kocian@gmail.com](mailto:pavel.p.kocian@gmail.com)**. It carries version numbers
and recent crash kinds, but no tokens, account names, or repository paths.
