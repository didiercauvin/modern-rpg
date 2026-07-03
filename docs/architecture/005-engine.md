# 005 - Engine Architecture

## Purpose

The goal of this document is to define the architectural boundaries of the engine.

It describes:

- what belongs to the engine;
- what belongs to a ruleset;
- what belongs to a game module;
- what belongs to a game session.

The engine is designed as a runtime capable of executing narrative role-playing games regardless of their universe or gameplay mechanics.

---

# Core Principle

The engine executes games.

It does not define them.

Everything specific to a game is provided through extensions.

---

# High-Level Architecture

```text
                           Engine
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
   Runtime Services     Extension Points      AI Integration
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
                Ruleset            Game Module
                    │
                    ▼
              Game Session
```

---

# Engine Responsibilities

The Engine provides generic services that are independent of any game universe.

Responsibilities include:

- command execution
- event dispatching
- state persistence
- save/load
- session lifecycle
- player management
- AI orchestration
- scheduling
- randomness
- logging
- extensibility

The Engine never contains gameplay rules.

---

# Runtime Services

Runtime Services are built into the engine.

Examples:

- Command Pipeline
- Event Pipeline
- Session Manager
- Persistence
- Time Scheduler
- Random Number Generator
- AI Gateway

These services are reusable by every Ruleset.

---

# Extension Points

The engine exposes extension points.

An extension point defines **what the engine needs**.

It never defines **how it works**.

Examples:

```text
ICombatSystem

ICharacterSystem

ISkillSystem

IInventorySystem

IQuestSystem

IDialogueSystem

IMagicSystem

IDeathSystem

ITimeSystem
```

The engine communicates only with these abstractions.

---

# Ruleset

A Ruleset provides implementations for the extension points.

It defines how a game works.

Examples:

```text
Dungeons & Dragons

Call of Cthulhu

Cyberpunk RED

Pathfinder

Custom Rules
```

A Ruleset may implement:

```text
ICombatSystem

↓

DnDCombatSystem
```

or

```text
ICombatSystem

↓

CallOfCthulhuCombatSystem
```

or

```text
ICombatSystem

↓

CyberpunkCombatSystem
```

The Engine does not know which implementation is being used.

---

# Ruleset Responsibilities

A Ruleset defines:

- character creation
- attributes
- skills
- combat
- progression
- inventory rules
- experience
- conditions
- status effects
- death
- dice mechanics
- magic
- sanity
- reputation

The Ruleset contains no story.

---

# Game Module

A Module provides playable content.

It contains:

- locations
- NPCs
- creatures
- quests
- factions
- dialogues
- lore
- items
- world layout
- AI prompts
- campaign configuration

A Module contains no mutable state.

It is a template.

---

# Game Session

A Game Session is a running instance of a Module.

It stores every mutable piece of information.

Examples:

- player positions
- opened doors
- dead NPCs
- inventory
- completed quests
- elapsed time
- discovered locations

A Module may have any number of Game Sessions.

---

# Artificial Intelligence

Artificial Intelligence is never authoritative.

It is responsible for:

- natural language interpretation
- narration
- dialogue generation
- summaries
- flavour text

The Engine remains the single source of truth.

---

# Request Flow

```
Player

↓

Natural Language

↓

LLM

↓

Structured Command

↓

Engine

↓

Extension Point

↓

Ruleset Implementation

↓

Domain Events

↓

Updated World State

↓

Narration AI

↓

Player
```

---

# Dependency Rules

The architecture follows strict dependency rules.

```
Engine
    ▲
    │
Ruleset
    ▲
    │
Module
    ▲
    │
Session
```

Meaning:

- the Engine never depends on a Ruleset;
- a Ruleset never depends on a Module;
- a Module never depends on a Session.

Each layer depends only on the one below it.

---

# Design Goals

The architecture should allow developers to:

- create new Rulesets;
- create new Modules;
- create new AI personalities;
- create new worlds;
- reuse existing Rulesets across multiple Modules.

Without modifying the Engine.

---

# Example

```
Engine

└── Ruleset
        │
        ├── D&D 5e
        │      ├── Lost Mine
        │      ├── Curse of Strahd
        │      └── Homebrew Campaign
        │
        ├── Call of Cthulhu
        │      ├── The Haunting
        │      └── Masks of Nyarlathotep
        │
        └── Cyberpunk RED
               ├── Night City Stories
               └── Corporate War
```

The Engine is identical in every case.

Only the Ruleset and the Module change.

---

# Guiding Principle

The project separates four independent concerns.

- The Engine executes.
- The Ruleset defines the mechanics.
- The Module defines the world.
- The Session records the history.

Artificial Intelligence enhances the experience but never owns the game state.