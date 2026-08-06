# How to Show the Result

Presentation rules for every skill in this plugin. Read this before producing a
final output.

## The rule

**Render the final deliverable as a visual card. Keep everything else as text.**

Visual: the Live Slice Card, the next slice card, the ship-check verdict, the
review verdict.

Text: questions, discussion, reasoning, follow-ups, anything mid-conversation.

Rendering every reply as a widget is slow and makes a conversation feel like a
slideshow. One card at the end, when there is something to keep.

## How to render

If a visual rendering tool is available in the current environment, use it and
pass the HTML below. Cowork and the desktop app provide one.

If no rendering tool is available, fall back to the plain text template in the
skill. The content is identical either way. Never mention which mode is being
used, and never apologise for the fallback.

## Colour meaning

Colour carries meaning here. Do not decorate.

| Meaning | Use | Where |
| --- | --- | --- |
| The one thing that must be real | Purple accent, filled row | Real part in every card |
| Good to go | Green | Ship-check "ready to share" |
| Go smaller for now | Blue | Ship-check "share privately first" |
| One thing to change | Amber | Ship-check "fix one thing", review gaps |
| Skipped or hand-done | Muted grey text | Not yet rows |

**Never use red.** Nothing this plugin reports is an emergency, and red makes
people stop rather than fix. Amber carries "change this" perfectly well.

Use CSS variables so the card works in light and dark mode. Never hardcode hex
values.

## Live slice card

Used by `plan-thin-slice`. Also by `next-slice`, with fewer rows.

```html
<div style="padding:1rem 0;font-family:var(--font-sans);color:var(--text-primary)">
<div style="border:1px solid var(--border-strong);border-radius:12px;padding:20px;background:var(--surface-2)">
  <div style="font-size:11px;color:var(--text-muted);letter-spacing:.04em">Live slice card</div>
  <div style="font-size:16px;font-weight:500;margin:2px 0 14px">PROJECT NAME</div>
  <div style="font-family:var(--font-mono);font-size:12px;line-height:2">
    <div style="display:flex"><span style="flex:0 0 132px;color:var(--text-muted)">first user</span><span style="flex:1">…</span></div>
    <div style="display:flex"><span style="flex:0 0 132px;color:var(--text-muted)">one job</span><span style="flex:1">…</span></div>
    <div style="display:flex;background:var(--bg-accent);border-radius:4px;padding:2px 6px;margin:2px -6px">
      <span style="flex:0 0 126px;color:var(--text-accent)">real part</span><span style="flex:1;color:var(--text-accent)">…</span></div>
    <div style="display:flex"><span style="flex:0 0 132px;color:var(--text-muted)">not yet</span><span style="flex:1;color:var(--text-secondary)">…</span></div>
    <div style="display:flex"><span style="flex:0 0 132px;color:var(--text-muted)">private/public</span><span style="flex:1">…</span></div>
    <div style="display:flex"><span style="flex:0 0 132px;color:var(--text-muted)">done when</span><span style="flex:1">…</span></div>
    <div style="display:flex"><span style="flex:0 0 132px;color:var(--text-muted)">question</span><span style="flex:1">…</span></div>
    <div style="display:flex"><span style="flex:0 0 132px;color:var(--text-muted)">next action</span><span style="flex:1">…</span></div>
  </div>
  <div style="font-size:12px;color:var(--text-muted);margin-top:14px;padding-top:12px;border-top:1px solid var(--border)">Timebox … · Cost cap …</div>
</div>
</div>
```

Rules:

- Only the real part row is filled with colour. One highlight per card, or the
  emphasis means nothing.
- Not yet is muted, because it is the part people should feel relaxed about.
- Next action is the last row, so it is the thing left on screen.
- Never add a ninth row.

## Ship-check verdict

Used by `ship-check`. The banner colour is the whole message, so get it right.

```html
<div style="padding:1rem 0;font-family:var(--font-sans);color:var(--text-primary)">
<div style="border:1px solid var(--border-success);border-radius:12px;padding:18px;background:var(--bg-success);margin-bottom:12px">
  <div style="font-size:11px;color:var(--text-success);letter-spacing:.04em;margin-bottom:4px">Ship check</div>
  <div style="font-size:18px;font-weight:500;color:var(--text-success)">Ready to share</div>
  <div style="font-size:13px;line-height:1.6;color:var(--text-success);margin-top:6px">ONE OR TWO SENTENCES ON WHY</div>
</div>
<div style="border:1px solid var(--border);border-radius:12px;padding:16px;background:var(--surface-1)">
  <div style="font-size:12px;color:var(--text-muted);margin-bottom:8px">When you share</div>
  <div style="font-size:14px;line-height:1.9">
    <div><span style="display:inline-block;width:110px;color:var(--text-secondary)">send to</span>…</div>
    <div><span style="display:inline-block;width:110px;color:var(--text-secondary)">ask them to</span>…</div>
    <div><span style="display:inline-block;width:110px;color:var(--text-secondary)">worked if</span>…</div>
  </div>
</div>
</div>
```

Swap the banner variables for the other two outcomes:

- **Share privately first** — `--border-accent`, `--bg-accent`, `--text-accent`
- **Fix one thing first** — `--border-warning`, `--bg-warning`, `--text-warning`

For "fix one thing first", the second box becomes the fix, not the share plan:

```html
<div style="border:1px solid var(--border);border-radius:12px;padding:16px;background:var(--surface-1)">
  <div style="font-size:12px;color:var(--text-muted);margin-bottom:6px">The one thing</div>
  <div style="font-size:14px;line-height:1.6">THE SPECIFIC ACTION</div>
  <div style="font-size:13px;color:var(--text-secondary);margin-top:8px">About N minutes. Then run ship check again.</div>
</div>
```

Never list a second fix, even in muted text. One is the whole point.

## Review verdict

Used by `review-slice`. Verdict banner, then the gaps, then the rewritten card.

Banner colours: thin enough is green, too big is amber, no real part is amber.

Each gap is one row: the gap, then the smallest fix, then the rough time.

```html
<div style="border:1px solid var(--border-warning);border-radius:12px;padding:14px 16px;background:var(--bg-warning);margin-bottom:12px">
  <div style="font-size:14px;font-weight:500;color:var(--text-warning);margin-bottom:4px">GAP</div>
  <div style="font-size:13px;line-height:1.6;color:var(--text-warning)">Smallest fix: THE ACTION · N minutes</div>
</div>
```

Three at most. Then the rewritten Live Slice Card underneath, in the standard
style, so the person leaves with the smaller version rather than the criticism.

## Unstick

The one-hour action gets a single card, nothing else.

```html
<div style="padding:1rem 0;font-family:var(--font-sans);color:var(--text-primary)">
<div style="border:1px solid var(--border-accent);border-radius:12px;padding:20px;background:var(--bg-accent)">
  <div style="font-size:11px;color:var(--text-accent);letter-spacing:.04em;margin-bottom:4px">What stalled it</div>
  <div style="font-size:16px;font-weight:500;color:var(--text-accent);margin-bottom:12px">THE PATTERN NAME</div>
  <div style="font-size:12px;color:var(--text-accent);letter-spacing:.04em;margin-bottom:4px">Your next hour</div>
  <div style="font-size:15px;line-height:1.6;color:var(--text-accent)">THE ONE ACTION</div>
</div>
</div>
```

No diagnosis list, no pattern table, no encouragement paragraph inside the card.
Those go in the text around it, if at all.

## Writing inside cards

- Sentence case everywhere. Never title case, never capitals.
- Values are fragments, not sentences. "Sam, my co-founder" not "The first user
  will be Sam, who is my co-founder."
- Keep each value under about ten words. If it does not fit, the answer is not
  decided yet.
- No emoji anywhere.
- Two font weights only: regular and medium.

## What never goes in a card

- Explanations of the method
- Caveats and limits, which belong in the text below
- Anything the person did not decide in this conversation
- More than one highlighted row
- Congratulations
