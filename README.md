# SeqBridge
<img width="1280" height="800" alt="Screenshot 2026-04-10 at 10 15 41 PM" src="https://github.com/user-attachments/assets/4357d276-0233-4d8a-8e97-b87ca043cc06" />

A macOS app for browsing and transferring data in [Illumina BaseSpace Sequence
Hub](https://basespace.illumina.com) — runs, projects and app sessions — without
living in a terminal.

It reads and writes the same `~/.basespace` profiles as the official BaseSpace
CLI, so if you already use `bs`, your connections are picked up automatically.

## Requirements

- macOS 14 (Sonoma) or later, Apple Silicon or Intel
- A BaseSpace Sequence Hub account

## What it does

**Browse** — Runs, Projects and AppSessions, each with search, an "Only mine"
filter, and per-tab counts that say how much is loaded of how much exists.

**Download** — a whole run, a project, or selected app sessions. Filter by file
type, or use SAV mode to pull just the files Sequencing Analysis Viewer needs.
The download dialog shows the item's size and the free space at your chosen
destination before it starts. Transfers run several files at a time, survive an
individual file failing, and can be cancelled mid-flight.

**Upload** — files into a project. Files above 5 GiB use S3 multipart upload,
with progress reported throughout.

Two upload paths need the `write global` OAuth scope, which BaseSpace does not
grant to SeqBridge's application registration: uploading a whole **run folder**,
and uploading **FASTQ** into a project. FASTQ becomes a BaseSpace *sample*,
which that scope covers; other file types become AppResults and are unaffected.

Both are offered only to profiles whose token carries the scope — in practice
ones created with the BaseSpace CLI rather than in SeqBridge. Otherwise the run
upload button is hidden and FASTQ is left out of the file-type picker, rather
than either failing partway through. Getting them back for everyone requires
Illumina to grant the scope.

**Multiple accounts** — as many profiles as you like, switched from the toolbar,
each with its own region and its own display name.

## Regions

BaseSpace runs as independent regional deployments, each with its own set of
registered applications. SeqBridge is registered in all of them except Middle
East:

| | |
| --- | --- |
| Australia · Canada · European Union · India · Indonesia | ✅ |
| Israel · Japan · Korea · Singapore | ✅ |
| United Kingdom · United States East · United States West | ✅ |
| Middle East | Not yet |

An unregistered region is disabled in the sign-in picker with an explanation,
rather than failing after you have already approved the sign-in.

## First run

1. SeqBridge asks for access to a folder called `.basespace` in your home
   folder, creating it if it does not exist. macOS requires you to grant this
   once; the app cannot read anything outside that folder and the destinations
   you pick for downloads.
2. Click **Sign In with BaseSpace**, choose your region and name the profile.
3. Illumina's sign-in page opens in a window belonging to SeqBridge, showing
   the page's address beside a lock, alongside a short code. Approve there; the
   window closes by itself and the profile is ready. No browser is launched.

## Where things are kept

| What | Where |
| --- | --- |
| Connection profiles | `~/.basespace/<profile>.cfg` — the CLI's format |
| Diagnostic logs | Inside the app's sandbox container, never transmitted. **Help → Open Log Folder…** (⇧⌘L) |
| Downloads | Wherever you choose, per download |

## Privacy

SeqBridge collects nothing. There is no analytics, no telemetry, and no server
operated by the developer — the app talks only to the BaseSpace instance you
sign in to. Full details, including how sign-in tokens are stored, are in the
[privacy policy](Privacy.md).

## Support

**[SeqBridge support](https://dmatica.github.io/SeqBridge/)** — troubleshooting,
answers to common questions, and an email address that needs no account
anywhere. Also reachable in the app at **Help → SeqBridge Help & Support**.

If you would rather work in the open, [open an
issue](https://github.com/dmatica/SeqBridge/issues) instead. Either way,
attaching the relevant log (**Help → Open Log Folder…**) makes transfer problems
far easier to diagnose — the logs stay on your machine until you choose to share
them, so do check them for anything you would rather not post.

---

SeqBridge is an independent application. It is not affiliated with, endorsed by,
or sponsored by Illumina, Inc. "Illumina", "BaseSpace" and "BaseSpace Sequence
Hub" are trademarks of Illumina, Inc., used here only to describe what the app
connects to.
