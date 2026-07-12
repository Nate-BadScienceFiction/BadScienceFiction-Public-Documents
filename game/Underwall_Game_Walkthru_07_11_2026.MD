# MIDDLE PLACE — THE UNDERWALL: A First-Timer's Walkthrough

Middle Place is a small desert village inside a voxel sandbox. Somewhere under its
north wall there is a buried route, an official story about that route, and a
missing companion. **The Underwall** is the quest that unfolds from those three
facts: you learn to read the ground, open the way seam by seam, catch the official
story in three lies, recover what was lost, and walk it home.

There is no quest log, no objective markers, and no dialogue trees. The world
speaks in small readable marks, one-line pins on your scan device, and a single
WATCH line in your Moon Ledger. This walkthrough tells you where to stand, what to
press, and what the game will say back — every line of UI copy quoted here is the
game's actual text.

**Spoiler note:** this document walks the whole quest. If you'd rather discover it,
read only §1–§3 (setup, controls, and how the game talks) and come back when stuck.

---

## 1. Getting in

Start the engine dev server (in the engine repo: `npm run dev`), then open:

```
http://localhost:5173/#scene=middle-place
```

The default scene is *not* Middle Place, so the `#scene=middle-place` hash matters.
Two in-game alternatives: press **Esc → Settings → scene dropdown → "Middle Place"**,
or press **0** then **R** to open the phone-booth directory and pick it there.

You spawn in the **kiln yard** at roughly (−36, 62, 9), facing north. Ahead of you
is the village's north wall; slightly right stands the domed **kiln**; about eight
blocks away to your right-front is a sandstone **drain apron** with a stone grate in
its center. This yard is the quest's home base — you will leave from it and return
to it.

**Reading coordinates:** this guide gives world coordinates like (−33, 61, 2).
Press **F3** to open the debug overlay — its `pos x= y= z=` line shows your position. North is −Z: z gets *more negative* as you head toward and under
the wall.

**Saving is automatic** (per-world, in your browser). Reload the same URL and the
quest resumes exactly where it was. Three things will *lose or leave* your
progress, so avoid them mid-quest:

- **Settings → "Clear Saved Edits"** — wipes the world's save including quest state.
- **Regenerate with a different seed** — a different seed is a different world with
  its own separate save (your old world remains and resumes if you switch back).
- **Toggling Trees or Water** — these also select a different save namespace.

---

## 2. Controls and the belt

Click the canvas to lock the mouse. **WASD** moves, mouse looks, **Space** jumps,
**F** toggles fly (allowed here — use it if you'd rather not manage ladders and
stairs), **Esc** opens Settings. After closing a panel with Esc, press any movement
key or click to re-lock the mouse.

Your ten belt slots (keys **1–9**, **0** for the tenth; mouse wheel also cycles):

| Key | Item | What it does in this quest |
|---|---|---|
| 1 | Adobe | building material (also seals wall lessons) |
| 2 | Adobe Baked | building material |
| 3 | Stone | building material |
| 4 | Sandstone | building material — later this slot is **reserved** as the port clay |
| 5 | **Moon Ledger** | press **R** to open: the clock, the WATCH line, trance/sit options |
| 6 | **Pry Bar** | **LMB** pries seams and reclaims totems; the only tool that opens authored walls |
| 7 | Tornado Laser | not used by the quest |
| 8 | **Scan Device** | **LMB** = aimed read (marks, signs, creatures, the kiln); **R** = local sweep |
| 9 | **Green-Eye Totem** | **RMB** places a glowing totem on any clear top face — your light source and your anchor marker |
| 0 | Phone Booth | scene directory (press R) |

**RMB** places the selected material; **LMB** breaks — but in Middle Place all
authored structure needs the Pry Bar, and quest seams additionally obey the quest's
own rules (§3). Interaction reach is 5 blocks. Block-picking (MMB) is disabled in
this scene.

**The field strip** — the quest's voice — is a small dark box at the lower-left
that appears **only while the Scan Device (slot 8) is selected**. It shows up to
three standing lines (**SKY**, **ROUTE**, **GROUND**), plus transient one-line
**pins** (~4–6 s), a blue control glyph when an interaction is available (e.g.
`8 · LMB READ`), and remote-contact lines from characters. Keep slot 8 in hand
whenever you're "listening."

**The Moon Ledger** (slot 5 + R) shows which half of the day you're in and the time
remaining (each half is 10 minutes real time), plus the quest's single **WATCH**
line — the current condition worth noticing. Its buttons:

- **TRANCE — LET THE DAY PASS / LET THE NIGHT PASS** — sleep to dusk / to first
  light. Refused below ground ("the ledger keeps no trance below ground") — get to
  the surface first.
- **SIT A SPELL** — advance five minutes.
- **SIT UNTIL WALL TURN / SIT UNTIL TALL SHADOWS** — appears only when you stand
  near a seam that's waiting on a night window (§6, §8); lands you 15 seconds
  before the window opens.

---

## 3. How the quest talks (read this once)

- **GROUND reads are facts; OFFICIAL reads are claims.** Fresh, lopsided marks on
  the floor tell the truth. Signs and screens that say `CERTAIN` are the official
  story — the quest is, three times, about catching them wrong.
- **Refusals are directions.** When a pry does nothing, the strip tells you exactly
  what's missing: `SEAM · READ LOCAL TRACE` means read the nearby fresh mark first;
  `SEAM · CLEAR BRACES` means outer cells first; `SEAM · WAIT FOR WALL TURN` /
  `SEAM · WAIT FOR TALL SHADOWS` mean wrong time of night; `SEAM · 6 LMB PRY` means
  wrong tool; `OLD · STILL` means this seam's chapter hasn't arrived yet.
- **Dusks drive the story.** The quest begins at your **second experienced dusk**,
  and each later chapter arms at the dusk *after* you finish the one before.
  Trances count as experienced dusks — you never have to wait in real time.
- **Nothing is missable.** Progress is monotonic and saved on every step. There are
  no fail states, no timers that punish you, and no way to lock yourself out. If in
  doubt, open the Ledger and read the WATCH line.

---

## 4. Chapter 1 — Wall Watch (two days, all of it optional)

These first lessons teach the verbs. They are genuinely optional — the story starts
at the second dusk regardless — but do them; they're short and they teach the
grammar of everything after. All of this happens within sight of spawn.

**The crooked scuff (lesson: read + seal).** A few steps south-east of the drain
apron, near a dozing field piggy, a scuff mark lies on the yard floor at
(−30.5, 61, 5.5). Select the **Scan Device (8)**, aim at it, **LMB**:

> `GROUND · FRESH · LOPSIDED · SNOUT-SCUFF`

Beside it, against the apron's east edge, is a shallow open **side throat** — three
open cells at (−31, 60, 1..3). Select any material (1–4) and **RMB** fill all
three. Partial fills pin `FOOTING · STILL OPEN`; the last one (with the scuff read,
either order) pins:

> `FOOTING · SEALED`

and the **SKY** line joins the strip's standing lines: `EAST FOOTING · PRESSED`.

**The pressed footing.** SKY named a place, not a block: cross the plaza ~20 blocks
east to the dwelling wall at x=−11. Same pair of verbs: read the fresh scuff at
(−11.5, 61, 5.5) — ignore the older, mirrored scrape nearby; reading it is harmless
but completes nothing — and seal the three-cell trench at (−12, 60, 1..3):

> `EAST FOOTING · SEALED`

**Open the Ledger.** Select slot **5**, press **R**. Opening it *is* the lesson.
Note the WATCH line: `RAMPART · TWO ORBITS AT DUSK`.

**First dusk — watch the orbit.** Trance to dusk (or wait). Stay on the surface and
just watch your two companion drones — Spitfire circling near, Spitball circling
far — for ten seconds or so:

> `COMPANION ORBIT · SPITFIRE INNER · SPITBALL OUTER`

**Day 2 — the drain will not quiet.** The WATCH line now reads
`KILN DRAIN · AIR BELOW`. In the yard just south of the grate, read the floor at
(−32.5, 61, 5.5):

> `GROUND · AIR MOVES BELOW THIS YARD`

---

## 5. Chapter 2 — The Call and Night 1 (under the yard)

**The Call.** At your **second dusk**, a pin:

> `SPITBALL · OUTER ORBIT · ABSENT`

Spitball has left the flight. Spitfire now holds a perch just above the drain
grate. The grate itself has changed — scan it: `SEAM · LOOSE · 6 LMB PRY`.

**Read the absence.** Aim the Scan Device at the **perched Spitfire** above the
drain and **LMB**. This read triggers the contact queue — a second of clear screen
between each line:

> `MISSION SERVICE · REMOTE` — *"Inventory correction in progress. Surface route not advised."*
> `HARRIET · OFF-SITE · WEAK LINK` — *"I cannot reach Spitball. Read what it touched."*

**Phrase one — match the light.** Spitfire's underside now repeats a rhythm: three
quick 0.35-second flashes (at 0 s, 1.3 s, 2.6 s of every 8-second cycle), then a
long rest. Keep the Scan Device aimed at Spitfire (glyph: `8 · LMB MATCH`) and
**LMB once on each flash** — three taps, each within ±0.4 s of a flash, one tap per
flash. Watch a full cycle first to get the feel; a mistimed click just does
nothing. You'll see `MOTION · 1/3`, `MOTION · 2/3`, then:

> `MOTION · KNOWN`

Your strip gains the **ROUTE** line — the quest's honest compass. It gives a
bearing with an error bracket and a distance (`FRESH CUT · <bearing>° ±<error>° ·
~<distance>m`), never a tracking dot. Two idle states are normal: `NO TARGET`
until you've read something worth pointing at, and `FIND AN ANCHOR` whenever you
stand between reference fields (it speaks bearings only within ~16 blocks of the
entrance or far exit, or ~10 blocks of an anchored ring). `FIND AN ANCHOR`
mid-corridor is not an instruction to stop — keep following the tunnel to the next
junction.

**Open S1 — the entrance seam (Pry Bar, 12 cells).** Select the **Pry Bar (6)** and
work top-down:

1. the **grate** at (−33, 60, 2);
2. the 1-wide **neck** below it: (−33, 60, 1) and (−33, 59, 1);
3. the 3×3 **face** behind: x −34..−32, y 58..60, at z=0.

Each legal cell breaks in one hit. Below opens a 3-wide stair descending north
under the kiln, ~17 blocks down to a tunnel floor at y=40. A pale one-block clay
**dry stripe** runs down the center line — it is the breadcrumb through everything
below; it stops at every closed seam.

*(Order note: you may pry S1 before doing phrase one — Spitfire simply relocates to
a landing perch partway down and everything above happens there. If you cross into
the dark early you get one `ENTRANCE · SPITFIRE WAITS` pin, and the Ledger's WATCH
line carries it until you calibrate.)*

**The fresh cut.** At the stair foot, a floor mark at (−32.5, 41, −19.5). Read it:

> `GROUND · FRESH · LOPSIDED`

ROUTE accepts it: `FRESH CUT · …° · ~…m`, pointing deeper north — and Harriet's
threshold line arrives:

> `HARRIET · OFF-SITE · WEAK LINK` — *"Underground, the sky is a rumor. Trust what leaves a mark."*

Optional but wise: place a **totem (9 + RMB)** on the floor here — your first work
light.

**J1 — the first junction, and the first lie.** Follow the bore ~15 blocks north to
a 5×5 bay centered (−33, 40, −33). Three things are here:

- An **official sign** on the west wall at (−34.6, 42.5, −32.5). Read it:
  `OFFICIAL · CONDUIT WEST · CERTAIN`. It claims the way is west.
- A **fresh floor spoor** between the ring and the north wall at (−33.5, 41, −34.5).
  Read it: `GROUND · FRESH · LOPSIDED`. **This read exposes contradiction C1** —
  the fresh trace runs north, not west.
- A faint **sandstone ring** on the bay floor — your first anchor ring.

(Prying the north face before reading the spoor refuses: `SEAM · READ LOCAL TRACE`.)

**Open S2** — the clay 3×4 face on the **north** wall (x −34..−32, y 41..44, at
z=−36), 12 cells with the Pry Bar.

**Anchor J1** — select the **totem (9)** and **RMB** one onto the floor inside the
ring (dead center (−33, 41, −33) works). An anchored ring steadies ROUTE's bearing
brackets from here on.

**Chapter close.** With the calls heard, phrase one done, C1 exposed, S1 and S2
open, and J1 anchored (any order):

> `UNDERWALL · QUIET UNTIL NEXT DUSK`

ROUTE resets to `HOME`. Surface, sleep, and let the next dusk come.

*Optional: the west face the sign pointed at (W1) can also be pried — 18 cells into
a small dead pocket. A read inside says `GROUND · THIS ROOM KEEPS NOTHING`. The
official story leads nowhere; that's the point.*

---

## 6. Chapter 3 — Night 2 (under the wall, and the false relay)

At the dusk after the chapter close, the WATCH line arms Night 2:

> `FIRST ANCHOR · FRESH DUST`

**The dust fan.** Back at J1, a fresh dust fan has appeared a block east of the
old spoor (which remains), at (−32.5, 41, −34.5). Read it — ROUTE turns to `DUST FAN`, pointing through S2 toward
(−33, 39, −58).

**S3 — the wall-line seam (braces by hand, cap by the clock).** Follow the bore
north through S2. The floor ramps down at z=−57..−59 into the **under-wall dip**
(floor y=37) — you are passing beneath the village wall itself. In the dip, at the
wall-line plane **z=−64**, is a stone 3×4 face:

1. **Braces first (any time tonight):** with the Pry Bar, clear the **two floor
   braces** in front of the face — (−34, 38, −63) and (−32, 38, −63) — then the
   **8-cell outer ring** of the face (the 3×4 minus its center 2×2:
   bottom row y38 x −34..−32, sides y39–40 at x=−32, top row y41 x −34..−32).
2. **The gate 2×2 by the clock:** the center four cells (x −34..−33 × y 39..40)
   open **only during WALL TURN** — a ~30-second window each night. Stand near the
   face, open the **Moon Ledger**, and press **SIT UNTIL WALL TURN** — you wake 15
   seconds before it. When the Ledger line reads `WALL TURN · OPEN NOW`, pry all
   four gate cells. Too early pins `SEAM · WAIT FOR WALL TURN`; braces uncleared
   pins `SEAM · CLEAR BRACES`.

**J2 — the moonlit junction.** Past S3 the bore continues north to z=−81, then jogs
**west** and north into a bay centered (−45, 40, −88) — a thin shaft of real night
sky falls through a 1×1 lightwell. **Anchor the ring** (totem on the ring floor).

**The false relay — the second lie.** On J2's wall a sign reads
`OFFICIAL · RELAY WEST · CERTAIN`; ROUTE accepts `OFFICIAL RELAY`. Follow the
official conduit west to a chamber around (−82, 40, −88). On its back wall glows a
**relay screen**; mid-chamber, a few blocks south of the screen, lies an old,
swept floor mark.

For the first two seconds after you enter, the screen's official prompt is
"speaking" — scanning the screen during it counts as accepting the claim
(`OFFICIAL CLAIM · UNVERIFIED`, a counted refusal, nothing lost; the prompt then
takes five seconds to speak again). Instead: stand in the room, let those two
seconds pass untouched, then **read the floor spoor** at (−82.5, 41, −87.5):

> `GROUND · OLD · MIRRORED · SWEPT — LOCAL FACT HOLDS`

That's **C2**: the room the official story calls a live relay is an old, swept,
mirrored fake. *(Optional, for the Almanac's GROUND section: read the dusted floor
on the chamber's west side at (−80.5, 41, −90.5) — the sign that someone keeps
this room swept.)*

**The Qyber frame.** Now scan the **relay screen** itself. A full-screen frame
opens — the quest's only modal: an official service map (`SERVICE MAP · CORRIDOR
CLEAN · CERTAIN`) with one wrong detail frozen in its lower-right corner — the
village wall seen **from outside**. For the first second there's no way to close
it; then `LMB · RETURN` appears. Click (or Esc). Closing it commits, all at once:

- the **far route is known** (this unlocks S4),
- ROUTE turns to `WRONG CORNER` — walk to the chamber's south-west corner and find
  *nothing there*; the frame's corner was the tell, and
- the **signal burn**: until dawn, the underpath's two honest-sky spots (the
  entrance shaft and J2's lightwell) read SKY `NO FIX`; on the surface SKY still
  reads `HOME`.

A breath after the frame closes, Penelope's line arrives:

> `MISSION SERVICE · REMOTE` — *"Assistance was rendered. The route was corrected."*

**S4 — the back seam.** Behind the screen, on the chamber's north wall at z=−93, a
dirt 3×4 (x −83..−81, y 41..44). With the frame reviewed it pries freely (before,
it refuses `SEAM · READ LOCAL TRACE`).

**J3 — the last junction.** The corridor behind S4 runs north, then jogs **east**
into a bay centered (−60, 40, −110). **Anchor the ring.** With C2 exposed, the
frame reviewed, S3 + S4 open, and J2 + J3 anchored:

> `KILN · PORT CLAY AT FIRST LIGHT`

---

## 7. Chapter 4 — First light at the kiln (the rehearsal)

Surface and trance to first light (the daylight after the night you closed
chapter 3 — before it, the kiln row reads `PORT SEAL · KILN COLD UNTIL FIRST
LIGHT`).

**Prepare the seal.** At the kiln, aim the **Scan Device** at it and **LMB** — the
materials panel opens with a quest row on top: **`PREPARE PORT SEAL`**. Click it.

> `PORT CLAY · REHEARSAL PENDING`

Belt **slot 4 is now reserved**: it holds raw adobe — the port clay — labeled
`· PORT` in the panel, and it refuses reassignment (a red flash if you try) until
the quest ends. Your own material choice underneath survives untouched.

**The practice socket.** Just west of the drain apron is a marked socket cell at
(−36, 61, 2); Spitfire watches from a kiln perch. Spitfire's underside now
demonstrates the **answering double-pulse**: pulse, pulse, rest — two quick 0.3 s
flashes half a second apart, repeating every 6 seconds.

Select **slot 4**, aim at the ground cell beneath the socket, and **RMB on the
answer** — any moment within ~3 seconds after the *second* flash begins. The placed
block always lifts away again on its own (rehearsal clay never stays). Wrong
material pins `SOCKET · THE PORT CLAY ANSWERS`; wrong moment pins
`SOCKET · PLACE ON THE ANSWER`. On the answer:

> `PORT SEAL · PREPARED`

The WATCH line turns to `UNDERWALL · FAR TRACE AT NEXT DUSK`. Sleep.

---

## 8. Chapter 5 — Night 3 (the far exit and the third lie)

At the next dusk: WATCH `LAST ANCHOR · FAR TRACE`.

**The far trace.** At J3, a fresh scorch lies at (−59.5, 41, −110.5) — read it from
the **north** side (your anchor totem blocks the southern sightline). ROUTE
accepts `FAR EXIT`, pointing far north to (−60, 41, −186).

**The long leg.** From J3 the corridor runs north. At z≈−139..−143 the floor simply
isn't there — the **arroyo undercut**, a harmless 4-deep drop; cross it, or drop in
and climb the three stone steps on the east wall. Then the **collapse chamber**,
the far bore, and finally a 3-wide **stair rising north** (from z=−182 up to
z=−198) into a narrow one-wide neck and a small 2×2 **exit well**, capped by four
sandstone cells at grade — seam **S5**.

**S5 prep (12 cells, any time tonight):** with the Pry Bar, clear the 3-wide face
at z=−199 (x −61..−59, y 58..60) and the three neck cells above the stair
((−60, 59, −200), (−60, 60, −200), (−60, 60, −201)). Work upward — each course
opens the aim path to the next. The four **grade cells** on top (x −61..−60,
z −203..−202, y 60) are the gate — they refuse until the third contradiction is
resolved (`SEAM · READ LOCAL TRACE`) and outside their window
(`SEAM · WAIT FOR TALL SHADOWS`).

**C3 — the last examination.** Three things must all be true, in any order, and
the shaft is built so one sitting covers them:

1. **The official claim latches by itself** at night-second 450 — a receiver plate
   on the stair-head wall then reads `OFFICIAL · LAST SKY 285° · CERTAIN`. (During
   that stretch of night the shaft's SKY line shows the same too-clean claim.)
2. **Read the fresh scorch** on the neck landing at (−60.5, 58, −197.5):
   `GROUND · FRESH · LOPSIDED`.
3. **Receive one of Spitball's pulses while standing in the shaft** — a distant
   pulse arrives every 60 night-seconds, with a guaranteed one at second 500.

The easy recipe: stand by the cap, open the Ledger, **SIT UNTIL TALL SHADOWS** (you
wake at second 495), stay in the shaft a few seconds (the 500 pulse lands), read
the scorch. The moment all three hold:

> `OFFICIAL CLAIM · STRUCK — ROUTE ACCEPTS PULSE`

ROUTE turns to `PULSE`. The official sky-fix was pointing 285°; the pulse is real
and it isn't coming from there.

**Open the cap.** **TALL SHADOWS** is the last phase of the night (seconds
510–600). Pry the four grade cells and climb out — you emerge on the **far shore**,
outside the wall, for the first time.

**The emergence walk.** As you first stand outside the wall, a one-time pin notes
it: `SKY · OUTER SIGNAL · OCCLUDED`. ROUTE now reads quantized pulse bearings
(`PULSE · ~330° ±10°` style). Follow them ~50 blocks **north-west** (z still more
negative, drifting west); two fresh scorches along the way at (−67.5, 61, −215.5)
and (−77.5, 62, −233.5) confirm the line. Within ten blocks of the destination:
`PULSE · ARRIVED`.

---

## 9. Chapter 6 — The handshake (recovering Spitball)

At (−85, 62, −248) stands a small three-walled **alcove**, open to the south: two
stone jambs, a lintel, a marked empty cell between them — the **port frame** — and,
grounded before it, **Spitball itself**, dark and still. Early reads here are
honest: scanning Spitball before the work pins
`RECALL CHANNEL HOLDS · NO LOCAL REPLY`. *(Optional, for the Almanac: a heat trace
beside the frame at (−84.4, 62, −249.5) reads
`GROUND · REOPENED MANY TIMES. NOTHING EVER CAME.`)*

The handshake goes live when you stand near the frame **at night** with S5 opened
and C3 struck (arriving near dawn is forgiven — a latched grace holds ~5 minutes
past first light). Three phrases, strictly in order; a miss only retries the
current phrase after a 5-second pause; two misses on one phrase slow the rhythm
down for you (`· SLOW PULSE`) — there is no fail state and no retry limit.

**Phrase one — "I see your true motion."** Spitball's underside light now carries a
steady beat — one flash every 2 seconds. As with Spitfire long ago: Scan Device
aimed at Spitball, **LMB on three different flashes** (±0.4 s each — skipping
flashes between accepted taps costs nothing).
`MOTION · 1/3 → 2/3 →`:

> `MOTION · KNOWN`

(Off the beat: `MOTION · OFF THE PULSE`, five seconds, try again.)

**Phrase two — "I refuse the clean channel."** A bright official recall prompt now
pulses over the frame; the glyph reads `WAIT · CLEAN PULSE`. **Don't click it** —
exactly as at the relay. Let one full bright cycle pass; when it dims, Spitball's
underside light goes dark and the glyph switches to `8 · LMB READ`. Read the floor
spoor at Spitball's feet (−85.5, 62, −246.5):

> `CHANNEL · REFUSED — 4 · RMB PORT`

(Clicking the bright prompt: `OFFICIAL CLAIM · UNVERIFIED` — a miss; phrase one is
not undone.)

**Phrase three — "Close the door when you answer."** Spitball's light switches to
the **answering double-pulse** you rehearsed at the kiln. Select **slot 4**, stand
before the frame, aim at the wall cell behind the marked port face, and **RMB
within the window after the second flash** (3 seconds at base assist, wider if
slowed). Wrong timing: `PORT · ON THE ANSWER`; wrong material: `PORT · RAW ADOBE`.
On the answer:

> `PORT · PLUG SET — HOME`

Spitball wakes, carries the plug, and falls in behind you. ROUTE reads `HOME`; the
Ledger reads `HOME · SPITBALL FOLLOWS`. Scanning Spitball now: `PORT · PLUG HOLDS`.

---

## 10. Chapter 7 — The walk home and the fired seal

Spitball follows you home **through the underpath**, advancing checkpoint by
checkpoint as you cross them — in order: the far-exit well, the stair foot, the
collapse chamber, the arroyo, J3, J2, the under-wall dip, J1, the entrance stair
foot, the kiln yard. Pass within a few blocks of each; you cannot skip ahead, and
every crossing saves.

**The one branch:** Spitball will not pretend to follow across the surface. If you
cross the far-exit well and then wander on overland, the Ledger flips to
`FAR EXIT · SPITBALL WAITS BELOW` and the kiln shows
`PORT SEAL · SPITBALL WAITS AT FAR EXIT`; if you skip the well entirely the lines
simply stay `HOME · SPITBALL FOLLOWS` / `PORT SEAL · SPITBALL RETURNING` while it
holds at its last checkpoint. Either way the remedy is the same: come back and
take the underpath; it resumes instantly.

**Penelope's question.** As you re-enter the false relay chamber on the way home,
one line arrives, once:

> `MISSION SERVICE · REMOTE` — *"Did I keep the wall?"*

Nothing follows it — no menu, no timer. **Silence is a permanent, valid answer.**
If you want to answer: a small sandstone **answer ring** has been on the chamber
floor all along (centered (−84, 40, −88), two blocks west of center) — the new
thing is the glyph it now offers: `9 · RMB LEAVE LIGHT`. Place a **totem** in it:

> `ANSWER · LIGHT LEFT`

*Pitfall:* if you happened to leave a totem there earlier in the quest, it does
**not** count — the game pins `OLD LIGHT; LIFT, THEN LEAVE`. Pry the old one out
and place a fresh totem in the ring. Only a light placed *after* the question
answers it (strictly, any fresh post-question totem in the ring counts — lifting
the old one first is the invited courtesy).

**Fire the seal.** Home in the kiln yard, scan the **kiln**. While Spitball is
still in transit the row reads `PORT SEAL · SPITBALL RETURNING` (disabled) — an
honest refusal, not a hidden gate. Wait for Spitball to settle beside you (seconds,
once you've stopped), and with both of you at the kiln the row becomes:

> **`FIRE PORT SEAL`**

Click it. The plug bakes mud-brown to red:

> `PORT SEAL · FIRED — BAKED RED`

The reserved slot 4 releases, the two drones resume their old paired orbit, and the
quest is complete.

---

## 11. Epilogue — the Almanac

After the completion cues clear, one last pin: `UNDERWALL ALMANAC · NEW PAGE`.
Open the Ledger (5 + R). The **UNDERWALL
ALMANAC** renders whole — three titled sections recording everything you did:

- **THE WAY** — the drain, the junctions you anchored, the reviewed relay, the far
  exit, the answered port, the three contradictions.
- **THE GROUND** — the loneliness signs you chose to read (the swept room; the port
  reopened many times, nothing ever came).
- **THE SERVICE** — three conduct lines, the question, your answer
  (`answer — light left` or `answer — silence`), and the closing entry:

> `service day 11,342 — attendance: two`

The underpath stays open. The village keeps its nights. Nothing is scored. Walk the
rampart at dusk and watch two orbits, one inner, one outer.

---

## Appendix A — Am I where I think I am? (stage checklist)

| If the Ledger WATCH says… | You are… | Next move |
|---|---|---|
| `RAMPART · TWO ORBITS AT DUSK` / `KILN DRAIN · AIR BELOW` | in Wall Watch (ch. 1) | do the lessons; reach the 2nd dusk |
| *(after the absence pin)* | in the Call (ch. 2) | read Spitfire, tap the rhythm, open S1 |
| `ENTRANCE · SPITFIRE WAITS` | underground before calibrating | go back to Spitfire's perch and finish phrase one |
| `UNDERWALL · QUIET UNTIL NEXT DUSK` | Night 1 done | trance to the next dusk |
| `FIRST ANCHOR · FRESH DUST` | Night 2 armed (ch. 3) | dust fan → S3 → relay |
| `KILN · PORT CLAY AT FIRST LIGHT` | Night 2 done | trance to daylight, go to the kiln |
| `KILN SOCKET · PORT CLAY READY` | rehearsal armed (ch. 4) | slot 4 on the socket's answer |
| `UNDERWALL · FAR TRACE AT NEXT DUSK` | rehearsal done | trance to dusk |
| `LAST ANCHOR · FAR TRACE` | Night 3 armed (ch. 5) | J3 scorch → far exit → C3 → S5 |
| `LAST JUNCTION · FAR TRACE · RING EMPTY` | Night 3 armed but you reclaimed J3's totem | re-anchor the J3 ring first |
| `HOME · SPITBALL FOLLOWS` | recovered (ch. 7) | walk the underpath home |
| `FAR EXIT · SPITBALL WAITS BELOW` | you left it behind | go back to the far exit |
| `UNDERWALL ALMANAC · NEW PAGE` | done | open the Ledger |

## Appendix B — Refusals decoded

| Line | Meaning |
|---|---|
| `DRAIN GRATE · FIXED` | the grate opens only after the Call |
| `OLD · STILL` | this seam's chapter hasn't armed yet — wait for its dusk |
| `SEAM · READ LOCAL TRACE` | read the fresh mark near this seam first (S2: the J1 spoor · S4: review the frame · S5 gate: resolve C3) |
| `SEAM · CLEAR BRACES` | outer prep cells before the center gate |
| `SEAM · WAIT FOR WALL TURN` | S3's gate opens ~30 s mid-night — use SIT UNTIL WALL TURN |
| `SEAM · WAIT FOR TALL SHADOWS` | S5's gate opens in the night's last phase — use SIT UNTIL TALL SHADOWS |
| `SEAM · 6 LMB PRY` | seams answer only the Pry Bar |
| `DEAD ROCK · PRY SKIPS` | the deep rock is not diggable — the route is elsewhere |
| `OFFICIAL CLAIM · UNVERIFIED` | you clicked a bright official prompt — wait it out instead |
| `… CLAIM STILL SPEAKING` | truthful early read — let the prompt finish, then read again |
| `SOCKET/PORT · …` lines | rehearsal/handshake coaching — material or timing |
| `<…> · PLAYER BLOCKS OBSTRUCT` (glyph `6 · LMB RECLAIM`) | your own placed blocks cover a needed mark/ring/socket — pry them back |

## Appendix C — Landmarks (x, y, z)

| Place | Where |
|---|---|
| Spawn / kiln yard | (−36.5, 62, 9.5) |
| Drain grate (S1, the way down) | (−33, 60, 2) |
| Kiln | (−34, 61, −5) |
| Stair foot / fresh cut | (−33, 41, −18) |
| J1 (first ring) | (−33, 40, −33) |
| S3 (wall-line seam) | z = −64, in the dip |
| J2 (lightwell ring) | (−45, 40, −88) |
| False relay chamber | (−82, 40, −88) |
| S4 (back seam) | z = −93 behind the relay |
| J3 (last ring) | (−60, 40, −110) |
| Far-exit shaft / S5 | (−60, 58, −199), well at z −202/−203 |
| Port frame (Spitball) | (−85, 62, −248) |

*Every fact in this guide was checked against the shipped implementation (engine
runtime + the verified in-app gate scripts). If the game ever seems to disagree
with this document, trust the game — and the Ledger's WATCH line.*
