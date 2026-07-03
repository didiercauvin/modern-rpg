# 005 - Game Model

## Purpose

This document defines the fundamental concepts used by the engine.

It establishes the separation between:

- the runtime,
- the game mechanics,
- the game content,
- the running game.

Every other architectural document depends on these concepts.

---

# Overview

```
                         Engine
                            │
                     executes
                            │
                            ▼
                       Ruleset
                            │
                  defines mechanics
                            │
                            ▼
                        Setting
                            │
                  provides the universe
                            │
                            ▼
                       Adventure
                            │
                   defines the story
                            │
                            ▼
                         Session
                            │
                    contains players
                            │
                            ▼
                      World State
```

---

# Engine

The Engine is the runtime.

Its responsibility is to execute a game.

The Engine provides generic services such as:

- command execution
- event dispatching
- persistence
- scheduling
- AI orchestration
- session lifecycle
- save/load
- multiplayer support

The Engine contains no gameplay rules.

It knows nothing about fantasy, horror or science-fiction.

---

# Ruleset

A Ruleset defines **how the game is played**.

Examples:

- Dungeons & Dragons
- Call of Cthulhu
- Pathfinder
- Cyberpunk RED

A Ruleset defines:

- character creation
- attributes
- skills
- combat
- inventory rules
- progression
- dice mechanics
- conditions
- death
- reputation
- sanity
- magic

A Ruleset contains no story and no world.

It only defines mechanics.

---

# Setting

A Setting defines **where the story takes place**.

Examples:

- Forgotten Realms
- Ravenloft
- Arkham
- Night City
- Middle Earth

A Setting contains:

- geography
- locations
- factions
- creatures
- NPC templates
- items
- cultures
- religions
- languages
- history
- lore

A Setting contains no player progression.

A Setting contains no running game state.

It is immutable.

---

# Adventure

An Adventure defines **what happens inside a Setting**.

Examples:

- Lost Mine of Phandelver
- Curse of Strahd
- The Haunting

An Adventure references exactly one Setting.

It contains:

- introduction
- objectives
- quests
- scripted events
- important NPCs
- encounters
- triggers
- endings
- optional branches

An Adventure is also immutable.

---

# Session

A Session is a running instance of an Adventure.

It contains every mutable element.

Examples:

- player characters
- inventory
- completed quests
- current location
- elapsed time
- discovered locations
- dead NPCs
- opened doors
- destroyed bridges

Multiple Sessions may exist for the same Adventure.

---

# Character

Characters belong to a Session.

Their structure is defined by the Ruleset.

Their initial values may depend on the Adventure.

---

# World State

The World State is the current state of the Setting during a Session.

The Setting provides the initial world.

The Session records every modification.

---

# Artificial Intelligence

Artificial Intelligence is never authoritative.

It may:

- interpret player intent
- narrate events
- generate dialogue
- summarize sessions
- adapt descriptions

It never modifies the World State directly.

---

# Example

```
Engine

└── Ruleset
      │
      └── Dungeons & Dragons
             │
             ├── Forgotten Realms
             │        │
             │        ├── Lost Mine of Phandelver
             │        ├── Icewind Dale
             │        └── Homebrew Adventure
             │
             └── Ravenloft
                      │
                      └── Curse of Strahd


└── Ruleset
      │
      └── Call of Cthulhu
             │
             └── Arkham
                      │
                      ├── The Haunting
                      └── Masks of Nyarlathotep
```

---

# Design Principles

The architecture follows four principles.

## Separation of concerns

Mechanics are separated from content.

## Immutable definitions

Rulesets, Settings and Adventures are immutable.

Only Sessions evolve.

## Reusability

A Ruleset may support many Settings.

A Setting may support many Adventures.

An Adventure may support many Sessions.

## Engine independence

The Engine depends on none of the above.

Everything is loaded through extension points.

---

# Guiding Principle

The Engine answers:

> How should this game execute?

The Ruleset answers:

> How is this game played?

The Setting answers:

> Where does this story happen?

The Adventure answers:

> What story will be experienced?

The Session answers:

> What has happened so far?