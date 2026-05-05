# Randomitas - Product Requirements Document

## Document Overview

**Product Name:** Randomitas  
**Platform:** iOS  
**Status:** Live on the App Store  
**Version:** 1.0  
**Date:** March 2026  
**Author:** Astor Luduena  
**Primary Audience for this Document:** Business Analyst / Product / Interview Review

## Executive Summary

Randomitas is an iOS application designed to reduce decision fatigue in everyday situations by helping users make fast, low-friction choices from personalized option lists.

This document was written retrospectively to formalize the product decisions made during development, and serves as a reference artifact for requirements analysis and product thinking.

The product addresses a common user problem: spending unnecessary time and mental energy deciding between multiple acceptable options such as what to eat, what to watch, where to go, or which activity to choose. Instead of forcing the user to manually evaluate each option every time, Randomitas provides a lightweight decision-support experience based on personalized lists and random selection.

The core value proposition is simple: users maintain their own structured decision sets, and the app delivers a fast, neutral, and repeatable outcome. This makes the decision process more efficient, reduces cognitive load, and increases convenience for recurring decision scenarios.

From a product perspective, Randomitas combines low setup complexity, high repeatability, and private on-device data persistence to create a utility product intended for frequent daily or weekly use.

## Problem Statement

Many users experience decision fatigue when facing repetitive, low-stakes decisions throughout the day. While each individual decision may seem minor, the cumulative effort creates friction, wasted time, and reduced satisfaction.

Existing alternatives are often either:

- Too generic and not personalized to the user’s real options
- Too manual, requiring users to recreate options repeatedly
- Too complex for a lightweight everyday use case

Randomitas solves this by offering a simple mobile-native experience where users can create reusable option structures and generate a decision instantly.

## Product Goal

Enable users to make quick, low-effort choices from personalized lists with a seamless iOS-native experience that supports reuse, organization, and trust in the selection process.

## Target Audience

### Persona 1: Everyday Decider

Users who frequently face small daily choices and want to reduce the time spent deciding.

**Typical scenarios**
- Choosing what to eat
- Choosing a movie or series
- Choosing a weekend activity

**Needs**
- Fast setup
- Minimal friction
- Reliable and simple decision flow

### Persona 2: Social Planner

Users who make decisions with friends, family, or a partner and want a neutral method to choose between options.

**Typical scenarios**
- Deciding where to eat
- Picking a game, plan, or destination
- Breaking indecision in group contexts

**Needs**
- Transparent result
- Fast outcome
- Easy reuse of stored options

### Persona 3: Structured Organizer

Users who prefer categorizing and organizing options over time, and want more control over what participates in the final choice.

**Typical scenarios**
- Maintaining topic-based decision lists
- Reusing curated options repeatedly
- Filtering or excluding options temporarily

**Needs**
- Persistent storage
- Hierarchical organization
- Control over inclusion and exclusion

## User Stories

### User Story 1

As a user, I want to create and save custom lists of options, so that I can reuse them whenever I need to make a decision quickly.

**Acceptance Criteria**
- The user can create a new item with a required name field.
- The system prevents creation of empty items.
- The system persists created items locally and reloads them after app restart.
- The user can edit, rename, and delete existing items.
- The UI reflects changes immediately after a successful save.

### User Story 2

As a user, I want to randomize a decision from my available options, so that I can avoid overthinking and reach an outcome in seconds.

**Acceptance Criteria**
- The system selects one valid item from the current visible set of eligible options.
- Hidden or excluded items do not participate in the randomization process.
- If no valid options exist, the system displays a clear empty-state or error message.
- The selected result is shown in a dedicated result view.
- The result can be stored in decision history.

### User Story 3

As a user, I want my lists and recent decisions to remain available between sessions, so that I do not need to recreate my data every time I open the app.

**Acceptance Criteria**
- User-generated lists persist between app sessions.
- Recent randomization results can be retrieved from history after reopening the app.
- Data persistence supports create, edit, delete, and update operations without integrity loss.
- The app restores the saved state during launch without requiring user setup.

## User Flow - Core Decision Flow

1. User opens app
2. User selects an existing list or creates a new one
3. User taps "Randomize"
4. System validates that eligible items exist
5. If no eligible items exist, the system displays an empty-state message
6. If eligible items exist, the system executes random selection
7. Result is displayed
8. Result is stored in history
9. User can re-randomize or navigate back

## Functional Requirements

### FR1. List and Item Management

- The system must allow users to create custom decision items.
- The system must allow users to rename, edit, and delete items.
- The system must support hierarchical organization of items.
- The system must support batch actions for selected items where applicable.
- The system must support marking items as favorites.

### FR2. Random Selection Engine

- The system must randomly select one eligible item from the current scope.
- The system must exclude hidden items and items under hidden parents from selection.
- The system must return a result with low latency and immediate UI feedback.
- The system must support a dedicated result presentation layer.

### FR3. Data Persistence

- The system must persist user data locally on the device.
- The system must persist core content including decision structures, favorites, and recent history.
- The system must restore persisted data on app relaunch.
- The persistence layer must maintain consistency between stored data and rendered UI state.

### FR4. History and Reusability

- The system must maintain a history of recent decision results.
- The system must allow users to review prior outcomes.
- The system must remove expired historical records according to the defined retention rule.

### FR5. UX and Platform Requirements

- The app must minimize the number of steps between launch and decision execution.
- The app must provide clear feedback for empty states, validation failures, and successful outcomes.
- The app must follow an iOS-native interaction model.
- The app must be implemented using Swift and SwiftUI.

## Non-Functional Requirements

- **NFR-01:** Random selection response time should remain below 300ms on supported devices under normal operating conditions.
- **NFR-02:** The app must support iOS 17.6 and above.
- **NFR-03:** Local user data must persist across app restarts and OS updates.
- **NFR-04:** The app must function fully offline with no network dependency.
- **NFR-05:** Core user flows must remain responsive during creation, editing, navigation, and randomization actions.
- **NFR-06:** User-generated data must remain local to the device unless future scope explicitly introduces synchronization features.

## Success Metrics (KPIs)

### Acquisition and Activation

- **First-Session Activation Rate:** percentage of users who create at least one item and complete at least one random decision during their first session.
- **List Creation Rate:** percentage of users who create more than one decision set or exceed a minimum number of items.

### Engagement

- **Decisions per Session:** average number of random selections executed in a session.
- **Sessions per Active User per Week:** average weekly usage frequency among active users.
- **Feature Reuse Rate:** percentage of users who return to an existing saved structure instead of creating one-off items only.

### Retention

- **Day 7 Retention:** percentage of users active seven days after install.
- **Day 30 Retention:** percentage of users active thirty days after install.

### Product Quality

- **Decision Completion Rate:** percentage of initiated decision flows that reach a final result.
- **Empty-State Failure Rate:** percentage of randomization attempts that fail because no eligible items are available.

## Technical Context

- **Language:** Swift
- **UI Framework:** SwiftUI
- **Persistence:** Local persistence architecture for user-generated decision data
- **Platform Positioning:** Lightweight native iOS utility app

## Assumptions

- Users value simplicity over advanced configuration in the first product iteration.
- The primary use case is recurring low-stakes decision support rather than complex planning.
- Reusability and persistence are key drivers of retention.

## Risks

- Low retention if the value proposition is not demonstrated in the first session.
- Low repeat usage if list creation feels too manual.
- Perceived randomness may not be enough to sustain engagement without recurring personal use cases.

## Out of Scope - Version 1.0

- Cloud synchronization or cross-device data sharing
- Social or collaborative decision lists
- Push notifications or scheduled reminders
- Android or web platform support
- Monetization or premium feature gating

## Future Opportunities

- Analytics-backed optimization of activation and retention funnels
- Optional onboarding to accelerate first value
- Shared or collaborative decision lists
- Smart suggestions or recommendation-enhanced randomization
- Cross-device sync

## Glossary

- **Item:** A single selectable option within a decision structure.
- **List/Folder:** A named group of items used as the scope for randomization.
- **Eligible Item:** An item that is visible, valid, and available for random selection.
- **History:** A time-limited log of recent randomization results.
- **Hidden:** A state applied to items or folders that excludes them from selection.
