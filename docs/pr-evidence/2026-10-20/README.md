# Contribution UI evidence — 2026-10-20

These eight PNGs support the client fixes for Fei2411/DeepSeek-Bot issues
[#216](https://github.com/Fei2411/DeepSeek-Bot/issues/216),
[#285](https://github.com/Fei2411/DeepSeek-Bot/issues/285),
[#297](https://github.com/Fei2411/DeepSeek-Bot/issues/297), and
[#339](https://github.com/Fei2411/DeepSeek-Bot/issues/339).

They are isolated component fixtures rendered from the changed DS Bot source and
its styles. They are not screenshots of a complete DSH deployment or evidence of
an end-to-end model run. The surrounding fixture shell and explanatory text are
test scaffolding. All Bot names, conversations, messages, IDs, and key-request
labels are synthetic. The key-request fields contain no secret values. Every
image was visually inspected before publication.

## Images

| Issue | Image | State shown |
|---|---|---|
| #216 | [216-exchange-latest.png](216-exchange-latest.png) | The exchange opens at its newest message. |
| #216 | [216-exchange-reading-earlier.png](216-exchange-reading-earlier.png) | Earlier messages remain readable after scrolling away from the bottom. |
| #285 | [285-loading-dock.png](285-loading-dock.png) | Pending question and key-request controls are visible while history is loading. |
| #285 | [285-inline.png](285-inline.png) | Both cards appear at their mounted tool calls, with no duplicate dock copies. |
| #297 | [297-before-click.png](297-before-click.png) | The Bot header offers Back to chat while another conversation view is selected. |
| #297 | [297-after-click.png](297-after-click.png) | The ordinary Bot header returns after selecting chat. |
| #339 | [339-sidebar-mobile-selected.png](339-sidebar-mobile-selected.png) | Selecting a conversation on a narrow screen leaves the collapsed sidebar rail. |
| #339 | [339-sidebar-desktop-selected.png](339-sidebar-desktop-selected.png) | The wider desktop sidebar remains expanded after selection. |

The message text in the exchange images is a fixed sample, including its sentence
about regression results; that sentence is not a test runner report.

## Validation scope

### #216 — exchange position

The real `ExchangeDialog` component and product CSS were mounted in a local
Chromium fixture. The exchange action returned synthetic messages. Browser checks
covered opening at the newest message, following new messages while at the
bottom, preserving the reading position after scrolling up, and opening another
pair at its latest message. DSH transport, model execution, and Markdown parsing
were not exercised by these screenshots; the Markdown primitive was replaced
with a text renderer in the fixture.

### #285 — pending cards during history loading

The real `QuestionDock`, `SecretDock`, and `ToolCell` components ran with React 18
and jsdom. The checks covered cold/loading visibility, actual `ToolCell` layout
effects moving each card from dock to inline and back after unmount, one visible
copy per request, a single keyboard-answer submission, and cancellation clearing
the pending key request. Roster and request actions used synthetic observable
state. The screenshots render the resulting React DOM and product CSS in
Chromium with finite animations settled. They do not exercise real secrets or
host-side delivery.

### #297 — returning to chat

The real DS Bot header and navigation helper ran with pinned React 18, jsdom, and
the DSH `SlotCore` and conversation store from `dsh-v0.2.1-rc.2`. Checks covered a
host header registered after the Bot replacement, reuse of its store handle,
clicking Back to chat, persisting the chat selection, retaining the editor draft,
restoring the details action, source removal, and cleanup. Target activation was
observed through a test callback; a complete DSH view renderer and service
composition were not launched by this fixture. The screenshots render the
resulting React DOM and product CSS in Chromium.

### #339 — sidebar selection on narrow screens

The real `TeamSidebar` component and product CSS were mounted in Chromium with
synthetic roster, sessions, retain information, and navigation/layout callbacks.
Browser checks exercised mobile and desktop selection behavior. The screenshots
show the resulting selected conversation and sidebar state. The fixture shell
and DSH logo/Markdown primitives are test replacements; this is not an Electron
or full DSH shell test.

## Source revisions

| Issue | Validated source commit |
|---|---|
| #216 | `747c4ad65a2f1c611bbae1b5218539de65d716b3` |
| #285 | `673e5d5a86e201900a3d00cc21bfa3eb2bace920` |
| #297 | `9928b742526319fa21fe4b7f88f36a58f9cb2fd5` |
| #339 | `0646f95afd12c3b4e1f341ebc1dcadbca816050d` |

This evidence-only branch is based on
`9534bec485ef07881d5435dbfe8de55baec7b260`. It adds this directory without changing
the product branches. The associated PRs contain the source changes and
persistent regression tests; their test results should be assessed alongside
these visual examples.
