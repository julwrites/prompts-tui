# Agent Instructions for `prompts-tui`

This document provides guidance for LLM agents working on the `prompts-tui` repository.

## Project Overview

This repository contains the terminal user interface (TUI) for the Prompts project. It is a Rust-based application built using the `ratatui` library. The TUI is a frontend for the `prompts-cli` core library, which is the sole dependency for this project.

## Core Tenets

- **Dependabot is Authoritative:** The `prompts-cli` dependency is managed by Dependabot. Do not manually update this dependency.
- **Focus on the UI:** The primary focus of this repository is the user interface. The core logic is handled by the `prompts-cli` library.
- **Component-Based Architecture:** The TUI is built using a component-based architecture. Each UI element is a separate component with its own state and logic.

## Development Workflow

1.  **Understand the `prompts-cli` API:** Before making any changes, familiarize yourself with the public API of the `prompts-cli` library.
2.  **Write Component Tests:** For any new UI component, write a test that renders the component and asserts on the rendered output.
3.  **Write Event Handling Tests:** For any new event handling logic, write a test that simulates the event and asserts on the application's state.
4.  **Run All Tests:** Ensure that all tests, including component and event handling tests, pass.

## Key Commands

- **Run tests:** `cargo test`
- **Build the project:** `cargo build`
