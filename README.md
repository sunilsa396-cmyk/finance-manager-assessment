Part 1 – Application Design

Assignment: Advanced Mobile Application Development
Task: Design a cross-platform mobile app for managing personal finances

1. Overview

The application is a cross-platform personal finance manager built with React Native and native modules (Swift for iOS, Kotlin for Android).

Core Features:

Add, edit, and delete income/expense entries.

Categorize transactions (Food, Transport, Entertainment, etc.).

Visualize spending trends with charts (bar/pie).

Sync with backend API (mock or real).

Offline-first support with local database.

2. High-Level Architecture

Presentation Layer → React Native screens (JS/TS), UI components, navigation.

State Management → Redux Toolkit / React Context with middleware for async API calls.

Data Layer → SQLite or Realm for offline-first storage; AsyncStorage for small flags/tokens.

Sync & Network Layer → Axios + Sync Engine for reconciliation between local and server.

Native Modules:

iOS (Swift): Calendar & Reminders sync.

Android (Kotlin): Battery optimization state/events.

Backend (mock/real) → REST API (transactions, categories, auth).

Logging & Monitoring → Sentry (crashes), Flipper/Reactotron (debugging).

3. Technical Architecture Diagram
./assets/architecture-diagram.png)

4. Data Flow

User adds/edits/deletes transaction → stored in local DB.

Redux/Context updates state → UI reflects immediately (optimistic update).

Sync Engine pushes local changes to API and pulls new data from backend.

Charts read aggregated data from DB (category totals, monthly spends).

Native modules (Calendar/Battery) provide platform-level integrations.

5. Offline Storage & Sync

Storage: SQLite/Realm for transactions, categories. AsyncStorage for tokens/flags.

Strategy:

Optimistic UI (immediate local write).

Sync queue retries failed network requests.

Conflict resolution: last-write-wins using updatedAt.

Background sync on app resume/network reconnect.

6. Error Handling & Debugging Strategy

Error Handling:

Axios interceptors for retries & token refresh.

User-friendly error messages.

Sync status flags in DB (pending/synced/failed).

Debugging:

Flipper/Reactotron for network, logs, DB inspection.

Sentry for crash/error reporting.

Structured logs with levels (info, warn, error).
