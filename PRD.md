# Product Requirements Document (PRD): Prompts CLI v2

This document outlines the requirements for the next version of the Prompts CLI, a tool for managing prompts for large language models (LLMs).

## Executive Summary

The Prompts CLI v2 enhances the developer experience by introducing a more streamlined and powerful workflow for prompt management. Key improvements include automatic storage location management, content-addressable storage using hashes for de-duplication, fuzzy search capabilities, and a more flexible interactive command structure.

This document also outlines the requirements for building a terminal user interface (TUI) and a desktop application for managing prompts for large language models (LLMs) using the Tauri framework.

## Product Overview

### Problem Statement

Developers need a frictionless way to manage their LLM prompts. The previous version of the CLI required manual file management (`--file` parameter), which was cumbersome. Naming prompts was an extra step, and finding them relied on exact matches. This version aims to remove these barriers.

For users who are less comfortable with command-line interfaces, or for those who prefer a more feature-rich graphical environment, a dedicated desktop application is the ideal solution for prompt management.

While a CLI is powerful, some users prefer a more visual and interactive way to browse, search, and manage their prompts. A TUI can provide a more intuitive user experience for these users, while still remaining within the terminal environment.

### Solution Approach

The CLI will now manage its own storage, using a default location within the user's config or data directory. Prompts will be identified by a hash of their content, eliminating the need for manual naming and enabling automatic de-duplication. Commands will support both one-shot and interactive modes, and a fuzzy finder will help users quickly locate prompts.

The Prompts Tauri application will be a desktop application built using Tauri, with a web-based frontend (likely using a framework like React or Vue) and a Rust backend. It will be part of the `prompts-cli` repository, but will be built and distributed as a separate application.

The Prompts TUI will be built in Rust using the Ratatui library. It will be an integrated part of the `prompts-cli` binary, launched with a specific command or flag (e.g., `prompts-cli tui`).

### Target Audience

- Developers who utilize LLMs for software development, content generation, or automation.
- Users who are comfortable working in a command-line environment.
- Anyone who needs to manage a large collection of prompts efficiently.
- Users who prefer a graphical user interface (GUI) for their applications.
- Developers and content creators who want a dedicated and powerful tool for managing their prompts.
- Users who want a consistent prompt management experience across different operating systems (Windows, macOS, and Linux).
- Developers and power users who spend a significant amount of time in the terminal.
- Users who prefer a more visual and interactive experience than a traditional CLI.
- Those who want to manage their prompts without switching to a full graphical desktop application.

## Product Goals and Success Metrics

| Goal | Success Metric | Target |
|---|---|---|
| **Frictionless Prompt Management** | Time to add and retrieve a prompt is significantly reduced. | < 5 seconds per operation |
| **Intuitive User Experience** | High user satisfaction and adoption rates. | >95% positive feedback from users |
| **Robust and Scalable Storage**| The system handles thousands of prompts efficiently without performance degradation. | CRUD operations remain under 100ms with 10,000+ prompts |
| **Cross-platform Compatibility** | Builds and runs seamlessly on Linux, macOS, and Windows. | 100% supported platforms |
| User-friendly prompt management   | High user satisfaction and positive reviews  | High ratings in app stores/feedback channels |
| Native desktop experience         | Seamless integration with the host OS        | Use of native notifications, menus, etc. |
| Cross-platform compatibility      | Builds and runs on Linux/macOS/Windows       | 100% supported platforms       |
| Intuitive prompt management       | User satisfaction and ease of use            | High ratings from user feedback |
| Responsive and performant UI      | Smooth and lag-free user experience          | < 100ms response to user input |
| Seamless integration with CLI     | Easy to launch and exit the TUI from the CLI | Clear and simple commands      |

## User Stories

| Story ID | User Story | Acceptance Criteria | Priority |
|---|---|---|---|
| **US-001** | As a developer, I want the CLI to automatically manage where my prompts are stored so I don't have to think about it. | The CLI uses a default, user-specific directory (e.g., `~/.config/prompts-cli`). The user can override this with a `--config` flag. | P0 |
| **US-002** | As a developer, I want to add prompts without having to name them, and the tool should handle duplicates. | A prompt's content is hashed to create a unique ID. Adding an existing prompt is a no-op. | P0 |
| **US-003** | As a developer, I want to quickly find a prompt even if I only remember parts of it. | Commands that need to identify a prompt use a fuzzy search on the prompt text. | P0 |
| **US-004** | As a developer, I want to either provide a prompt directly in a command or have the CLI ask me for it. | Commands like `add`, `show`, `edit`, `delete` support both a one-shot mode (prompt in args) and an interactive mode (reads from stdin). | P1 |
| **US-005** | As a developer, when my fuzzy search returns multiple results, I want the CLI to show me the options so I can choose the correct one. | The CLI returns a structured JSON list of matching prompts, including their text and hash, for the user to make a specific choice. | P1 |
| US-006 | As a terminal user, I want a TUI to browse and manage prompts interactively. | Responsive Ratatui interface with keyboard navigation. | P1 |
| US-007 | As a desktop app user, I want a user-friendly UI for managing prompts with drag & drop and rich controls. | Tauri app with native integrations and a smoother UX. | P1 |
| **US-008** | As a developer, I want to use variables in my prompts so I can easily reuse them for different contexts. | The `generate` command supports a `--variable "key=value"` syntax. The prompt text can contain `{{key}}` placeholders. | P1 |
| **US-009** | As a developer, I want to organize my prompts with tags so I can easily find all prompts related to a specific topic. | The `add` and `edit` commands support a `--tag` flag. The `list` command can filter by tags. | P1 |
| US-010 | As a TUI user, I want to see a list of my prompts with their titles and tags. | A scrollable list of prompts is displayed on launch. | P1 |
| US-011 | As a TUI user, I want to be able to select a prompt and view its full content. | A dedicated view shows the full text of the selected prompt. | P1 |
| US-012 | As a TUI user, I want to be able to edit a prompt's content and metadata directly within the interface. | An editing mode allows for in-place modification of prompts. | P1 |
| US-013 | As a desktop user, I want to be able to use my mouse to navigate the application and interact with my prompts. | The application is fully navigable with a mouse. | P1 |
| US-014 | As a desktop user, I want to receive native notifications for certain events (e.g., when a prompt is successfully saved). | The application uses the OS's native notification system. | P1 |
| US-015 | As a desktop user, I want to be able to customize the application's appearance (e.g., with a light or dark theme). | The application provides theme customization options. | P2 |
| **US-016** | As a developer, I want to be able to import and export my prompts so I can share them with others or back them up. | The CLI has `import` and `export` commands that can handle a directory of prompt files. | P2 |
| **US-017** | As a developer, I want to configure the CLI using a configuration file so I don't have to pass the same flags every time. | The CLI reads `~/.config/prompts-cli/config.toml` for default settings. | P2 |
| **US-018** | As a TUI user, I want to be able to add and remove tags from a prompt in the TUI. | The TUI has a dedicated view for managing tags. | P1 |
| **US-019** | As a TUI user, I want to be able to filter the prompt list by typing a fuzzy search query. | The TUI has a search bar that filters the list in real-time. | P1 |
| **US-020** | As a TUI user, when I select a prompt with variables, I want the TUI to ask me to fill them in. | The TUI presents a form for entering variable values. | P1 |
| **US-021** | As a TUI user, I want to be able to copy a prompt's content to the clipboard. | A keybinding (e.g., `c`) copies the selected prompt's content. | P1 |

## Technical Architecture

The CLI will be built in Rust. Key libraries will include:
- **Clap**: For command-line argument parsing.
- **Directories**: For finding the appropriate user-specific storage location on different operating systems.
- **Sha2**: for hashing prompt content to create a unique ID.
- **Fuzzy-matcher**: For implementing fuzzy search.
- **Serde**: For serializing and deserializing prompt data.
- **Tera**: For prompt templating.

Prompts will be stored as individual JSON files in a dedicated directory. The filename for each prompt will be the SHA256 hash of its content.

The TUI will be built in Rust using the Ratatui and Crossterm libraries. It will be a module within the `prompts-cli` crate and will share the same core logic for prompt management.

The desktop application will be built using the Tauri framework. The frontend will be a single-page application (SPA) built with a modern web framework like React or Vue. The backend will be written in Rust and will be responsible for all the core prompt management logic.

## Feature Specification

- **Storage:**
    - **Default Location:** The tool will use a default directory (e.g., `~/.config/prompts-cli/prompts`).
    - **Custom Location:** A `--config` global flag will allow users to specify an alternative storage directory.
    - **Content-Addressable:** Prompts are stored in files named by the SHA256 hash of their content.
- **Configuration:**
    - A configuration file at `~/.config/prompts-cli/config.toml` can be used to set default values for the storage path, editor, and other settings.
- **Commands:**
    - `add [PROMPT_TEXT]`: Adds a new prompt. If `PROMPT_TEXT` is not provided, it reads from stdin. Can add tags with `--tag`.
    - `list [--tag TAG]`: Lists all stored prompts, showing a snippet and their hash. Can be filtered by tag.
    - `show [FUZZY_QUERY]`: Searches for a prompt. If multiple are found, returns a JSON list. If one is found, it's displayed. If `FUZZY_QUERY` is not provided, it reads from stdin.
    - `edit [FUZZY_QUERY]`: Same search mechanism as `show`. If a single prompt is identified, it opens it for editing (e.g., in the user's `$EDITOR`).
    - `delete [FUZZY_QUERY]`: Same search mechanism as `show`. Deletes the identified prompt after confirmation.
    - `generate [FUZZY_QUERY] [--variable "key=value"]`: Same search mechanism as `show`. Generates text based on the identified prompt, filling in any variables.
    - `import [DIRECTORY]`: Imports all prompts from a directory.
    - `export [DIRECTORY]`: Exports all prompts to a directory.
- **Fuzzy Search:**
    - Implemented for `show`, `edit`, `delete`, and `generate`.
    - Matches against the text of the prompts.
    - If multiple matches are found, outputs a JSON array of objects, where each object contains the prompt text and its hash.
- **Prompt Metadata:**
    - The `Prompt` struct will contain the prompt text, tags, and categories. The hash is used as the external identifier.
- **Templating:**
    - Prompts can contain variables in the format `{{key}}`.
    - The `generate` command can fill these variables using the `--variable` flag.
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
- **Graphical Prompt Management**: All the core CRUD, search, and filtering features will be available through a user-friendly GUI.
- **Rich Text Editing**: A "what you see is what you get" (WYSIWYG) editor or a code editor with syntax highlighting for editing prompts.
- **Drag and Drop**: The ability to drag and drop prompts to reorder them or organize them into folders.
- **Native OS Integration**: Use of native menus, notifications, and other OS-specific features.
- **Customization**: Options to customize the application's appearance and behavior.

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

- GUI or TUI interfaces.
- Syncing prompts across devices.
- Advanced versioning of prompts.
- Automatic syncing of prompts between devices.