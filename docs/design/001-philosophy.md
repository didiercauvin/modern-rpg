# 001 - Design Philosophy

## Purpose

This document defines the fundamental philosophy of the engine.

It establishes the roles and responsibilities of every actor involved in a game.

Its purpose is to ensure that the engine always remains faithful to the author's intent while using Artificial Intelligence to enhance the player experience.

This document is normative.

If a future architectural decision contradicts this philosophy, the decision should be reconsidered.

---

# Vision

This project is **not** an AI Game Master.

It is a game engine capable of executing adventures created by authors.

Artificial Intelligence exists to improve immersion, not to replace the game designer.

The author always remains in control of the experience.

---

# Core Principle

> **The author writes the story.**
>
> **The engine enforces the rules.**
>
> **The AI tells the story.**

Each actor has a clearly defined responsibility.

None of them replaces another.

---

# The Four Actors

```
             Author
                │
                ▼
          Adventure Design
                │
                ▼
             Engine
                │
                ▼
        Artificial Intelligence
                │
                ▼
             Players
```

---

# The Author

The Author creates the experience.

The Author defines:

- the setting;
- the adventure;
- the important characters;
- the objectives;
- the possible endings;
- the progression;
- the narrative constraints.

The Author defines **what may happen**.

The Author also defines **what must never happen**.

---

# The Engine

The Engine is the authority.

Its responsibilities are:

- validating commands;
- executing gameplay rules;
- maintaining world state;
- enforcing scenario constraints;
- producing domain events;
- saving game progress.

The Engine is the only source of truth.

Nothing may modify the world without passing through the Engine.

---

# Artificial Intelligence

Artificial Intelligence is an interpreter.

It is not a Game Master.

Its responsibilities include:

- interpreting player input;
- generating descriptions;
- writing dialogues;
- adapting narration;
- summarizing game sessions.

Artificial Intelligence never decides:

- quest outcomes;
- combat results;
- important story events;
- world state modifications.

Every gameplay decision belongs to the Engine.

---

# Players

Players interact using natural language.

Their intentions are interpreted by the AI and validated by the Engine.

Players influence the story only through valid gameplay actions.

---

# Scenario Integrity

An Adventure defines the narrative boundaries.

Examples:

- important NPCs;
- mandatory events;
- optional events;
- forbidden actions;
- branching paths;
- victory conditions;
- failure conditions.

The Engine guarantees these constraints.

The AI must respect them.

---

# AI as an Actor

Artificial Intelligence behaves like an actor performing a script.

It may change:

- wording;
- pacing;
- atmosphere;
- emotional intensity;
- dialogue style.

It may never change:

- established facts;
- gameplay rules;
- scenario constraints;
- world state.

---

# Narrative Freedom

Players are free to attempt any action.

The AI translates their intention into structured commands.

The Engine determines whether those commands are valid.

The AI then narrates the outcome.

```
Player

↓

"I attack the king."

↓

AI

↓

AttackCommand(King)

↓

Engine

↓

Rejected

↓

Narration

"The royal guards intercept your attack before your blade reaches the king."
```

The AI does not invent the outcome.

It communicates it.

---

# Story Evolution

Stories emerge from player choices.

However, every story evolves inside the boundaries established by the Adventure.

The AI enriches those events.

It never replaces them.

---

# Canon

Everything validated by the Engine becomes canon.

The AI must always respect canon.

Canon includes:

- character status;
- world state;
- completed quests;
- discovered locations;
- established relationships;
- previous events.

The AI may never contradict canon.

---

# Separation of Responsibilities

| Responsibility | Owner |
|----------------|-------|
| Game mechanics | Engine |
| Story structure | Author |
| World consistency | Engine |
| Narrative quality | AI |
| Player decisions | Player |
| Scenario constraints | Adventure |

---

# Guiding Principle

The Engine asks:

> What actually happened?

The Adventure asks:

> What is allowed to happen?

The AI asks:

> How should this be experienced?

The Player asks:

> What do I want to do?

The Author answers:

> What story do I want players to live?