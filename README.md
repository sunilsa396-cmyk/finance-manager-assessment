Part 1 – Application Design
Task: Design a cross-platform mobile app for managing personal finances

Overview
Cross-platform personal finance manager built with React Native and native modules (Swift for iOS, Kotlin for Android).

Core Features:
1.Add, edit, and delete income/expense entries.
2.Categorize transactions (Food, Transport, Entertainment, etc.).
3.Visualize spending trends with charts (bar/pie).
4.Sync with backend API (mock or real).
5.Offline-first support with local database.

## 🏗 High-Level Architecture

- **Presentation Layer**
  - React Native screens (JS/TS)
  - UI components & navigation

- **State Management**
  - Redux Toolkit / React Context
  - Middleware for async API calls

- **Data Layer**
  - SQLite or Realm → offline-first storage
  - AsyncStorage → small flags/tokens

- **Sync & Network Layer**
  - Axios for REST API communication
  - Sync Engine for reconciliation (local ↔ server)

- **Native Modules**
  - **iOS (Swift):** Calendar & Reminders sync
  - **Android (Kotlin):** Battery optimization state/events

- **Backend (Mock/Real)**
  - REST API for transactions, categories, authentication

- **Logging & Monitoring**
  - Sentry → crash reporting
  - Flipper / Reactotron → debugging


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
