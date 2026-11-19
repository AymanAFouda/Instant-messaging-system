# Instant Messaging System

A JavaFX-based client-server instant messaging application that enables multiple users to connect to a central server, view active users, initiate private chat sessions, and exchange text messages in real time.

Developed as a course project for **Computer Networks I**, the application demonstrates socket programming, multithreading, and JSON-based communication through a custom client-server messaging protocol.

## Features

- **Client-Server Architecture:** Separate client and server applications communicate through network sockets.
- **Multiple Concurrent Clients:** Multithreading allows the server to handle multiple client connections simultaneously.
- **Active Users List:** Displays currently connected users and automatically updates when users connect or disconnect.
- **Private Chat Sessions:** Users can initiate individual chat sessions with other connected users.
- **Real-Time Messaging:** Exchange text messages between users through the central server.
- **JSON-Based Communication:** Client-server messages follow a structured JSON-based protocol with different message types.
- **JavaFX GUI:** Graphical user interface for managing connections, viewing active users, and exchanging messages.

## Technologies Used

| Technology | Purpose |
|---|---|
| Java (JDK 22) | Primary programming language |
| JavaFX | Graphical user interface |
| Java Socket Programming | Network communication between clients and the server |
| Java Threads | Handling multiple client connections concurrently |
| JSON | Formatting messages exchanged between clients and the server |
| IntelliJ IDEA Community Edition | Development environment |

## System Architecture

The application consists of two main components: `IMServer` and `IMClient`.

### 1. Server (`IMServer`)

The server acts as the central communication point between connected clients.

Its main responsibilities include:

- Opening a server socket and accepting incoming client connections.
- Creating a separate `ClientThread` for each connected client.
- Reading and processing messages received from clients.
- Maintaining the list of currently active users.
- Broadcasting active user list updates whenever a client connects or disconnects.
- Forwarding chat initiation requests and text messages to their intended recipients.

**Main Classes:**

| Class | Responsibility |
|---|---|
| `Server` | Initializes the server, accepts connections, manages client threads, and forwards messages. |
| `ClientThread` | Handles communication with an individual client, processes incoming messages, and sends responses. |
| `Message` | Encapsulates the data exchanged between the client and server. |

### 2. Client (`IMClient`)

The client is a JavaFX desktop application that allows users to connect to the server and communicate with other connected users.

Its main responsibilities include:

- Establishing a socket connection with the server.
- Sending connection, chat, text, and disconnection messages.
- Receiving and processing messages from the server.
- Displaying the list of active users.
- Opening individual chat windows and displaying exchanged messages.

**Main Classes:**

| Class | Responsibility |
|---|---|
| `Main` | Entry point of the client application and responsible for launching the JavaFX application. |
| `Client` | Manages the socket connection and sending and receiving messages. |
| `Message` | Encapsulates messages exchanged between the client and server. |
| `Controller` | Handles application events and coordinates the main GUI components. |
| `ChatController` | Manages the active users list and related chat functionality. |
| `UserItemController` | Handles chat window events and displays text messages. |

## Communication Protocol

The application uses a custom client-server protocol in which messages are exchanged as JSON-formatted strings.

Each message must contain a message type, which determines the additional data fields required.

The protocol supports the following message types:

| Message Type | Direction | Description | Data Fields |
|---|---|---|---|
| `Connect` | Client → Server | Establishes a connection with the server. | `name` |
| `Users` | Server → All Clients | Updates the active users list whenever a user connects or disconnects. | `activeUsers` |
| `Chat` | Client → Server → Recipient | Initiates a chat session with another user. The server forwards the message to the recipient. | `from`, `to` |
| `Text` | Client → Server → Recipient | Sends a text message to another user through the server. | `from`, `to`, `text` |
| `Disconnect` | Client → Server | Notifies the server that a client is disconnecting. | None |

### Communication Workflow

1. A client sends a `Connect` message containing the user's name.
2. The server registers the user and broadcasts a `Users` message containing the updated active users list.
3. A user selects another connected user and initiates a chat session using a `Chat` message.
4. The server forwards the chat initiation message to the intended recipient.
5. Both users can exchange text messages using `Text` messages, which the server forwards to their intended recipients.
6. When a client disconnects, it sends a `Disconnect` message, and the server broadcasts the updated active users list to the remaining clients.

## Project Structure

The repository is organized into two main directories:

```text
Instant-messaging-system/
│
├── IMClient/
│   └── Client application and JavaFX GUI
│
└── IMServer/
    └── Server application and client connection handling
```

## Testing

The application was tested manually using three laptops:

- One laptop running the server.
- Two laptops running client applications.

The following scenarios were tested:

| Test Scenario | Expected Result |
|---|---|
| Client connects to the server. | The client's username appears in the active users list for all connected clients. |
| Client disconnects from the server. | The client's username is removed from the active users list for all remaining clients. |
| Client initiates a chat session. | A chat window appears for both users. |
| Client sends a text message. | The message appears in the chat window of both users. |

## How to Run

The project was developed using **Java JDK 22**, **JavaFX**, and **IntelliJ IDEA Community Edition**.

To run the application:

1. Open the server and client projects in IntelliJ IDEA.
2. Configure the projects to use JDK 22.
3. Configure the JavaFX runtime and dependencies for the client application.
4. Run the server application using the `Server` main class.
5. Launch the client application using the `Main` class on the client machines.
6. Connect the clients to the running server using their configured network connection settings.

**Note:** The exact build configuration, JavaFX version, server address, and port settings depend on the project source and configuration files.

## Course Information

- **Course:** Computer Networks I
- **Instructor:** Asst. Prof. Evrim Güler
- **Project Date:** May 15, 2024

## Team Members

- **Ayman Fouda**
- **Osama Fouda**
