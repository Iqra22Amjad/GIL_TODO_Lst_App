# Flutter TODO List App Documentation

## Table of Contents
1. [Introduction](#introduction)
2. [Application Structure](#application-structure)
3. [Key Components](#key-components)
4. [State Management](#state-management)
5. [Database Integration](#database-integration)
6. [Features](#features)
7. [Screens](#screens)
8. [UI/UX Design](#uiux-design)
9. [Error Handling](#error-handling)
10. [Future Improvements](#future-improvements)

## 1. Introduction

This Flutter application is an enhanced TODO list app that allows users to create, view, update, and delete tasks. It incorporates features such as image attachment, geolocation, and cloud storage integration, providing a rich user experience for task management.

## 2. Application Structure

The application follows a standard Flutter project structure with the main entry point in the `main()` function. It uses the Provider package for state management and integrates with Supabase for backend services.

Key structural elements:
- `main()`: Entry point of the application
- `MyApp`: Root widget of the application
- `TaskProvider`: Manages the state of tasks
- `HomeScreen`: Displays the list of tasks
- `AddEditTaskScreen`: Allows adding new tasks or editing existing ones
- `TaskDetailScreen`: Shows detailed information about a task

## 3. Key Components

### Task
The `Task` class represents the core data model of the application. It includes the following properties:
- `id`: Unique identifier for the task
- `description`: Text description of the task
- `isCompleted`: Boolean indicating whether the task is completed
- `imagePath`: Optional path to an attached image
- `latitude` and `longitude`: Optional geolocation coordinates
- `locationName`: Optional name of the location

The `Task` class includes methods for JSON serialization and deserialization, facilitating easy data transfer between the app and the backend.

### TaskProvider
`TaskProvider` is a ChangeNotifier class that manages the state of tasks. It handles CRUD operations on tasks and communicates with the Supabase backend. Key methods include:
- `_loadTasks()`: Fetches tasks from the backend
- `addTask()`: Adds a new task
- `updateTask()`: Updates an existing task
- `toggleTaskStatus()`: Toggles the completion status of a task
- `deleteTask()`: Deletes a task

## 4. State Management

The application uses the Provider package for state management. The `TaskProvider` is injected at the root of the widget tree in the `main()` function:

```dart
runApp(
  ChangeNotifierProvider(
    create: (context) => TaskProvider(),
    child: const MyApp(),
  ),
);
```

This allows any widget in the tree to access and modify the task data using `Provider.of<TaskProvider>(context)` or the `Consumer` widget.

## 5. Database Integration

The app integrates with Supabase for backend services. The Supabase client is initialized in the `main()` function:

```dart
await Supabase.initialize(
  url: 'SUPABASE_URL',
  anonKey: 'SUPABASE_KEY',
);
```

The `TaskProvider` class uses the Supabase client to perform CRUD operations on the 'tasks' table.

## 6. Features

1. **Task Management**: Users can create, view, update, and delete tasks.
2. **Image Attachment**: Tasks can include an attached image, which is uploaded to Supabase storage.
3. **Geolocation**: Users can add location information to tasks.
4. **Task Completion**: Tasks can be marked as completed or pending.
5. **Persistence**: All task data is stored in the Supabase backend, ensuring data persistence across app restarts.

## 7. Screens

### HomeScreen
- Displays a list of all tasks
- Uses a `SliverAppBar` for a dynamic header
- Implements a pull-to-refresh functionality
- Shows an empty state when no tasks are present
- Allows navigation to add a new task or view task details

### AddEditTaskScreen
- Dual-purpose screen for adding new tasks or editing existing ones
- Includes fields for task description, image attachment, and location
- Implements image picking from the device gallery
- Allows adding geolocation data to tasks

### TaskDetailScreen
- Shows detailed information about a specific task
- Displays the task image (if present), description, and location information
- Allows toggling the task completion status
- Provides options to edit or delete the task

## 8. UI/UX Design

The application uses Material Design 3 with a custom color scheme:

```dart
theme: ThemeData(
  colorScheme: ColorScheme.fromSeed(
    seedColor: const Color(0xFF6750A4),
    brightness: Brightness.light,
  ),
  useMaterial3: true,
  // ... other theme configurations
),
```

Key UI elements:
- Cards for displaying tasks with rounded corners
- Hero animations for smooth transitions between screens
- Custom buttons with icons for actions like adding images or location
- Dismissible widgets for swipe-to-delete functionality
- Floating Action Button for adding new tasks

## 9. Error Handling

The application implements basic error handling, primarily using try-catch blocks in the `TaskProvider` methods. Errors are logged to the console, but there's room for improvement in error reporting to the user.

## 10. Future Improvements

1. Implement user authentication for personalized task lists
2. Add task categories or tags for better organization
3. Implement push notifications for task reminders
4. Add a search functionality for tasks
5. Improve error handling and user feedback
6. Implement offline support with local caching
7. Add unit and widget tests for better code reliability
8. Implement data encryption for sensitive task information
9. Add support for recurring tasks
10. Implement task sharing or collaboration features

This documentation provides an overview of the Flutter TODO List application. For more detailed information about specific components or functionalities, refer to the inline comments in the source code.
