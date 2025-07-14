# Task List: Workout Time Tracker

## Based on PRD: prd-workout-tracker.md

## Relevant Files

- `WorkoutTracker/WorkoutTracker.csproj` – Main project file for .NET MAUI app
- `WorkoutTracker/MauiProgram.cs` – App entry point and dependency injection setup
- `WorkoutTracker/App.xaml` – Application resources and styling
- `WorkoutTracker/App.xaml.cs` – Application lifecycle management
- `WorkoutTracker/AppShell.xaml` – Shell navigation container
- `WorkoutTracker/AppShell.xaml.cs` – Shell navigation logic
- `WorkoutTracker/Models/WorkoutSession.cs` – Data model for workout sessions
- `WorkoutTracker/Services/IWorkoutService.cs` – Interface for workout session management
- `WorkoutTracker/Services/WorkoutService.cs` – Implementation of workout business logic
- `WorkoutTracker/Services/IDataStorageService.cs` – Interface for local data persistence
- `WorkoutTracker/Services/RealmDataStorageService.cs` – Realm.NET implementation for local data storage
- `WorkoutTracker/ViewModels/WorkoutViewModel.cs` – View model for workout timer and session management
- `WorkoutTracker/ViewModels/HistoryViewModel.cs` – View model for workout history display
- `WorkoutTracker/Views/WorkoutPage.xaml` – UI for workout timer and controls
- `WorkoutTracker/Views/WorkoutPage.xaml.cs` – Code-behind for workout timer UI
- `WorkoutTracker/Views/HistoryPage.xaml` – UI for displaying workout history
- `WorkoutTracker/Views/HistoryPage.xaml.cs` – Code-behind for history UI
- `WorkoutTracker.Tests/Services/WorkoutServiceTests.cs` – xUnit tests for workout business logic
- `WorkoutTracker.Tests/Services/RealmDataStorageServiceTests.cs` – xUnit tests for data persistence

### Notes

- This is a .NET MAUI application using Realm.NET for local data persistence
- MVVM pattern is used for separation of concerns
- All unit tests should use xUnit and live in a separate test project (e.g., `WorkoutTracker.Tests`)
- Use `dotnet test` to run the test suite
- Add the following package reference in the test project:
  ```xml
  <PackageReference Include="xunit" Version="[LATEST_VERSION]" />
  ```

## Tasks

* [ ] 1.0 **Project Setup and Core Infrastructure**

    * [ ] 1.1 Create new .NET MAUI project with Android target only
    * [ ] 1.2 Add Realm.NET and xUnit NuGet packages
    * [ ] 1.3 Set up dependency injection in MauiProgram.cs
    * [ ] 1.4 Configure app resources and styling in App.xaml
        * [ ] 1.4.a Define global styles and resources for the app, such as colors, fonts, and button styles.
        * [ ] 1.4.b Add support for light and dark themes to enhance user experience.
        * [ ] 1.4.c Ensure accessibility by using high-contrast colors and larger font sizes.
        * [ ] 1.4.d Define reusable styles for headers, footers, and cards to maintain consistency.
        * [ ] 1.4.e Plan for simple animations, such as button press effects or tab transitions, to enhance interactivity.
        * [ ] 1.4.f Specify icons for each tab (Workout, History, Settings) to improve navigation.
        * [ ] 1.4.g Plan for a tabbed layout with three main tabs: Workout, History, and Settings. These tabs will define the app's navigation structure.
    * [ ] 1.5 Set up Shell navigation in AppShell.xaml
        * [ ] 1.5.a Create the tabbed layout in `AppShell.xaml` using the styles, themes, and icons defined in **1.4**.
        * [ ] 1.5.b Add the three main tabs: Workout, History, and Settings.
        * [ ] 1.5.c Link each tab to its corresponding page (`WorkoutPage.xaml`, `HistoryPage.xaml`, `SettingsPage.xaml`).
        * [ ] 1.5.d (Optional) Add routes for deeper navigation if needed (e.g., WorkoutDetails).
        * [ ] 1.5.e Define functionality for the Settings tab
            * [ ] 1.5.e.a Add a theme toggle to switch between light and dark modes.
            * [ ] 1.5.e.b Add a location tracking toggle to enable or disable GPS tracking.
            * [ ] 1.5.e.c Add a clear history option to delete all workout session data.

* [ ] 2.0 **Workout Timer and Session Management**

    * [ ] 2.1 Design WorkoutPage.xaml with timer display and Start/Pause/Stop buttons
        * [ ] 2.1.a Ensure the page uses the reusable styles, icons, and animations defined in **1.4**.
    * [ ] 2.2 Implement WorkoutViewModel with timer logic (start, pause, resume, stop)
        * [ ] 2.2.a Register the ViewModel in the dependency injection container as defined in **1.3**.
    * [ ] 2.3 Bind UI controls to ViewModel commands
        * [ ] 2.3.a Confirm that the bindings align with the accessibility features (e.g., larger buttons, high-contrast colors) defined in **1.4**.
    * [ ] 2.4 Add logic to save session data (date, duration) on stop
        * [ ] 2.4.a Ensure compatibility with the data persistence tasks in **3.0**.
    * [ ] 2.5 Implement error handling for timer operations
        * [ ] 2.5.a Follow best practices for user feedback and error messages.

* [ ] 3.0 **Data Persistence with Realm.NET**
    * [ ] 3.1 Define WorkoutSession model for Realm
        * [ ] 3.1.a Include fields for date and duration.
        * [ ] 3.1.b Ensure the model inherits from `RealmObject`.
        * [ ] 3.1.c Add any additional fields if required (e.g., notes).
    * [ ] 3.2 Create IDataStorageService interface
        * [ ] 3.2.a Define methods for saving, retrieving, and deleting workout sessions.
        * [ ] 3.2.b Ensure the interface is flexible for different storage implementations.
    * [ ] 3.3 Implement RealmDataStorageService for CRUD operations
        * [ ] 3.3.a Implement the methods defined in `IDataStorageService`.
        * [ ] 3.3.b Use Realm.NET APIs for data persistence.
        * [ ] 3.3.c Test the implementation with sample data.
    * [ ] 3.4 Integrate data storage with WorkoutService
        * [ ] 3.4.a Inject `IDataStorageService` into `WorkoutService`.
        * [ ] 3.4.b Ensure workout session data is saved and retrieved correctly.
    * [ ] 3.5 Write xUnit tests for data storage logic
        * [ ] 3.5.a Test `RealmDataStorageService` methods for correctness.
        * [ ] 3.5.b Mock `IDataStorageService` for unit testing.
    * [ ] 3.6 Integrate OpenStreetMap for Workout Locations
        * [ ] 3.6.a Add an OpenStreetMap view to `WorkoutPage.xaml`.
        * [ ] 3.6.b Use the user's location at the start of the workout to place the marker.
        * [ ] 3.6.c Save the workout location data in a simple JSON file.
        * [ ] 3.6.d Ensure the map integration aligns with the app's styling and accessibility features.
            

* [ ] 4.0 **Workout History Display**
    * [ ] 4.1 Design HistoryPage.xaml to list past workout sessions
        * [ ] 4.1.a Create a layout to display workout sessions in a list format.
        * [ ] 4.1.b Ensure the design aligns with the app's global styles and themes.
    * [ ] 4.2 Implement HistoryViewModel to load and display sessions
        * [ ] 4.2.a Fetch workout session data from the data storage service.
        * [ ] 4.2.b Implement logic to handle empty or large datasets.
    * [ ] 4.3 Add sorting/filtering options (by date, duration)
        * [ ] 4.3.a Provide UI controls for sorting and filtering.
        * [ ] 4.3.b Implement sorting/filtering logic in the ViewModel.
    * [ ] 4.4 Bind history data to UI
        * [ ] 4.4.a Ensure data bindings are responsive and accessible.
        * [ ] 4.4.b Test bindings with sample data.
    * [ ] 4.5 Implement navigation from history to session details (optional)
        * [ ] 4.5.a Add navigation logic to open session details.
        * [ ] 4.5.b Ensure session details page displays relevant information.
    * [ ] 4.6 Add relative time display (e.g., "2 days ago", "Last Monday")
        * [ ] 4.6.a Implement a small helper to convert DateTime to user-friendly text.
        * [ ] 4.6.b Fallback to exact date if conversion fails.

* [ ] 5.0 **Edit and Delete Workout Sessions**
    * [ ] 5.1 Add edit and delete options to HistoryPage.xaml
        * [ ] 5.1.a Create UI elements for edit and delete actions.
        * [ ] 5.1.b Ensure the design aligns with the app's global styles and themes.
    * [ ] 5.2 Implement edit/delete logic in HistoryViewModel and data service
        * [ ] 5.2.a Add methods for editing and deleting workout sessions in the data service.
        * [ ] 5.2.b Ensure the ViewModel updates the UI after edit/delete actions.
    * [ ] 5.3 Confirm deletion with user prompt
        * [ ] 5.3.a Display a confirmation dialog before deleting a session, with options to cancel or confirm.
        * [ ] 5.3.b Ensure the dialog is accessible, user-friendly, and provides clear feedback on the action taken.
    * [ ] 5.4 Write xUnit tests for edit/delete functionality
        * [ ] 5.4.a Test edit and delete methods in the data service.
        * [ ] 5.4.b Mock the ViewModel for unit testing edit/delete logic.
    * [ ] 5.5 Add Share with WhatsApp feature
        * [ ] 5.5.a Create a button on HistoryPage.xaml for sharing workout sessions.
        * [ ] 5.5.b Implement logic in HistoryViewModel to format session data for sharing.
        * [ ] 5.5.c Send a simple text message via WhatsApp with workout details and coordinates.
        * [ ] 5.5.d Ensure the feature aligns with the app's global styles and themes.
        * [ ] 5.5.e Test the sharing functionality with sample data.

* [ ] 6.0 **Testing and Polish**
    * [ ] 6.1 Write unit tests for WorkoutService and ViewModels
        * [ ] 6.1.a Test all methods in `WorkoutService` for correctness.
        * [ ] 6.1.b Write unit tests for `WorkoutViewModel` and `HistoryViewModel`.
    * [ ] 6.2 Test app on Android simulator
        * [ ] 6.2.a Verify app functionality on Android devices.
        * [ ] 6.2.b Ensure UI/UX consistency across different Android screen sizes.
    * [ ] 6.3 Fix UI/UX issues and polish design
        * [ ] 6.3.a Address any design inconsistencies or bugs.
        * [ ] 6.3.b Ensure accessibility features are fully functional.
    * [ ] 6.4 Review and update documentation
        * [ ] 6.4.a Document all features and workflows.
        * [ ] 6.4.b Ensure the documentation is clear and user-friendly.
