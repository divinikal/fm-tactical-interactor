# fm-tactical-interactor

# FM Tactical Interactor

### A positional play analysis tool for Football Manager Mobile

-----

## What Is This?

A tactical tool that lets you build a lineup of FM roles, pick a game plan, and see how your team’s shape looks **with the ball** and **without the ball** — on a numbered pitch grid.

It’s built on two ideas:

1. **Positional play** — your team’s shape in possession follows real spatial rules (Guardiola’s framework adapted for FM). The tool checks those rules and flags problems.
1. **Role zone mapping** — every FM role has zones it naturally inhabits, moves into, and occasionally appears in. The tool knows where every role lives on the pitch and shifts those zones based on your game plan.

-----

## The Pitch Grid

The tool uses a **20-zone pitch grid** based on a horizontal layout (attack on the left, defence on the right):

```
| Attacking Third | Build-Up | Mid-Block | Defensive Third |
|    16    |  11  |  6  |  1  |   ← Top/Left flank
|  17a 17bc| 12   |  7  |  2  |
|  18a 18b | 13   |  8  |  3  |   ← Centre
|  19a 19bc| 14   |  9  |  4  |
|    20    |  15  | 10  |  5  |   ← Bottom/Right flank
```

**Key zones to know:**

- **18b** — Six-yard box. Highest goal threat.
- **13** — Centre circle. Possession hub. Pivot zone.
- **7, 9, 12, 14** — Half-spaces. The most dangerous zones to exploit or leave empty.
- **2, 4** — Wide defensive channels. Where CBs and fullbacks live.
- **17a, 19a** — Pre-box channels. Where chances are created.

-----

## How to Use It

### Step 1 — Build your lineup

**Option A — Manual Build:**
Pick a Position Group → Role → Side (Left / Centre / Right) → Add

**Option B — Use a Formation:**
Click any preset formation. It loads a default set of roles that you can then customise.

Available presets: 4-4-2, 4-4-2 Diamond, 4-3-3, 4-2-3-1, 4-1-4-1, 4-5-1, 4-3-2-1, 3-5-2, 3-4-3, 3-4-2-1, 3-3-3-1, 3-1-4-2, 5-3-2, 5-4-1, 5-2-3

**Rules for adding roles:**

- Max 11 players
- Same role + same side = blocked (duplicate)
- Same role, different side = allowed (e.g. CB Left + CB Right)
- L/R roles mirror automatically — a Right Winger maps to zones 20, 19a etc.
- Centre roles expand symmetrically — a Centre CM covers both z12 and z14

### Step 2 — Pick a game plan

|Game Plan    |What it means                                                              |
|-------------|---------------------------------------------------------------------------|
|**Contain**  |Park the bus. Shape barely changes whether you have the ball or not.       |
|**Defensive**|Hard to beat. Compact block, counter when you can.                         |
|**Counter**  |Absorb and explode. Tight defensively, direct and vertical when you win it.|
|**Control**  |We’re in charge. Patient build-up, mid-high press, structured.             |
|**Attacking**|Take the game to them. Most players push forward. Accept risk.             |
|**Overload** |All in. Every player as far forward as possible. You will be exposed.      |

### Step 3 — Toggle the views

|View                       |What you see                                    |
|---------------------------|------------------------------------------------|
|**Starting Shape**         |Where roles naturally sit — no mentality applied|
|**With the Ball (IPF)**    |How your shape looks when you have possession   |
|**Without the Ball (OOPF)**|How your shape compresses when you’re defending |

-----

## Reading the Grid

### Zone colours

|Colour              |Meaning                                               |
|--------------------|------------------------------------------------------|
|🟢 Green (1 player)  |One role covers this zone — clean ownership           |
|🟡 Yellow (2 players)|Two roles overlap — good for combinations             |
|🔴 Red (crowded)     |Three or more roles stacking — positional problem     |
|🔵 Blue (no cover)   |Someone *should* be there but isn’t based on the shape|
|⚫ Empty             |Zone genuinely outside your team’s reach              |

### Colour dots

Each role has a unique colour dot. Where you see dots in a zone, those are the roles occupying it. Hover over a dot to see which role it is.

-----

## The Analysis Cards

### 📊 Pitch Covered %

How much of the 23 zones your shape reaches. 75%+ = good. Below 50% = your team is very compact (which may be intentional on Contain/Defensive).

### ↔️ Shape Shift

How different your “With the Ball” shape is from your “Without the Ball” shape.

- **Small** = stable, consistent shape, low transition risk
- **Medium** = manageable, players need to be fit and organised
- **Large/Extreme** = big difference, you’ll be exposed on counters

### 🚨 Shape Problems

Positional issues the tool has detected. Each one tells you what the problem is and what it means tactically. See the “Positional Rules” section below for what each rule checks.

### ✅ Shape Checks Passed

Every rule your shape passes. Shows what’s working.

### 🤝 Key Combinations

Pairs of roles that share zones — these are your natural passing combinations on the pitch.

### 🕳 Uncovered Zones

Zones nobody is reaching. Broken down by third so you can see if you’re exposed in attack, midfield or defence.

### ⚠️ / ✅ Likelihood Cards

How confident the tool is that each role actually executes the shape change when the game plan demands it. Driven by role mobility, game plan intensity and positional discipline.

- **Green (70%+)** = reliable — this role consistently reaches its intended zones
- **Yellow (45–69%)** = decent — usually gets there
- **Orange (<45%)** = unreliable — this role may not execute the shape shift consistently

Only roles that *need* to move (non-zero shift) appear here. Static roles like GK are excluded.

-----

## The Likelihood Numbers (IPF / DEF)

On each player tag you’ll see two percentages once a game plan is selected:

- **IPF %** — how likely this role reaches its attacking shape zones
- **DEF %** — how likely this role reaches its defensive shape zones

These are estimates based on three things:

1. **Mobility** — how much this role naturally roams (1=stays put, 3=covers huge distance)
1. **Game plan intensity** — Overload demands more movement than Counter
1. **Discipline** — how reliably this role type follows positional instructions (Anchor = very disciplined, Trequartista = does what it wants)

-----

## Positional Rules the Tool Checks

These are the principles the tool uses to flag problems. Based on positional play / Juego de Posición principles.

|Rule                                         |What it checks                                                                                                                                           |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
|**Lane spacing**                             |No more than 2 players in the same vertical lane. More than 2 = congestion, no passing angles.                                                           |
|**5 lanes occupied** (IPF only)              |All 5 width zones should have someone — Far Left, Left Half-space, Centre, Right Half-space, Far Right. Empty lanes = you’re not stretching the opponent.|
|**Vertical depth**                           |Players must occupy all 3 horizontal lines (top, middle, bottom). A flat shape has no depth and is easy to press.                                        |
|**Rest defence**                             |At least 2 players behind the ball in possession (3 minimum out of possession).                                                                          |
|**Zone overcrowding**                        |No zone should have 3+ players. Too many players doing the same job = wasted.                                                                            |
|**Flank coverage** (IPF only)                |Both wide channels must have someone. Uncovered flanks = free crossing lanes for the opponent.                                                           |
|**Half-space occupation**                    |Zones 7, 9, 12, 14 must have at least 1 player. These are the most dangerous zones in football — leave them empty at your peril.                         |
|**Horizontal flatness**                      |No more than 3 players on the same horizontal line. Flat lines = no combinations, no depth.                                                              |
|**Front line** (IPF, Attacking/Overload only)|On aggressive game plans, at least 4–5 players should reach the final third.                                                                             |
|**Defensive block** (OOPF only)              |At least 3 players in the midfield block (zones 7–14). Thin mid-block = opposition plays straight through you.                                           |
|**Shape stretch** (OOPF only)                |If players are in the final third but your defensive line is thin, you’re exposed.                                                                       |

-----

## Left / Right / Centre — How Sides Work

All role zone data is written from the **Left perspective**. When you add a role:

- **Left** — zones used as defined (e.g. Winger Left → zones 11, 16, 17a)
- **Right** — zones automatically mirrored (e.g. Winger Right → zones 15, 20, 19a)
- **Centre** — zones expanded symmetrically (e.g. CM Centre → covers both z12 and z14, z7 and z9)

This means the same role definition covers all three sides correctly without duplication.

-----

## How Game Plans Shift Shapes

The tool applies different logic for in-possession and out-of-possession shifts:

**In Possession (IPF)** — all roles shift forward by a set number of columns, scaled by mobility. High-mobility roles (WB, BBM, RPM) shift further. Low-mobility roles (GK, Anchor, Poacher) barely move.

**Out of Possession (OOPF)** — roles behave differently based on their type:

- **Defenders** (GK, CB, FB, DM, Anchor) — drop backward to hold the defensive line
- **Midfielders** (CM, Wide Mid, Winger, BWM) — hold position or drop slightly
- **Attackers** (AM, Strikers, Inside Forwards) — press forward to win the ball high

Defenders also have **positional floors** — they can never be pushed out of their defensive zone regardless of how aggressive the game plan is.

-----

## Role Sectors

|Sector         |Roles                                                                                                          |
|---------------|---------------------------------------------------------------------------------------------------------------|
|Goalkeeper     |GK, SK                                                                                                         |
|Centre Back    |CB, Wide CB, BPD, NCB, Sweeper, Libero                                                                         |
|Fullback       |FB, WB, IFB, IWB, DFB                                                                                          |
|Flanker        |Winger, Inverted Winger, Wide Mid, Defensive Winger                                                            |
|DM             |DM, Anchor, DLP, BBM, RPM, BWM                                                                                 |
|Central Mid    |CM, AP, DLP, BBM, DM, RPM, Anchor, BWM                                                                         |
|Wing Attack    |Winger, Inverted Winger, Inside Forward, AP (Wing)                                                             |
|Central Attack |AM, AP, Shadow Striker, Trequartista                                                                           |
|Wide Striker   |Inside Forward, Advanced Forward, Pressing Forward                                                             |
|Central Striker|Poacher, Advanced Forward, Pressing Forward, Target Forward, Trequartista, Deep Lying Forward, Complete Forward|

*Note: Some roles appear in multiple sectors (e.g. DLP appears in DM and Central Mid). They map to different zones depending on which sector you pick.*

-----

## Companion Tool

This tool comes with a companion reference — **FM Role Zone Map** — which lets you look up any individual role and see exactly which zones it homes in, moves to, and can occasionally appear in. Useful for understanding a role before building it into your lineup.

-----

## Built by

Nick (Nicodemus Okoh) + Claude  
Seoul FC · K League · FM Mobile  
March 2026
