# About Us:
We are a team consisting of 3 developers to make games. We actually made this game because we got an assignment from our teacher to make a game for one month, after one month of work we finally succeeded in making a game called Box Siege, a simple game made with Unity and C#, this game can be downloaded via our website. you can try it now

<div align="center">

---

# Box Siege

**A Round-Based Local Multiplayer 2D Fighting Game**

[![Unity](https://img.shields.io/badge/Engine-Unity-000000?style=for-the-badge&logo=unity&logoColor=white)](https://unity.com)
[![C#](https://img.shields.io/badge/Language-C%23-239120?style=for-the-badge&logo=csharp&logoColor=white)](https://learn.microsoft.com/en-us/dotnet/csharp/)
[![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)](https://boxsiege.vercel.app)
[![Players](https://img.shields.io/badge/Players-2--4%20Local-FF6B35?style=for-the-badge)](https://boxsiege.vercel.app/#characters)
[![Status](https://img.shields.io/badge/Status-Beta-brightgreen?style=for-the-badge)](https://boxsiege.vercel.app)
[![Download](https://img.shields.io/badge/Download-Available-blue?style=for-the-badge)](https://boxsiege.vercel.app/#download)

[Website](https://equinoxinteractive.vercel.app) • [Download Game](https://boxsiege.vercel.app/#download) • [Our Team](#our-team)

---

## About Box Siege

**Box Siege** is a local multiplayer 2D fighting game built with Unity and C#, developed in one month as a school assignment by a team of three. Players compete head-to-head across multiple maps, choosing from a roster of 16 characters and fighting through a structured round system — complete with power-ups, rebindable controls, and a Sudden Death tiebreaker when rounds are too close to call.

### What's Inside

- **16 Playable Characters** — Each with a unique alive and death sprite, assigned per player slot
- **Round-Based Win System** — First to 3 round wins takes the match, scaled by player count
- **Sudden Death Mode** — Triggered automatically when players are tied at the final threshold
- **4 Power-Up Types** — Collectible mid-match items that shift the momentum
- **Fully Rebindable Controls** — Keyboard and gamepad support via Unity Input System
- **Graphics Settings** — Resolution and fullscreen toggle with persistent PlayerPrefs storage
- **Map Selection** — Browse and preview maps before launching into a match

---

## Quick Download

Head to the game website to download and play:

```
https://boxsiege.vercel.app/#download
```

No installation required — download, extract, and run.

---

## Game Info

| Property | Details |
|---|---|
| Genre | 2D Local Multiplayer Fighting |
| Engine | Unity |
| Language | C# |
| Players | 2 – 4 (same machine) |
| Platform | Windows |
| Development Time | 1 month |
| Team Size | 3 developers |
| Characters | 16 playable characters |
| Input | Keyboard & Gamepad (fully rebindable) |

---

## Round System

```
┌─────────────────────────────────────────────────────────────────┐
│                     BOX SIEGE — ROUND RULES                     │
├──────────────────────┬──────────────────────────────────────────┤
│  Win Condition       │  First player to win 3 rounds            │
│  2 Players           │  Max 5 rounds                            │
│  3 Players           │  Max 7 rounds                            │
│  4 Players           │  Max 9 rounds                            │
├──────────────────────┴──────────────────────────────────────────┤
│                      SUDDEN DEATH TRIGGER                       │
│                                                                 │
│  Activates when the timer expires and 2 or more players are     │
│  tied at exactly 2 wins with the same HP value.                 │
│                                                                 │
│  Rules during Sudden Death:                                     │
│    • Only tied players participate (knife combat only)          │
│    • Eliminated players: frozen, HP set to 0                    │
│    • Tied players HP reset to 3                                 │
│    • Power-ups do not spawn                                     │
│    • Timer is disabled (infinite)                               │
│    • Winner of Sudden Death = winner of the game                │
└─────────────────────────────────────────────────────────────────┘
```

---

## Power-Up System

Four power-up types spawn randomly during a match. Dead or eliminated players cannot pick them up, and they are disabled entirely during Sudden Death.

```csharp
public enum PowerUpType
{
    Health,     // Restores 1 HP to the collecting player
    Shield,     // Absorbs the next 2 hits of incoming damage
    JumpBoost,  // 1.5x jump height for 10 seconds
    SpeedBoost  // 1.5x movement speed for 10 seconds
}
```

---

## Character Roster

16 characters total, distributed across four player slots:

| Player Slot | Available Characters |
|---|---|
| Player 1 | Angry, Bandel, Melow, Ninja |
| Player 2 | Calm, Baik, Mime, Silat |
| Player 3 | Blind, Drunk, Joker, Spiderweaver |
| Player 4 | Bald-man, Deadswim, Savior, Spiderblack |

Each character has two sprites: one for alive state and one for death state, defined as a ScriptableObject:

```csharp
[CreateAssetMenu(fileName = "NewCharacterData", menuName = "Character/CharacterData")]
public class CharacterData : ScriptableObject
{
    public Sprite aliveSprite;   // Displayed while the character is alive
    public Sprite deathSprite;   // Displayed on elimination
    public string characterName; // Used in selection UI
}
```

---

## Features

| Feature | Description |
|---|---|
| Character Selection | 16 characters across 4 player slots with per-slot sprite sets |
| Map Selection | Preview and select maps before the match begins |
| Round System | Win-tracking with round box indicators per player |
| Sudden Death | Automatic tiebreaker — knife only, infinite timer, HP reset |
| Power-Ups | 4 types with mid-match random spawning via `PowerUpManager` |
| Graphics Settings | Resolution dropdown and fullscreen toggle, saved via `PlayerPrefs` |
| Rebindable Controls | Full keyboard and gamepad remapping with icon display (PS & Xbox) |
| Audio System | Per-event SFX for rounds, power-ups, and actions via `AudioManager` |
| Pause Menu | In-game pause with continue and main menu options |
| Multi-Player Scaling | UI, health, ammo, and power-up panels auto-show/hide based on active player count |

---

## Project Structure

```
BoxSiege/
├── Karakter/
│   ├── CharacterData.cs          # ScriptableObject: alive/death sprite + name
│   ├── CharacterSelection.cs     # Selection screen logic
│   ├── GameData.cs               # Singleton: carries player count across scenes
│   └── P1–P4 Sprite/             # Sprite assets per player slot
│
├── Pause Script/
│   ├── GameManger.cs             # Core: round logic, Sudden Death, win detection
│   └── PauseOption.cs            # Pause menu — continue, main menu, timescale
│
├── PowerUp/
│   ├── PowerUp.cs                # Trigger logic and effect dispatch per type
│   ├── PowerUpManager.cs         # Spawn timing and control
│   ├── PowerUpTimerUI.cs         # Active effect countdown display
│   └── PlayerPowerUpEffects.cs   # Applies shield, speed, jump effects to players
│
├── Health/                       # Health + healthbar components for P1–P4
│   ├── Health.cs / Healthbar.cs
│   ├── HealthP2.cs / HealthbarP2.cs
│   ├── HealthP3.cs / HealthbarP3.cs
│   └── HealthP4.cs / HealthbarP4.cs
│
├── Scripts/Rebinding UI/
│   ├── RebindActionUI.cs         # Input rebinding with keyboard and gamepad icons
│   ├── ControllerAssignmentManager.cs
│   └── GamepadIconsDataXbox.cs   # Xbox button icon set
│
├── Maps/
│   └── MapSelector.cs            # Browse maps, update preview, load selected scene
│
├── Resolution Setting/
│   ├── GraphicsSettings.cs       # Resolution list, fullscreen toggle, PlayerPrefs save
│   └── SettingsUI.cs
│
├── Guns/                         # Weapon and shooting scripts
├── Timer/                        # Round timer
├── Round/                        # Round UI assets and images
└── Main Menu/
    └── Main Menu.cs
```

---

## Game Preview:
  <img src="profile/Foto/GamePreview/Lobby.png" height="150">
  <img src="profile/Foto/GamePreview/Select.png" height="150">
  <img src="profile/Foto/GamePreview/Selection.png" height="150">
  <img src="profile/Foto/GamePreview/InGame.png" height="150">
  <img src="profile/Foto/GamePreview/Rebind.png" height="150">

---

### Our Website:

<a href="https://equinoxinteractive.vercel.app">
  <img src="profile/Foto/WebsitePreveiw/EIWeb.png" height="200">
</a>

### Our Game Website:

<a href="https://boxsiege.vercel.app">
  <img src="profile/Foto/WebsitePreveiw/BSWeb.png" height="200">
</a>

---

## Socials:
[![Instagram](https://img.shields.io/static/v1?message=Instagram&logo=instagram&label=&color=E4405F&logoColor=white&labelColor=&style=for-the-badge)](https://instagram.com/equinox.interactive) [![Tiktok](https://img.shields.io/badge/TikTok-000000?style=for-the-badge&logo=tiktok&logoColor=white)](https://tiktok.com/@equinox.interactive) [![X](https://img.shields.io/badge/X-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/@EquinoxIntratve)

## Our Team:

<a href="https://badutzy.vercel.app">
  <img src="profile/Foto/Team/BadutZY.jpg" height="100">
</a>

BadutZY:

[![Instagram](https://img.shields.io/static/v1?message=Instagram&logo=instagram&label=&color=E4405F&logoColor=white&labelColor=&style=for-the-badge)](https://instagram.com/rzky.mp_36/)
[![X](https://img.shields.io/badge/X-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/BadutZYY_)
[![Youtube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtube.com/@badutzy)
[![Github](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/BadutZY)

[![Modrinth](https://img.shields.io/badge/Modrinth-logo?style=for-the-badge&logo=modrinth&logoColor=white)](https://modrinth.com/user/BadutZY)
[![Curseforge](https://img.shields.io/badge/curseforge-F16436?style=for-the-badge&logo=curseforge&logoColor=white)](https://www.curseforge.com/members/badutzy/)

<br>

<a href="https://ariaja.pages.dev/">
  <img src="profile/Foto/Team/Ari.jpg" height="100">
</a>

Ari8Bit:

[![Instagram](https://img.shields.io/static/v1?message=Instagram&logo=instagram&label=&color=E4405F&logoColor=white&labelColor=&style=for-the-badge)](https://www.instagram.com/gamersindo_17/)
[![Youtube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@AriAja17)
[![Youtube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@GamersIndo17)
[![Tiktok](https://img.shields.io/badge/TikTok-000000?style=for-the-badge&logo=tiktok&logoColor=white)](https://www.tiktok.com/@gamersindo.17)
[![Github](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/AriAja17)

[![Modrinth](https://img.shields.io/badge/Modrinth-logo?style=for-the-badge&logo=modrinth&logoColor=white)](https://modrinth.com/user/AriAja17)
[![Curseforge](https://img.shields.io/badge/curseforge-F16436?style=for-the-badge&logo=curseforge&logoColor=white)](https://www.curseforge.com/members/ariaja17)

<br>

<a href="#">
  <img src="profile/Foto/Team/SwimmingFOX.jpg" height="100">
</a>

SwimmingFox:

[![Instagram](https://img.shields.io/static/v1?message=Instagram&logo=instagram&label=&color=E4405F&logoColor=white&labelColor=&style=for-the-badge)](https://www.instagram.com/swimmingfoxx_/)
[![Github](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Marrwertz)

# Tech Stack:
![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=csharp&logoColor=white) ![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white) ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white) ![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Vercel](https://img.shields.io/badge/vercel-%23000000.svg?style=for-the-badge&logo=vercel&logoColor=white) ![NPM](https://img.shields.io/badge/NPM-%23CB3837.svg?style=for-the-badge&logo=npm&logoColor=white) ![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB) ![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white) ![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white) ![Adobe Photoshop](https://img.shields.io/badge/adobe%20photoshop-%2331A8FF.svg?style=for-the-badge&logo=adobe%20photoshop&logoColor=white) ![Adobe Premiere Pro](https://img.shields.io/badge/Adobe%20Premiere%20Pro-9999FF.svg?style=for-the-badge&logo=Adobe%20Premiere%20Pro&logoColor=white) ![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white) ![Unity](https://img.shields.io/badge/unity-%23000000.svg?style=for-the-badge&logo=unity&logoColor=white) ![Godot](https://img.shields.io/badge/Godot-478CBF?style=for-the-badge&logo=GodotEngine&logoColor=white)

<br>

*Made with dedication by Equinox Interactive — built in one month, designed to last.*

[⬆ Back to Top](#box-siege)

</div>