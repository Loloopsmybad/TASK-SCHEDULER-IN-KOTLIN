# RAT — Revision Allocation Timetable

An Android app that takes your tasks and deadlines and automatically generates a
day-by-day study/work schedule for you. Built with **Kotlin** and **Jetpack Compose (Material 3)**.

> Repo name: `Android-app-development` · App name: **RAT** (`com.example.rat`)

## What it does

1. **Add tasks** — a name, a deadline (date), and how many minutes you estimate it will take.
2. **Generate a schedule** — the app splits each task's remaining time across the days
   until its deadline and lays out timed slots for each day, inserting **breaks** between slots.
3. **View the schedule** — a day-by-day, slot-by-slot timetable you can follow.

### Screens

| Route       | Screen             | Purpose                                             |
|-------------|--------------------|-----------------------------------------------------|
| `home`      | `HomeScreen`       | Task list, entry points to add a task / generate    |
| `add_task`  | `AddTaskScreen`    | Form to create a new task                           |
| `schedule`  | `ScheduleScreen`   | The generated timetable                             |

## Tech stack

- **Language:** Kotlin (2.2.10)
- **UI:** Jetpack Compose + Material 3, Navigation Compose, edge-to-edge
- **Architecture:** MVVM (`SchedulerViewModel` + `model` data classes)
- **Date handling:** `java.time` backported via core library desugaring (minSdk 24)
- **Build:** AGP 9.2.1, Gradle 9.4.1 (Kotlin DSL), version catalog in `gradle/libs.versions.toml`
- **SDK:** compileSdk 36, targetSdk 36, minSdk 24, Java 11

## Project structure

```
app/src/main/java/com/example/rat/
├── MainActivity.kt          # Entry point + NavHost with 3 routes
├── model/
│   ├── Task.kt              # name, deadline, estimated/remaining minutes
│   └── ScheduleSlot.kt      # task, day, start time, duration, break flag
├── viewmodel/
│   └── SchedulerViewModel.kt# Holds tasks, generates the schedule
├── screens/
│   ├── HomeScreen.kt
│   ├── AddTaskScreen.kt
│   └── ScheduleScreen.kt
└── ui/theme/                # Compose theme (Color / Type / Theme)
```

## Building & running

```bash
# Debug APK
./gradlew :app:assembleDebug

# Install & run on a connected device/emulator
./gradlew :app:installDebug

# Unit tests (JUnit 4)
./gradlew :app:testDebugUnitTest

# Instrumented tests (Espresso + Compose UI)
./gradlew :app:connectedDebugAndroidTest

# Everything (lint + tests)
./gradlew :app:check
```

On Windows use `gradlew.bat` instead of `./gradlew`.

## Conventions

- All dependencies are referenced through the **version catalog** (`libs.*` aliases) — don't hardcode versions in build files.
- Kotlin code style is `official` (set in `gradle.properties`).
- Release builds currently have minification disabled; ProGuard rules live in `proguard-rules.pro`.
- See `AGENTS.md` for agent-oriented build/test notes.
