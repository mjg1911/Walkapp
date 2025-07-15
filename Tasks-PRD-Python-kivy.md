# Task List: Workout Time Tracker (Python + KivyMD)

## Based on PRD: prd-workout-tracker-kivy.md

## Relevant Files

- `main.py` – App entry point
- `kv/` – KivyMD language UI files (e.g., `workout.kv`, `history.kv`, `settings.kv`)
- `models/workout_session.py` – Model: Data model for workout sessions
- `services/data_service.py` – Model: Data persistence logic (local JSON file)
- `controllers/workout_controller.py` – Controller: Timer/session management logic
- `controllers/history_controller.py` – Controller: History display and session management
- `views/` – View: Python view classes (if not using pure KV)
- `tests/` – Unit tests (pytest or unittest)

### Notes

- This is a Python application using **KivyMD** (Material Design for Kivy) for UI
- The project uses the **MVC (Model-View-Controller) pattern** for separation of concerns:
    - **Model:** Handles data and business logic (e.g., workout session objects, JSON storage)
    - **View:** Handles UI (KivyMD `.kv` files and any Python view classes)
    - **Controller:** Handles user input, updates the model, and coordinates between model and view
- Use local JSON files for all data persistence (no SQLite, TinyDB, or other databases)
- All unit tests should use `pytest` or `unittest` and live in a separate `tests/` folder
- Use `pytest` or `python -m unittest` to run the test suite
- Add the following to `requirements.txt`:
  ```
  kivy
  kivymd
  kivy-garden.mapview  # for map display
  pytest  # or unittest
  plyer   # for GPS/location (optional)
  pywhatkit # for WhatsApp sharing (optional)
  ```

## Tasks

* [ ] 1.0 **Project Setup and Core Infrastructure (MVC, KivyMD)**

    * [ ] 1.1 Set up new Python project with KivyMD
        * [ ] 1.1.a Create a virtual environment
        * [ ] 1.1.b Install dependencies (`kivy`, `kivymd`, `kivy-garden.mapview`, etc.)
    * [ ] 1.2 Create basic KivyMD app structure
        * [ ] 1.2.a `main.py` entry point
        * [ ] 1.2.b `kv/` folder for `.kv` files (View, KivyMD)
        * [ ] 1.2.c `views/`, `models/`, `controllers/` folders (MVC)
    * [ ] 1.3 Configure screen management and navigation (3 screens) using KivyMD widgets
        * [ ] Workout
        * [ ] History
        * [ ] Settings
    * [ ] 1.4 Define global styles and Material Design theme (KivyMD)
        * [ ] Themes: darkmode toggle (KivyMD theme engine)
        * [ ] Fonts, icons, spacing (Material Design)
        * [ ] Header/footer styling (using KivyMD components)

* [ ] 2.0 **Workout Timer and Session Management (MVC, KivyMD)**

    * [ ] 2.1 Design Workout screen (KV layout, View, KivyMD)
        * [ ] Timer display (using KivyMD widgets)
        * [ ] Start / Pause / Stop buttons (MDButton)
        * [ ] Show map widget on Workout screen
        * [ ] Display user's current location on the map
        * [ ] Add MapView widget to Workout screen
        * [ ] Request location permissions (Android)
        * [ ] Fetch current GPS coordinates using plyer **once, when the user presses Start**
        * [ ] Save the start location  for the session
        * [ ] Fetch current GPS coordinates using plyer **again, when the user presses Stop**
        * [ ] Save the stop location  for the session
        * [ ] Center map on user’s location and add marker
        * [ ] Show a loading indicator while fetching location (KivyMD progress widget)
        * [ ] Handle errors if location cannot be fetched (e.g., permissions denied, GPS unavailable)
        * [ ] Do not update or track location between start and stop (no live tracking)
    * [ ] 2.2 Implement timer logic in controller (Controller)
        * [ ] Start / pause / resume / stop session
        * [ ] Display elapsed time
        * [ ] Prevent timer from starting twice
        * [ ] Handle app closing mid-session
    * [ ] 2.3 Save session data on stop (Model)
        * [ ] Save `start_time`, `end_time`, `duration`, start location , and stop location  to local JSON file
        * [ ] Confirm to the user when a session is saved (with both locations, use KivyMD dialog)
        * [ ] Optionally, allow the user to edit the locations before saving

* [ ] 3.0 **Data Persistence Layer (Model)**
    * [ ] 3.1 Define `WorkoutSession` model
        * [ ] Fields: id, start_time, end_time, duration, start_latitude, start_longitude, stop_latitude, stop_longitude, optional note
        * [ ] Define the JSON schema for a workout session (show an example)
    * [ ] 3.2 Implement data service (local JSON file)
        * [ ] Save session
        * [ ] Retrieve all sessions
        * [ ] Delete / update session
        * [ ] Implement safe read/write with file locking or error handling
        * [ ] Handle the case where the JSON file does not exist or is corrupted
    * [ ] 3.3 Optional: Add basic location logging
        * [ ] Use `plyer` for GPS (Android only)
        * [ ] Save start and stop lat/lon in session

* [ ] 4.0 **Workout History Display (MVC, KivyMD)**
    * [ ] 4.1 Design History screen layout (View, KivyMD)
        * [ ] List of previous sessions (use KivyMD list widgets)
        * [ ] Show date, duration, start and stop locations, optional note
    * [ ] 4.2 Add sorting and filtering (Controller/Model)
        * [ ] Sort by date or duration
        * [ ] Filter past X days/weeks
    * [ ] 4.3 Navigation to session details (optional, Controller/View)
        * [ ] View full session data on tap (use KivyMD dialogs or screens)
    * [ ] 4.4 Relative time display helper (Controller/Model)
        * [ ] e.g. “2 days ago”, “Last Monday”

* [ ] 5.0 **Edit and Delete Workout Sessions (MVC, KivyMD)**
    * [ ] 5.1 Add UI options to edit/delete (View, KivyMD)
    * [ ] 5.2 Confirm deletion with popup (View/Controller, KivyMD dialog)
    * [ ] 5.3 Update session in local JSON file (Model/Controller)
    * [ ] 5.4 Reflect changes in UI instantly (Controller/View)
    * [ ] 5.5 Optional: Share session with WhatsApp (Android only)
        * [ ] Use `pywhatkit` or `plyer`
        * [ ] Format session as simple text message

* [ ] 6.0 **Testing and Polish**
    * [ ] 6.1 Write unit tests (with `unittest` or `pytest`)
        * [ ] Timer logic (Controller/Model)
        * [ ] Data service (save/load/delete) (Model)
        * [ ] Test saving/loading sessions with/without location
        * [ ] Test on devices with/without GPS
        * [ ] Test map display on different screen sizes
    * [ ] 6.2 Manual testing on Android emulator
        * [ ] UI scaling
        * [ ] Dark/light mode
        * [ ] Permissions (if using GPS)
    * [ ] 6.3 Final design polish
        * [ ] Improve visual hierarchy (View, KivyMD)
        * [ ] Ensure touch targets are large (View, KivyMD)
        * [ ] Smooth animations (optional, View, KivyMD)
    * [ ] 6.4 Document setup and usage
        * [ ] Developer README
        * [ ] Screenshots/GIFs of app 