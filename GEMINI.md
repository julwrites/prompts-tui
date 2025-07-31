# Gemini Development Guide: Prompts TUI

This document guides the development of the Prompts TUI, a terminal user interface for the Prompts project.

## Project Overview

The Prompts TUI is a terminal user interface for managing prompts for large language models (LLMs). It is built in Rust using the `ratatui` library and is a frontend for the `prompts-cli` core library.

## Core Tenets

- **Rust for Performance:** The TUI will be written in Rust to ensure high performance and a responsive user experience.
- **TDD Workflow:** Development will follow a strict Test-Driven Development (TDD) approach. Every new feature will start with a failing test.
- **Component-Based Architecture:** The TUI will be built using a component-based architecture to keep the UI code organized and maintainable.

## Development Workflow

1.  **Test First:** For any new feature, write a failing test that clearly defines the desired behavior.
2.  **Implement:** Write the minimum amount of code required to make the test pass.
3.  **Refactor:** Refactor the code to improve its design, readability, and performance, ensuring all tests still pass.
4.  **Repeat:** Repeat the cycle for the next feature.

## Key Technologies

- **Rust:** The primary programming language.
- **Ratatui:** For the terminal user interface.
- **Crossterm:** For terminal manipulation.
- **prompts-cli:** The core library for prompt management.

## Initial Setup

1.  **Initialize Cargo Project:** Set up a new Cargo project.
2.  **Add Dependencies:** Add `ratatui`, `crossterm`, and `prompts-cli`.
3.  **Write First Test:** Write a simple test to ensure that the basic TUI rendering is working correctly.
