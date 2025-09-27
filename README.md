# 🎮 C# & Unity MMO Client-Server

This project demonstrates the core process of real-time multiplayer communication by integrating a high-performance MMO game server, built from scratch in C#, with a client created in the Unity engine. It covers the entire process, from the server's foundational architecture to the client's actual movement packet transmission.

<br>

## 🚀 Key Feature Demo

Multiple clients connect to the server, send their position data, and the server broadcasts this information to all other clients to synchronize their positions in real-time.

**(It is highly recommended to add a GIF here showing multiple clients moving simultaneously!)**

[![multiple clients moving in a game world](https://github.com/Jeonhyeonmin/Unity-MMO-Client-Server/blob/main/Unity.gif?raw=true)
<br>

## 🏛️ Architecture

### 1. Server (C# Server Engine)

This server's design is modular, focusing on the key pillars of MMO technology. Each system was built from the ground up to ensure efficiency and control.

| Core System          | Key Concepts Implemented                                                                                   | Purpose                                                                                                      |
| :------------------- | :--------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------- |
| 🧠 **Multithreading** | `SpinLock`, `ReaderWriterLock`, Custom Thread Management, `MemoryBarrier`, Deadlock Avoidance, `Thread Local Storage (TLS)` | To achieve maximum concurrency and performance on multi-core processors while ensuring data integrity.         |
| 🌐 **Networking** | Asynchronous `Socket` Programming, Session Management, Custom `Send/Recv` Ring Buffers, TCP `Listener` & `Connector` | To handle thousands of simultaneous client connections with a non-blocking, low-latency I/O model.         |
| 📦 **Packet Handling** | Custom Binary Serialization, Automated C# Code Generation from XML/JSON Packet Definitions               | To create a highly efficient and error-free data protocol between the client and server.                     |
| ⚡️ **Concurrency & Jobs** | `Job Queue` System with a dedicated worker thread, Command Pattern, `Job Timer` for delayed execution      | To serialize critical game logic (like world updates) in a single thread, avoiding complex synchronization. |

<br>

### 2. Client (Unity Client)

The Unity client focuses on handling communication with the server and processing user interactions.

* **NetworkManager:** The core manager responsible for the TCP socket connection, session management, and handling incoming packets from the server.
* **MyPlayer (Player):** Represents the player object. It periodically generates a `C_Move` packet containing its position data and sends it to the server via the `NetworkManager`.
    * **(Why a Coroutine? 🤔)** Sending packets every frame in `Update()` can cause significant overhead. A `Coroutine` with `WaitForSeconds` is used to send packets periodically (every 0.25 seconds in this case) to manage network traffic efficiently.

<br>

## 🛠️ Tech Stack

* **Server:** C# (.NET Core)
* **Client:** Unity, C#
* **IDE:** Visual Studio

<br>

## ⚙️ Getting Started

1.  Run `Server.exe` located in the `Server/bin/Debug` folder to start the game server.
2.  Open the `Client` folder as a project in Unity Hub.
3.  Press the **Play** button in the Unity Editor to run the client.
4.  To test multiple clients, build the project (**File > Build and Run**) and then run multiple instances of the executable.

---

This project serves as a comprehensive portfolio piece demonstrating a strong understanding of low-level server programming and concurrent systems architecture.
