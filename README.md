# Possible Modes and Args for JoinRoom Remote

This file lists all possible modes and their valid arguments for the JoinRoom remote in the game.
Use this to configure the NAS.json file for the auto-execute script.
Format for args: [world, act, hard, friends]
- world: Numeric index or identifier for the world (see below for mappings).
- act: Act number (integer).
- hard: Difficulty level (1 = Normal, 2 = Hard, 3 = Nightmare).
- friends: Boolean (true = friends-only room, false = public room).

## Modes
The JoinRoom remote is called with: FireServer(method, type, world, act, hard, friends)
- method: "Create" or "TeleGameplay"
- type: Mode type (Story, Raid, Siege, Inf, Challenge)

### Create Mode
- method: "Create"
- type: Story, Raid, Siege, Inf, Challenge
- args: [world, act, hard, friends]

#### Story
- Description: Story mode levels across various worlds.
- World Values:
  - 1: World1 (Leaf Village, Level 0, Acts: Kimimaru, Mamba, Mamba, Gaaro Half Beast, One Tailed Beast)
  - 2: World2 (Marine Island, Level 0, Acts: Smoke Boss, Light Boss, Ice Boss, Magma Boss, Gold Buddha)
  - 3: World3 (Red Light District, Level 0, Acts: Ball & Arrow Demon, Lower Moon Five, Lower Moon One, Daky (Obi Demon), Upper Moons Six)
  - 4: World4 (West City, Level 0, Acts: Raku, Friezo First Form, Friezo Final Form, Cel (Perfect), Super Mabu)
  - 5: World5 (Firefighting City, Level 0, Acts: Fighter Infernal, Power Infernal, Scythe Infernal, Ember, Dragon)
  - 6: World6 (Jujutsu High, Level 0, Acts: Possessed Curse User F, Possessed Curse User B, Possessed Curse User A, Yoota, Heto)
  - 7: World7 (Demon Village, Level 0, Acts: Hekido, Rizetsu, Orogi, Sohakuten, Akaz)
- Act: 1 to 5 (each world has 5 acts)
- Hard: 1 (Normal), 2 (Hard, requires HardBadgeId), 3 (Nightmare, requires NightmareBadgeId)
- Friends: true, false
- Notes: Higher acts and difficulties may require unlocking via story progress or badges.

#### Raid
- Description: Raid mode levels in specific raid worlds.
- World Values:
  - 1: WorldRaid1 (Foggy Night Mansion, Level 20)
  - 2: WorldRaid2 (Dark Fortress, Level 25)
  - 3: WorldRaid3 (Green Rampage, Level 30)
- Act: 1 to 5
- Hard: 1 (Normal), 2 (Hard, requires HardBadgeId), 3 (Nightmare, requires NightmareBadgeId)
- Friends: true, false
- Notes: Higher world numbers require higher player levels (20, 25, 30).

#### Siege
- Description: Siege mode in a single world.
- World Values:
  - 1: WorldSiege1 (Mugen Siege, Level 15)
- Act: 1 to 5
- Hard: 1 (Normal), 2 (Hard, requires HardBadgeId), 3 (Nightmare, requires NightmareBadgeId)
- Friends: true, false
- Notes: Requires player level 15+.

#### Inf (Infinite Mode)
- Description: Boss Rush Dungeon in infinite mode.
- World Values:
  - 1: WorldInf1 (Boss Rush Dungeon, Level 15)
- Act: 1 to 5
- Hard: 1 (Normal), 2 (Hard, requires HardBadgeId), 3 (Nightmare, requires NightmareBadgeId)
- Friends: true, false
- Notes: Requires player level 15+.

#### Challenge
- Description: Challenge mode with time-based availability.
- World Values:
  - 1: Challenge_1 (Hope Against Titans, Level 0)
- Act: 1 (likely fixed, no evidence of multiple acts)
- Hard: 1 (Normal), 2 (Hard), 3 (Nightmare)
- Friends: true, false
- Notes: Only available when workspace.ChallengeOpen.Value is true. Check LeftTimeOpen/LeftTimeClose attributes.

### TeleGameplay Mode
- method: "TeleGameplay"
- type: Challenge (other types like Raid, Story, Siege, Inf may be possible but unconfirmed)
- args: [world, act, hard, friends]
- World Values:
  - For type "Challenge":
    - 1: Challenge_1 (Hope Against Titans, Level 0)
  - For type "Raid" (example, may need testing):
    - 1: WorldRaid1 (Foggy Night Mansion, Level 20)
    - 2: WorldRaid2 (Dark Fortress, Level 25)
    - 3: WorldRaid3 (Green Rampage, Level 30)
- Act: 1 (for Challenge), 1 to 5 (for Raid, if valid)
- Hard: 1 (Normal), 2 (Hard), 3 (Nightmare)
- Friends: true, false
- Notes: TeleGameplay for non-Challenge types needs testing. Challenge mode requires workspace.ChallengeOpen.Value to be true.

### Example JSON Configuration
{
  "Create": {
    "event": "JoinRoom",
    "method": "Create",
    "type": "Raid",
    "args": [2, 2, 1, false] // WorldRaid2, Act 2, Normal, Public
  },
  "TeleGameplay": {
    "event": "JoinRoom",
    "method": "TeleGameplay",
    "type": "Challenge",
    "args": [1, 1, 1, false] // Challenge_1, Act 1, Normal, Public
  }
}

### Notes
- Level Requirements: Check WorldData for minimum levels (e.g., WorldRaid3 requires Level 30).
- Unlocks: Higher acts and difficulties may require story progress or badges (HardBadgeId, NightmareBadgeId).
- Challenge Mode: Gated by workspace.ChallengeOpen.Value; check LeftTimeOpen/LeftTimeClose.
- Testing: Some TeleGameplay types (e.g., Story, Siege) may work but aren't confirmed in provided scripts.
