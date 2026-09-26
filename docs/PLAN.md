# MarioBlueprints — Plan & Design

> An idea machine that helps kids dream up fun Super Mario Maker 2 levels.
> Spin → get a level idea → learn the trick → go build it.

## Decisions (round 2)

| Topic | Decision |
|---|---|
| Ages | 7–10 |
| Language | English |
| Who can use it | Our family only. Private, no public sign-ups |
| Icons | No emojis. We draw our own SVG icons (no Nintendo sprites) |
| Creativity | The site gives **sparks, not plans**. Kids pick how much help they want (Tiny spark, Spark, Big spark). Everything else is labeled "You choose!", and instead of steps they get open questions like "Where does the big surprise go?" |
| Music | A whole section on Music Blocks: how they work, a song helper with a block-by-block map, and a tune maker kids can play and hear |
| Accounts / database | Not needed. Saved ideas stay on the device. **No Supabase** for now |
| Hosting | **Vercel** (free Hobby plan), protected with a family password. GitHub Pages would need a public repo on the free plan, so the site would be public |

Clickable mockup: `mockup/index.html`

> Everything below is round 1. Where it disagrees with the table above, the table wins.

---

## 1. Who it's for

| | |
|---|---|
| **Main users** | Kids aged about 6–12 who play Super Mario Maker 2 |
| **Also** | Parents, siblings, teachers running "make a level" activities |
| **Reading level** | Short words, one idea per line, every word paired with a picture |
| **Devices** | Tablet first (kids often sit next to the Switch with a tablet), then phone, then desktop |

**Design rules for kids**
1. **Pictures before words.** Every part, theme and goal has an icon or colour.
2. **One big button does the magic.** The main action is always the giant "Spin!" button.
3. **No typing needed.** Everything works by tapping.
4. **Read-aloud button** on every card (browser speech, no audio files needed).
5. **Nothing scary.** No accounts, no chat, no ads, no personal data collected (keeps us clear of COPPA-type rules).
6. **Big tap targets** (at least 48px), high contrast, works without sound.
7. **Celebrate.** Confetti / a star sound when you lock in an idea or finish a checklist.

---

## 2. What we learned from the Mario Maker community

**The game's building blocks (what we can combine)**
- 5 game styles: Super Mario Bros., SMB3, Super Mario World, New Super Mario Bros. U, Super Mario 3D World.
- 10 course themes: Ground, Underground, Underwater, Ghost House, Castle, Airship, Forest, Sky, Desert, Snow. Each has a Day and a Night version (not in 3D World). Night changes how some things work, like poisonous water or low gravity.
- About 119 separate parts in four groups: Terrain, Items, Enemies, Gizmos.
- Clear conditions in three kinds: *Parts* (collect or defeat X), *Status* (finish as Fire Mario), and *Action* (don't jump, don't touch the ground…).
- Level tags like Standard, Puzzle, Speedrun, Auto-scroll, Multiplayer Versus, Themed, Music, Art, Boss battle, Shooter, Link.

**Design wisdom creators keep repeating**
- **Pick one main gimmick** and build the whole level around it. For example, an airship level built around Bill Blasters and cannons.
- **Nintendo's 4-step recipe (kishōtenketsu):** introduce a mechanic safely, develop it, twist it, then finish with a final test. For kids we call it **Meet it → Practice it → Twist it → Boss it!**
- Teach new things **where falling doesn't kill you**.
- Put **checkpoints between each part** of the level.
- Use **coin trails and arrow signs** to show the way.
- Don't use hidden-block traps or blind jumps, because they aren't fair for other players ("troll" levels).
- **Play your level from the start** before uploading, including a no-power-up run.
- Castle and airship themes suit boss-fight endings.

**Tools that already exist (and what's missing)**
| Tool | What it does | Gap for kids |
|---|---|---|
| Random Acts of Mario idea generator | Randomizes level concepts | Text-heavy, built for adult creators |
| SMM2 Concept Generator (Siraj Chokshi) | Randomizes style/theme/concept | Plain lists, no teaching |
| GOOP.WTF slot machine | Slot-machine style ideas | Fun, but just an idea, with no "how to build it" |
| 12 Item Challenge Generator | Picks 12 parts to use | Challenge only, no guidance |

**Our twist:** none of these tools are made for kids, and none of them teach. MarioBlueprints gives you an idea **plus** a picture-based build plan, tips and a checklist.

---

## 3. The idea engine (thousands of combinations)

Each idea card is built from **slots**. Kids can spin all of them or lock the ones they like and re-spin the rest, like a slot machine.

| Slot | Example values | Count (v1 target) |
|---|---|---|
| 🎮 Game Style | SMB, SMB3, SMW, NSMBU, 3D World | 5 |
| 🌍 World (theme) | Ground, Sky, Snow, Ghost House… | 10 |
| 🌗 Time | Day / Night | 2 |
| ⭐ Star Part (main gimmick) | Springs, P-Switch, Clown Car, Vines, Tracks, Ice, Conveyor belts, Pipes, Yoshi, Shoe Goomba… | 40 |
| 🌀 Twist | "Everything is upside down", "Only moving platforms", "Chased by Lava", "Enemies are your friends"… | 30 |
| 🏁 Goal | Normal flag, 50 coins, beat 5 Goombas, don't jump, finish as Cat Mario… | 25 |
| 📖 Story Hook | "Save the lost Toad", "Escape the haunted bakery", "Race the Koopa to the top"… | 30 |
| 🎚 Difficulty | Easy-peasy / Medium / Super hard | 3 |

5 × 10 × 2 × 40 × 30 × 25 × 30 = **27,000,000** combos before difficulty. We'll add **compatibility rules** so every idea actually works in the game (e.g. no Night in 3D World, 3D World-only parts only with 3D World, no Yoshi in SMB/SMB3), so every card can really be built.

**Silly title generator:** `[Adjective] + [Star Part] + [Place]` gives titles like *"The Wobbly Spring Palace"* or *"Grumpy Goomba Airport"*. Kids love naming their level.

**Other modes (later)**
- **Daily Idea:** everyone gets the same idea today (seeded by date). Good for classrooms and friends.
- **Challenge Mode:** "Build a level using only these 5 parts."
- **Share code:** each idea has a short URL (`/idea/7Q3K9`) so kids can send it to a friend. No accounts needed.

---

## 4. Site map

```
Home (big Spin button)
├── 🎰 Idea Machine        — spin / lock slots / silly title / read-aloud
│    └── Idea Card         — the idea + "How to build it" 4-step plan + checklist
├── 🧱 Parts Picture Book  — every part with icon, "what it does", 1 kid tip, idea links
├── 💡 Tips & Tricks       — short illustrated cards ("Coin trails show the way!")
├── 🧩 Mini Challenges     — "5-part challenge", "No-jump level", "Music level"
├── 📓 My Blueprints       — saved ideas (stored on this device only)
└── 👪 For Grown-ups       — what this is, safety, classroom ideas, fan disclaimer
```

### Key screen: Idea Machine (wireframe)

```
┌─────────────────────────────────────────┐
│  MarioBlueprints              🔊  📓     │
├─────────────────────────────────────────┤
│   [🎮 3D World] [☁️ Sky] [🌙 Night] 🔒   │
│   [⭐ Clown Car] [🌀 Upside down]        │
│   [🏁 Collect 30 coins] [📖 Save Toad]   │
│                                         │
│      "The Wobbly Clown-Car Cloudland"   │
│                                         │
│          ┌───────────────────┐          │
│          │    🎰  SPIN!      │          │
│          └───────────────────┘          │
│   [ 💾 Save ]  [ 🔨 How to build it ]    │
└─────────────────────────────────────────┘
```

### Idea Card → "How to build it"
1. **Meet it:** "Put a Clown Car at the start on safe ground."
2. **Practice it:** "Make a path of coins in the sky to follow."
3. **Twist it:** "Now add wind or enemies that block the way."
4. **Boss it:** "Big finish! Fly past a Bowser Jr. to the flag."
- ✅ Checklist: *Checkpoint added? Played from the start? Can a friend beat it?*
- 💡 2 matching tips from the Tips library.

---

## 5. Content data model (JSON, easy to grow)

```jsonc
// data/parts.json
{ "id": "spring", "name": "Trampoline", "group": "gizmo",
  "styles": ["smb","smb3","smw","nsmbu","3dw"],
  "kidSays": "Boing! Jump super high.",
  "tip": "Hold jump while you land for an extra-big bounce.",
  "icon": "spring.svg" }

// data/twists.json
{ "id": "upside-down", "text": "Everything is upside down!",
  "worksWith": ["*"], "notWith": ["underwater"] }

// data/tips.json
{ "id": "coin-trail", "title": "Coin trails show the way",
  "body": "Put coins where you want players to jump.", "tags": ["beginner"] }
```

Adding content is just editing JSON, so parents, kids or contributors can add new twists without touching code.

---

## 6. Tech plan

| Choice | Why |
|---|---|
| **Vite + React + TypeScript** | Fast, simple, lots of help online |
| **Static site, no backend** | Free, fast, safe, no data about kids |
| **Tailwind CSS** | Quick, chunky, colourful UI |
| **localStorage** for "My Blueprints" | Saved ideas stay on the device |
| **Web Speech API** for read-aloud | Built into browsers, free |
| **Seeded random** (e.g. mulberry32) | Share codes + Daily Idea |
| **PWA** | Install on a tablet and use offline |
| **Deploy on Vercel** (connected already) or GitHub Pages | One-click deploys from this repo |

**Legal / IP:** this is an unofficial fan site. We **won't use Nintendo sprites, logos or music**. We'll draw our own simple icons or use emoji, and add a clear "not affiliated with Nintendo" note.

---

## 7. Build phases

| Phase | Deliverable |
|---|---|
| **0. Plan** ✅ | This document |
| **1. Clickable mockup** | One HTML page with the Idea Machine look and feel to test with a real kid |
| **2. MVP** | Idea Machine + Idea Card + build steps + read-aloud + ~150 content entries |
| **3. Library** | Parts Picture Book + Tips & Tricks pages |
| **4. Save & Share** | My Blueprints, share codes, Daily Idea |
| **5. Polish** | Sounds, confetti, PWA/offline, accessibility pass, For Grown-ups page |
| **6. Launch** | Deploy, test on a tablet with kids, iterate |

**Success check:** a 7-year-old can get an idea they like and know what to build first **in under 30 seconds, without help.**

---

## 8. Open questions for the owner
1. Age range: closer to 6–8 (almost no text) or 9–12 (more tips)?
2. Languages: English only, or also Arabic or others (with right-to-left layout)?
3. Hosting: Vercel or GitHub Pages?
4. Should kids be able to submit their own ideas later? (That needs moderation, so it's not in v1.)

---

### Sources
- [Super Mario Maker 2 Wiki: Course Themes](https://supermariomaker2.fandom.com/wiki/Course_Themes), [Course Parts](https://supermariomaker2.fandom.com/wiki/Course_Parts), [Game Styles](https://supermariomaker2.fandom.com/wiki/Game_Styles), [Clear Conditions](https://supermariomaker2.fandom.com/wiki/Clear_Conditions)
- [Kaizo Mario Maker Wiki: List of Course Elements](https://kaizomariomaker.fandom.com/wiki/SMM2:List_of_Course_Elements)
- [Nintendo Life: Course building tips](https://www.nintendolife.com/guides/super-mario-maker-2-course-building-tips-check-out-these-classic-levels-for-inspiration)
- [Tom's Guide: Build levels like a pro](https://tomsguide.com/how-to/super-mario-maker-2-tips-how-to-build-levels-like-a-pro)
- [TechRadar: Making a Mario Maker level that's actually fun](https://www.techradar.com/how-to/how-to-make-a-super-mario-maker-level-thats-actually-fun)
- [Kishōtenketsu in level design (MCV/Develop)](https://mcvuk.com/business-news/publishing/video-nintendos-level-design-secrets-in-four-steps/)
- Existing generators: [Random Acts of Mario](https://randomactsofmario.com/idea-generator), [SMM2 Concept Generator](https://github.com/SirajChokshi/SMM2-Concept-Generator), [GOOP.WTF](https://goop.wtf/mario-ideas/), [12 Item Challenge](https://www.timetler.com/mario-maker/)
