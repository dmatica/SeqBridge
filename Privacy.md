# SeqBridge Privacy Policy

_Last updated: 16 August 2026_

SeqBridge is a macOS client for Illumina BaseSpace Sequence Hub. It runs entirely
on your Mac and talks only to the BaseSpace instance you sign in to.

## What SeqBridge collects

**Nothing.** There is no analytics, no telemetry, no crash-reporting service, and
no server operated by the developer of SeqBridge. No information about you or
your use of the app is transmitted to the developer, and none is sold or shared
with anyone.

## What SeqBridge connects to

SeqBridge makes network requests to two kinds of destination, both of them
Illumina's:

- **The BaseSpace API for the region you choose** — one of the regional
  endpoints under `basespace.illumina.com`. This is where runs, projects and
  app sessions are listed, and where downloads originate.
- **Amazon S3 endpoints supplied by BaseSpace** for file transfers. These
  addresses are returned by the BaseSpace API for the specific transfer taking
  place; SeqBridge does not choose them.

The app also checks whether the network is reachable by contacting
`api.basespace.illumina.com`. No other host is contacted.

## Your BaseSpace credentials

SeqBridge signs in using the OAuth 2.0 Device Authorization Grant. You enter
your username and password on **Illumina's own sign-in page**, shown in a secure
system-provided window (ASWebAuthenticationSession) — SeqBridge never sees them.

What SeqBridge receives and stores is an access token, kept on your Mac in
`~/.basespace/<profile>.cfg`. This is the same location and file format the
official BaseSpace CLI uses, which is what lets the two share profiles. **These
files are plain text**, protected by your macOS account's file permissions
rather than by encryption. Anyone with access to your user account, or to an
unencrypted backup of it, can read them. Enabling FileVault protects them at
rest.

Access tokens are sent only to the BaseSpace instance they belong to.

## What else is stored on your Mac

- **Profile display names** you set in the app, in SeqBridge's own preferences.
- **A security-scoped bookmark** recording your permission to use the
  `~/.basespace` folder. It grants access to that folder only.
- **Diagnostic logs and MetricKit reports**, inside SeqBridge's sandbox
  container at `Library/Logs/SeqBridge/`. These record app activity — file
  names, transfer progress, errors — to help diagnose problems. **They are never
  transmitted anywhere.** Older logs are deleted automatically, and you can view
  or remove them at any time via **Help → Open Log Folder…**.
- **Files you download**, in the folder you select for each download.

## System APIs SeqBridge uses

Declared in the app's privacy manifest, all for the app's own operation:

| API | Why |
| --- | --- |
| User defaults | Stores the folder bookmark and your profile display names |
| File timestamps | Finds abandoned download fragments and old logs to delete |
| Disk space | Checks the destination has room before a download starts |

## Deleting your data

- **Sign-in credentials:** delete the relevant `.cfg` file from `~/.basespace`,
  or the whole folder. You can also revoke SeqBridge's access from your
  BaseSpace account settings.
- **Logs:** open **Help → Open Log Folder…** and delete the contents.
- **Everything else:** removing the app and its container
  (`~/Library/Containers/davinderholyfield.SeqBridge`) leaves nothing behind.

Data held in your BaseSpace account is governed by
[Illumina's privacy policy](https://www.illumina.com/company/legal/privacy.html),
not this one.

## Children

SeqBridge is a professional tool for genomics data and is not directed at
children.

## Changes

Any change to this policy will be published at this address with a revised date
above.

## Contact

Questions about this policy: seqbridge.ngs@gmail.com

Support, including anything not covered here:
<https://dmatica.github.io/SeqBridge/>

---

SeqBridge is an independent application. It is not affiliated with, endorsed by,
or sponsored by Illumina, Inc. "Illumina", "BaseSpace" and "BaseSpace Sequence
Hub" are trademarks of Illumina, Inc., used here only to describe what the app
connects to.
