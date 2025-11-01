---
applyTo: 'entrypoints/devtools-panel/**, hooks/**, utils/**, components/**, playwright/**'
---

# Devtools Panel Instructions

The devtools-panel entrypoint contains a React application that will load into a custom panel in the browser's devtools.

The devtools panel heavily relies on the components found in the [components](../../components/) directory, hooks from the [hooks](../../hooks/) directory, and utils from the [utils](../../utils/) directory.

## App Initialization

[DevtoolsPanelMain](../../entrypoints/devtools-panel/DevtoolsPanelMain.tsx) initializes the application:

1. It connects to the extension service worker, which allows packets to be sent and received from other parts of the extension
2. It loads the monaco editor (slimmed down version of VS Code for the web). This allows the user to compose custom WebSocket messages.
3. It initializes the application's state management store
4. It renders the App component, which then renders the rest of the application

## Major UI components

[AppSidebar](../../components/AppSidebar.tsx)

- Shows the host page's WebSocket connections
- User can select a WebSocket connection, which is used in other components

[MessageTable](../../components/MessageTable.tsx)

- Shows a preview of the selected WebSocket connection's incoming and outgoing messages
- User can click a button that will stop all messages on the selected WebSocket, except for messages created with the MessageComposer. Clicking the button again causes messages to resume.
- User can click a button that will clear all messages from the table
- User can search and filter the messages
- User can select a message, which opens the MessageDetail
- User can copy a message to the MessageComposer to easily create similar messages

[MessageDetail](../../components/MessageDetail.tsx)

- Displays the full payload of the WebSocket message that was selected in the MessageTable

[MessageComposer](../../components/MessageComposer.tsx)

- User can create custom WebSocket messages using the monaco editor
- User can send the custom message to the selected WebSocket connection's client or server

## State Management

Global state is currently handled using React's built-in context and reducer.

The `useSocketState` hook allows React components to subscribe to the global state and send packets to the extension service worker.

See the [useSocketState](../../hooks/useSocketState/) directory for state-management files.
