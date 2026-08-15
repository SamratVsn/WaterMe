# WaterMe 🌱

WaterMe is a simple Android app, built with Jetpack Compose, that helps you remember to water your plants. Pick a plant from the list, choose a reminder interval, and WaterMe will notify you when it's time to give it some water.

## Features

- **Plant catalog** — browse a list of plants (succulents, houseplants, root vegetables, flowers, fruit, and more), each with a name, type, description, and suggested watering schedule.
- **Watering reminders** — set a reminder for any plant using preset intervals (e.g. 5 seconds for testing, 1 day, 7 days, 30 days).
- **Background notifications** — reminders are scheduled with WorkManager, so notifications fire even if the app isn't open.
- **Built entirely in Jetpack Compose** — a modern, declarative UI with Material 3 components.

## Tech stack

- **Kotlin**
- **Jetpack Compose** (Material 3, `LazyColumn`, `AlertDialog`, etc.)
- **WorkManager** (`androidx.work:work-runtime-ktx`) for scheduling delayed/background reminder notifications
- **ViewModel** (`androidx.lifecycle:lifecycle-viewmodel-compose`) for UI state management
- **Parcelize** for passing plant data between components

## Project structure

```
app/src/main/java/com/example/waterme/
├── MainActivity.kt              # App entry point
├── WaterMeApplication.kt        # Application class / DI container setup
├── Constants.kt                 # Reminder interval constants (5 sec, 1 day, 7 days, 30 days)
├── data/
│   ├── AppContainer.kt          # Simple app-level dependency container
│   ├── DataSource.kt            # Static list of plants
│   ├── Reminder.kt              # Reminder data model
│   ├── WaterRepository.kt       # Repository interface
│   └── WaterWorkManagerRepository.kt  # WorkManager-backed reminder scheduling
├── model/
│   └── Plant.kt                 # Plant data model
├── ui/
│   ├── WaterMeApp.kt            # Main Compose UI (plant list + reminder dialog)
│   ├── WaterViewModel.kt        # ViewModel exposing plant data to the UI
│   └── theme/                   # Compose theme (color, typography)
└── worker/
    ├── WaterReminderWorker.kt   # CoroutineWorker that fires the reminder notification
    └── WorkerUtils.kt           # Notification-building helpers
```

## Getting started

### Prerequisites

- [Android Studio](https://developer.android.com/studio) (latest stable release)
- JDK 11+
- An Android device or emulator running **API 24 (Android 7.0)** or higher

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/SamratVsn/WaterMe.git
   ```
2. Open the project in Android Studio.
3. Let Gradle sync and download dependencies.
4. Run the app on an emulator or physical device.

Alternatively, build from the command line:

```bash
./gradlew assembleDebug
```

## How it works

1. WaterMe loads a preset list of plants from `DataSource`.
2. Tap a plant to open a reminder dialog and choose how often you want to be reminded.
3. `WaterViewModel` passes the selection to `WaterWorkManagerRepository`, which schedules a `WaterReminderWorker` job via WorkManager.
4. When the scheduled time arrives, `WaterReminderWorker` runs in the background and posts a notification reminding you to water that plant.

## Contributing

Contributions, issues, and feature requests are welcome. Feel free to open a pull request or file an issue.

## License

No license has been specified for this project yet. If you plan to reuse this code, please check with the repository owner.
