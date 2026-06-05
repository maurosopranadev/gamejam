# gamejam
vBrowser card game with narrative choices, recruitable classes and a boss battle — built with AI assistance and balanced via Monte Carlo simulation.


# ⚔️ Guild Master

> *Every choice has a price. Every guild has a fate.*

A browser-based narrative card game inspired by Reigns, built as a solo project 
to explore AI-assisted development, game design decision-making, and data-driven 
balancing techniques.

**🎮 [Play it live](https://guildmasterjam.netlify.app)**  
**🏆 Submitted to itch.io Game Jam — [View page](https://maurosoprana.itch.io/guild-master)**

---

## About the Project

Guild Master was built as part of a personal experiment to test AI tools 
(Claude by Anthropic) in a real creative workflow — understanding their 
capabilities, limits, and how to direct them effectively toward a product vision.

The result is a fully playable game with:
- Global leaderboard (Supabase)
- Original chiptune soundtrack via Web Audio API
- Boss battle with turn-based mechanics
- Persistent legacy system across runs

---

## Product & Design Decisions

This section documents the key decisions I made as the product owner, 
designer, and director of this project.

### 🎴 Card System Design
- 36+ base cards with narrative consequences
- Every card effect was reviewed for **narrative consistency** — 
  if the story says "refuse the contract," the stats should reflect 
  that decision, not punish the player with unrelated penalties
- Memory system: past choices return as new cards 3+ turns later,
  creating a cause-and-effect narrative loop

### 👥 Recruit & Evolution System
- 5 recruitable classes (Mage, Archer, Cleric, Rogue, Knight)
- Each evolves into a more powerful class after 15 days survived
- Evolution denial bug identified by players → fixed with a 
  10-day cooldown before re-offering, preventing an infinite loop
- Dead recruit slots reopen for new recruitment — 
  discovered via player feedback that this wasn't working

### ⚔️ Boss Fight Design
- Three escalating neutral narrative cards before the final battle
  (no yes/no choice — just atmosphere building)
- Turn-based combat using the same swipe mechanic:
  ATTACK scales with Control stat + alive recruits + evolved status
  DEFEND recovers your lowest stat
- Distinct boss music and 3-stage SFX system (each reveal more intense)

### 📊 Balance — Monte Carlo Simulation
One of the most technically interesting decisions in this project.

Rather than guessing whether the game was balanced, I ran a 
**Monte Carlo simulation of 5,000 random playthroughs** to measure 
stat pressure across all cards.

**Before rebalancing:**
| Death cause     | Frequency |
|----------------|-----------|
| Control max     | 41.8%     |
| Gold zero       | 32.9%     |
| Morale zero     | 14.4%     |
| Renown max/zero | ~8%       |

Control was responsible for 42% of all deaths on random play —
meaning the stat drifted naturally toward 100 with no player input.

**After rebalancing:**
| Death cause     | Frequency |
|----------------|-----------|
| Gold zero       | 38.0%     |
| Morale zero     | 22.0%     |
| Control max     | 14.5%     |
| Renown max/zero | ~18%      |

13 targeted card fixes were applied to Control gains,
6 to Gold losses, and 11 Renown gains were reduced.

### 🎨 UI/UX Decisions
- **Floating +/- delta numbers** on stat bars after each decision —
  consequences visible without spoiling them before the choice
- **Warning icons** (▼▲) appear when any stat reaches danger zone (≤15 or ≥85)
- **Cause of death highlighted** on the final screen after player feedback
  showed players couldn't identify which stat killed them
- **Toast duration** extended after playtest feedback that messages 
  disappeared before players could read them
- **Volume slider** added to HUD — mute alone wasn't enough for players 
  who wanted low background music

### 🌐 Infrastructure
- Single HTML file (~130kb) — no build tools, no dependencies
- Deployed on **Netlify** (static hosting)
- Global leaderboard via **Supabase** (PostgreSQL + REST API)
- Row Level Security policies configured to allow public read/insert/delete
- Leaderboard capped at 10 entries with automatic pruning of lowest score

---

## Technical Stack

| Layer | Technology |
|-------|-----------|
| Game logic | Vanilla JavaScript |
| Audio | Web Audio API (procedural chiptune) |
| Styling | CSS custom properties + animations |
| Database | Supabase (PostgreSQL) |
| Hosting | Netlify |
| Font | Press Start 2P (Google Fonts) |

No frameworks. No build step. One file.

---

## What I Learned

- How to direct AI tools effectively as a non-developer:
  giving clear context, validating output, and pushing back when needed
- How Monte Carlo simulation applies to game balancing
- How player feedback translates into concrete technical fixes
- The difference between a feature that works and a feature that 
  feels right — and how iteration bridges that gap

---

## About

Built by **Mauro Soprana** — transitioning into tech from 10+ years in 
sales, hospitality and team leadership.

Currently studying Systems Analysis, focused on Python, Data Engineering, and AI applications.

[LinkedIn](https://linkedin.com/in/msoprana-python) · 
[GitHub](https://github.com/maurosopranadev) · 
soprana.dev@gmail.com
