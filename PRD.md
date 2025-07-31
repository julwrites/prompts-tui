# Product Requirements Document (PRD): Prompts TUI

This document outlines the requirements for building a terminal user interface (TUI) for managing prompts for large language models (LLMs).

## Executive Summary

The Prompts TUI provides a rich, interactive, and visually-oriented terminal interface for managing prompts. It is designed for users who prefer a more guided and graphical experience within their terminal, without leaving the keyboard-centric workflow.

## Product Overview

### Problem Statement

While a CLI is powerful, some users prefer a more visual and interactive way to browse, search, and manage their prompts. A TUI can provide a more intuitive user experience for these users, while still remaining within the terminal environment.

### Solution Approach

The Prompts TUI will be built in Rust using the Ratatui library. It will be an integrated part of the `prompts-cli` binary, launched with a specific command or flag (e.g., `prompts-cli tui`).

### Target Audience

- Developers and power users who spend a significant amount of time in the terminal.
- Users who prefer a more visual and interactive experience than a traditional CLI.
- Those who want to manage their prompts without switching to a full graphical desktop application.

## Product Goals and Success Metrics

| Goal                               | Success Metric                               | Target                          |
|-----------------------------------|----------------------------------------------|--------------------------------|
| Intuitive prompt management       | User satisfaction and ease of use            | High ratings from user feedback |
| Responsive and performant UI      | Smooth and lag-free user experience          | < 100ms response to user input |
| Seamless integration with CLI     | Easy to launch and exit the TUI from the CLI | Clear and simple commands      |

## User Stories

| Story ID | User Story | Acceptance Criteria | Priority |
|----------|------------|---------------------|----------|
| US-006 | As a terminal user, I want a TUI to browse and manage prompts interactively. | Responsive Ratatui interface with keyboard navigation. | P1 |
| US-010 | As a TUI user, I want to see a list of my prompts with their titles and tags. | A scrollable list of prompts is displayed on launch. | P1 |
| US-011 | As a TUI user, I want to be able to select a prompt and view its full content. | A dedicated view shows the full text of the selected prompt. | P1 |
| US-012 | As a TUI user, I want to be able to edit a prompt's content and metadata directly within the interface. | An editing mode allows for in-place modification of prompts. | P1 |
| US-018 | As a TUI user, I want to be able to add and remove tags from a prompt in the TUI. | The TUI has a dedicated view for managing tags. | P1 |
| US-019 | As a TUI user, I want to be able to filter the prompt list by typing a fuzzy search query. | The TUI has a search bar that filters the list in real-time. | P1 |
| US-020 | As a TUI user, when I select a prompt with variables, I want the TUI to ask me to fill them in. | The TUI presents a form for entering variable values. | P1 |
| US-021 | As a TUI user, I want to be able to copy a prompt's content to the clipboard. | A keybinding (e.g., `c`) copies the selected prompt's content. | P1 |

## Technical Architecture

The TUI will be built in Rust using the Ratatui and Crossterm libraries. It will be a module within the `prompts-cli` crate and will share the same core logic for prompt management.

## Feature Specification

- **Interactive Prompt List**: A scrollable and filterable list of all prompts.
- **Prompt Content View**: A detailed view of the selected prompt's content and metadata.
- **In-TUI Editing**: The ability to edit prompts directly within the TUI.
- **Keyboard-driven Navigation**: Intuitive keybindings for all actions.
- **Help and Documentation**: A help screen that explains the keybindings and features.
- **Visual Tag Management**: Add, remove, and view tags for each prompt.
- **Fuzzy Search Integration**: A search bar in the TUI to filter the prompt list.
- **Variable Input**: A form to enter values for variables in prompts.
- **Copy to Clipboard**: A keybinding to copy prompt content.
- **Color-Coded Tags**: Display tags with different colors.

## Architectural Considerations

- **State Management:** The TUI is a stateful application. A clear and robust state management solution is needed to handle the application's state, including the list of prompts, the user's selection, and user input. This could be a simple struct that is passed around, or a more advanced solution like a Redux-style store.
- **Component-Based Architecture:** To keep the UI code organized and maintainable, the TUI should be built using a component-based architecture. Each UI element (e.g., the prompt list, the content view, the search bar) should be a separate component with its own state and logic.
- **Event-Driven Architecture:** The TUI should use an event-driven architecture to handle user input and other events. This will make the application more responsive and easier to debug. A central event loop can process events from a channel and update the application state accordingly.
- **Performance:** The TUI needs to be fast and responsive, even with a large number of prompts. This means that the application should use efficient data structures and algorithms, and it should avoid blocking operations in the main UI thread. All interactions with the core `prompts-cli` library should be done asynchronously.

## Testing Strategy

- **Component Tests:** Each TUI component should be tested in isolation. This will involve creating a test that renders the component and then asserting on the rendered output. The `ratatui` library provides a `TestBackend` that can be used for this purpose.
- **Event Handling Tests:** The event handling logic should be tested to ensure that the application responds correctly to user input. This will involve simulating user input and then asserting on the application's state.
- **Snapshot Testing:** Snapshot testing should be used to ensure that the UI doesn't change unexpectedly. The `insta` crate is recommended for this purpose.
- **End-to-End Tests:** E2E tests will be created to test the application as a whole. This will involve running the TUI and then simulating user input to test the application's functionality. The `rexpect` crate can be used to control the TUI in a headless environment.

## Out of Scope for v2

- Syncing prompts across devices.
- Advanced versioning of prompts.
- Automatic syncing of prompts between devices.