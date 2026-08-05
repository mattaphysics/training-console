# Training Console v3.0

A hypertrophy program and autoregulating logbook for the EGYM floor at Fred Fitness.
One HTML file, works offline, installs to the iPhone home screen.

---

## The program

Four sessions, Monday / Tuesday / Thursday / Friday. Upper and lower alternate, so no
muscle is trained on consecutive days and every muscle gets 3 days of recovery mid-week
and 4 over the weekend.

| Day | Session | Exercises | Sets | Time |
|---|---|---|---|---|
| **Mon** | Upper A · chest lean | Chest press · Seated row · Shoulder press · **Crunch** · Butterfly · Reverse flys · Triceps | 25 | ~78 min |
| **Tue** | Lower A · quads + core | Leg press · Leg curl · Leg extension · Hip thrust · **Back extension · Rotary torso** | 19 | ~56 min |
| **Thu** | Upper B · back + arms | Lat pulldown · Seated row · Chest press · **Crunch** · Bicep curl · Reverse flys · Triceps | 23 | ~70 min |
| **Fri** | Lower B · glutes + core | Hip thrust · Leg curl · Leg press · **Back extension · Crunch · Rotary torso** | 19 | ~55 min |

Core appears in **every** session. On the upper days it sits mid-session rather than last:
every machine around it is seated and back-supported, so core work costs nothing there, and
anything left to the end is the first thing dropped when time runs short. On the lower days
it stays late, because leg press and hip thrust need a braced trunk.

**Weekly fractional sets:** glutes 17 · hamstrings 13 · upper back 12.5 · triceps 11.5 ·
rear delts 10.5 · chest 10 · quads 10 · biceps 9.5 · abs 9 · shoulders 7.5 · lats 7.5 ·
obliques 6 · lower back 6.

Every muscle clears the 4-set minimum effective dose and none exceeds 20, where returns
collapse. Chest, arms, posture and abs each sit above 10.

**Why four days rather than three.** Frequency itself does almost nothing for size — the
2026 Pelland meta-regression found frequency's effect on hypertrophy compatible with
negligible. Four days is a container, not a stimulus: it is simply how 86 weekly sets fit
into sessions short enough that the last set is still worth doing.

## Rest

Rest is prescribed per exercise: **3 minutes on compounds, 2 on isolations, 90 seconds on
core**. Longer rest lets you complete more reps at the same load, and those reps are where
the growth is; Schoenfeld's trial found 3-minute rests beat 1-minute for both size and
strength. Cutting rest short buys time and pays in reps.

A countdown starts automatically after every logged set, showing which set is next. Skip it
or add 30 seconds any time, and switch it off entirely in the Data tab.
---

## Which EGYM method, and why

| Method | What the machine does | Where it is used |
|---|---|---|
| **Regular** | Same resistance both directions | Almost everything. Hard straight sets are what build size. |
| **Negative** | Adds load at the turnaround, slows the lowering | One anchor lift per day, weeks 3-5 only |
| **Adaptive** | Drops resistance as you fatigue, so the set runs past failure | Last set of isolations, and the whole bonus day |
| **Isokinetic** | Fixed speed, resistance matches your effort | Rough days and deload weeks |
| Explonic | Explosive concentric | Not used — trains power, not appearance |

**Negative is deliberately rationed.** In already-trained lifters, accentuated eccentric
loading beat traditional training for force output, work capacity and muscle activation,
but *not* for hypertrophy. It costs a lot of recovery for no extra size, so it appears on
one compound per session and only once you are mid-block.

**On a Negative set you enter two numbers.** In Individual mode the machine asks for the
positive (lifting) weight and the heavier negative (lowering) weight; what it automates is
the swap between them at the turnaround, not the choice of them. The app prescribes both
and gives you two fields to log, e.g. **170 positive / 230 negative**.

The negative weight is set as a **share of your estimated 1RM**, defaulting to 90%
(adjustable 80-105% on the **Negative load** slider). That is how the research
parameterises it: eccentric muscle activity only rises measurably once the load clears
roughly 80% of 1RM, and beyond about 110% it starts eating into the lifting phase. A flat
percentage above the lifting weight would drift outside that band as the rep range changes.
A floor keeps the negative at least 20% above the positive so the set stays genuinely
accentuated. If you type a different split on the machine, the app follows your ratio.

Negative sets are charged 1.15x in the recovery model. Note this is for metabolic stress
and perceived effort, not muscle damage: creatine kinase and soreness do not actually
differ from normal sets in the meta-analytic evidence.

**Worth knowing:** for pure size, the 2026 *Sports Medicine* meta-analysis of 49 studies
found no advantage for accentuated eccentric loading over normal sets in muscle
cross-sectional area, while perceived exertion was much higher. Negative is in this program
for variety and tendon robustness, not because it grows more muscle. Weekly hard-set volume
is the lever that does that.

Block structure: weeks 1-2 all Regular · weeks 3-5 anchors go Negative · week 6 deload.

---

## Cross-device sync

Your log is committed to `data.json` in your GitHub repo, so any device with the app
shows the same data.

**Setup, once per device:**

1. GitHub → Settings → Developer settings → **Fine-grained personal access tokens** → Generate new token.
2. Repository access: **Only select repositories** → pick `training-console`.
3. Permissions → Repository permissions → **Contents: Read and write**. Nothing else.
4. Copy the token, open the app → **Data** tab → enter your username, repo name and token → **Save and sync**.

The dot in the header shows sync state: green saved, amber pending, red problem.

**Do not paste the token into `index.html`.** GitHub scans public repositories and
automatically revokes personal access tokens it finds, so a hardcoded token stops working
within hours. It also grants write access to whatever you scoped it to, which is why the
fine-grained, single-repo, contents-only token above is the right shape. The token stays
in each phone's local storage and is never written into the site or into `data.json`.

**Merging:** both sides are combined by session ID, so logging on your phone and your
laptop on the same day keeps both. If two devices write at once, the app pulls, merges and
retries automatically.

---

## Setup

1. Create a **public** repo called `training-console`.
2. Upload `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`.
3. Settings → Pages → Deploy from a branch → `main` / root.
4. On the iPhone open the Pages URL **in Safari** → Share → **Add to Home Screen**.
5. Open it once while online so it caches, then it runs offline at the gym.

## Updating

Replace `index.html` in the repo, then open the app twice with internet: the service
worker serves the cached copy first and installs the new one behind it.

## Upgrading from an earlier version

Earlier builds shipped with global intensity silently set to 92%, which quietly shaved 8%
off every number. On first launch this is reset to 100% and the same correction is applied
to your logged sessions, so **no prescribed weight changes** — the discount simply stops
being invisible. Your weights, reps and RIR are untouched. If you had deliberately chosen a
different value, it is left alone.

## Other things worth knowing

- **Weights ratchet** from what you actually lifted last time. Complete the prescribed sets
  at the bottom of the rep range or better and the load goes up; how far is scaled by
  everything you had spare — reps above the bottom of the range, plus reps still in the tank.
  It is a continuous surface, so there is no cliff between 11 reps and 12. Bottom of the
  range at true failure holds; short of the range backs off. Single steps are capped at
  +7.5%, and the rise shrinks on its own as your reserve does, so it flattens out rather
  than running away.
- **The rep stepper starts where you left off**, not at the bottom of the range.
- **Anything you type is kept** when you tap the rep stepper or an RIR button, so adjusting
  one field never clears another.
- **Charts are session-indexed**, so sessions logged minutes apart do not pile up against
  the right edge. Gridlines sit on round numbers, so every axis label is exactly where it
  says it is. The performance chart marks your average; the strength chart draws the
  smoothed estimate alongside the raw per-session points, which is why the headline number
  trails your best single session while you are climbing fast.
- **Change figures say what they measure.** A four-week comparison only appears once four
  weeks of data exist; before that it reads "over N sessions".
- **The six-week block repeats.** Weeks 1-2 Regular, 3-5 Negative on the anchors, 6 deload,
  then back to week 1 automatically.
- **Weights are validated** on entry: nothing zero, negative, or over 2000 lb can be stored,
  since one stray digit would otherwise poison the e1RM and every weight after it.
- **Global intensity** (Data tab) defaults to **100%**, meaning exactly what the program
  prescribes. Anything else is a discount you are deliberately applying, and it is shown on
  the Today screen and in the session header so it can never apply quietly. You should not
  need it: loads already come off the middle of each rep range, and the weights follow what
  you actually lift.
- **Percentages next to each weight are the real change** from the weight you lifted last
  time, not an internal adjustment factor. If rounding, the e1RM rails or an intensity
  change alter the result, it says so.
- **Backups:** the Data tab still exports and imports JSON. With sync on, the repo is
  already your backup, and every commit is a restore point.
