# RPG Engine

> A deterministic RPG engine designed for AI-assisted storytelling.

## Vision

The goal of this project is to build a deterministic RPG engine capable of powering text-based role-playing games where artificial intelligence enhances immersion without ever controlling the game world.

The engine is responsible for every gameplay rule.

Artificial intelligence is responsible for understanding natural language and generating narrative.

This separation guarantees that every game remains coherent, testable and reproducible.

---

# Philosophy

The engine follows a few fundamental principles.

## Gameplay first

Every architectural decision must serve gameplay.

Technology never dictates the design of the game.

---

## Deterministic simulation

The game world is always deterministic.

Given the same world state and the same command, the engine must always produce the same result.

```
World State + Command = New World State
```

This property allows:

- reliable saves
- deterministic tests
- multiplayer synchronization
- replaying game sessions

---

## Single source of truth

The engine is the only authority regarding the game world.

Artificial intelligence never owns game state.

The LLM may describe the world.

It may never modify it directly.

---

## AI is a storyteller

The LLM is not the Game Master.

Instead, it acts as:

- narrator
- interpreter
- chronicler
- dialogue writer

The engine decides what happens.

The AI decides how it is told.

---

## Commands instead of text

Players interact using natural language.

Natural language is converted into structured commands.

Example:

Player input

> Attack the goblin with my axe

↓

Engine command

```
AttackCommand
Target = Goblin
Weapon = Axe
```

The engine never parses natural language.

---

## Events describe history

The engine records facts.

Examples:

- PlayerMoved
- ItemPickedUp
- MonsterKilled
- QuestCompleted

Events are immutable.

They describe what happened.

---

## Small independent systems

The engine is built from multiple independent subsystems.

Examples:

- movement
- combat
- inventory
- quests
- dialogue
- crafting
- factions

Each subsystem can evolve independently.

---

## Infrastructure independent

The engine contains no dependency on:

- Orleans
- SQL Server
- Semantic Kernel
- OpenAI
- Blazor
- ASP.NET
- Console

Infrastructure is only an implementation detail.

---

# Project Goals

The engine aims to provide:

- deterministic gameplay
- rich world simulation
- persistent worlds
- AI assisted narration
- moddability
- multiplayer support
- long-term maintainability

---

# Non Goals

This project does not try to build:

- a game engine with graphics
- a physics engine
- a scripting language
- an AI driven world simulation

The focus remains on deterministic role-playing mechanics.

---

# High Level Architecture

```
                Player
                   │
                   ▼
         Natural Language
           Interpretation
                   │
                   ▼
              Commands
                   │
                   ▼
            RPG Engine Core
                   │
         ┌─────────┴─────────┐
         ▼                   ▼
   World State          Game Events
         │                   │
         └─────────┬─────────┘
                   ▼
            AI Narration Layer
                   │
                   ▼
              Final Story
```

---

# Guiding Principle

The engine answers one question:

> What actually happened?

The AI answers another:

> How should the player experience it?