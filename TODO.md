# TODO for `prompts-tui`

This document outlines the implementation plan for the `prompts-tui` project, based on the requirements in the PRD.

## Phase 1: Basic TUI Structure

- **Task 1: Initialize the TUI application**
    - Sub-task: Set up the basic `ratatui` and `crossterm` backend.
    - Sub-task: Create the main application loop.
    - Test: Write a component test to ensure the basic TUI window renders correctly.

- **Task 2: Implement the prompt list view**
    - Sub-task: Display a scrollable list of prompts fetched from `prompts-cli`.
    - Sub-task: Implement keyboard navigation (up/down arrows).
    - Test: Write a component test to verify the list rendering and navigation.

## Phase 2: Prompt Details and Interaction

- **Task 3: Implement the prompt content view**
    - Sub-task: Display the full content of the selected prompt.
    - Test: Write a component test to verify content display.

- **Task 4: Implement in-TUI editing**
    - Sub-task: Allow editing of prompt content and metadata (tags, categories).
    - Sub-task: Integrate with `prompts-cli` for saving changes.
    - Test: Write an E2E test to verify editing and saving.

## Phase 3: Enhanced Features

- **Task 5: Implement visual tag management**
    - Sub-task: Display tags with different colors.
    - Sub-task: Allow adding and removing tags from within the TUI.
    - Test: Write component tests for tag display and interaction.

- **Task 6: Implement fuzzy search integration**
    - Sub-task: Add a search bar to filter the prompt list in real-time using `prompts-cli`'s fuzzy search.
    - Test: Write an E2E test to verify fuzzy search functionality.

- **Task 7: Implement variable input**
    - Sub-task: When a templated prompt is selected, prompt the user for variable values.
    - Sub-task: Pass variables to `prompts-cli`'s `generate` command.
    - Test: Write an E2E test to verify variable input and generation.

- **Task 8: Implement copy to clipboard**
    - Sub-task: Add a keybinding to copy the selected prompt's content to the clipboard.
    - Test: Write an E2E test to verify clipboard functionality.
