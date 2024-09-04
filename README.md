# irc

Internet Relay Chat or IRC is a text-based communication protocol on the Internet.It offers real-time messaging that can be either public or private. Users can exchange direct messages and join group channels. IRC clients connect to IRC servers in order to join channels. IRC servers are connected together to form a network.


Creating an IRC server (`ircserv`) in C++98 can be a challenging but rewarding project. Here’s a simplified step-by-step explanation of how you can implement it:

### Step-by-Step Implementation of `ircserv`

#### Step 1: **Understand Project Requirements**
- The server must handle multiple clients simultaneously using non-blocking I/O.
- Use `poll()` (or an equivalent function) for I/O multiplexing to manage multiple connections.
- Implement IRC commands like `NICK`, `USER`, `JOIN`, `PRIVMSG`, `KICK`, `INVITE`, `TOPIC`, and `MODE`.
- The server should follow the IRC protocol, handling user authentication and channel management.
- The server should be able to accept incoming connections on a specified port with a connection password.

#### Step 2: **Setup Your Project Structure**
- Create the necessary files: `Makefile`, header files (`*.h, *.hpp`), source files (`*.cpp`), and optionally, template files (`*.tpp`, `*.ipp`).
- Organize your project into logical components, such as `Server`, `Client`, `Channel`, and `CommandHandler`.

#### Step 3: **Create a Makefile**
- Write a `Makefile` to compile your project with targets like `all`, `clean`, `fclean`, and `re`.
- The `NAME` variable should define the executable name, `ircserv`.
- Ensure the `Makefile` handles compilation and linking correctly for all source files.

#### Step 4: **Implement the Main Entry Point (`main.cpp`)**
- The `main` function should parse command-line arguments: `port` and `password`.
- Validate that the `port` is a valid number and within the acceptable range (usually 1024-65535).
- Initialize the server with these parameters.

#### Step 5: **Create the `Server` Class**
- This class will manage the core functionality of the IRC server:
  - **Socket Setup**: Create a socket using `socket()`, set options with `setsockopt()`, and bind it to the specified `port` using `bind()`.
  - **Listening for Connections**: Call `listen()` to start listening for incoming client connections.
  - **Accepting Clients**: Use `accept()` to accept new connections.

#### Step 6: **Implement Non-Blocking I/O with `poll()`**
- Set the socket to non-blocking mode using `fcntl()` (on macOS) or `setsockopt()`.
- Use `poll()` to manage multiple file descriptors (clients) for reading and writing.
  - Initialize a `pollfd` array to keep track of each connected client and the server socket.
  - Continuously monitor the sockets for incoming connections, data to read, or data to write.

#### Step 7: **Handle Client Connections in `Client` Class**
- Create a `Client` class to represent each connected client.
- Store information like socket file descriptors, nicknames, usernames, and channels.
- Implement methods for receiving and sending messages (`recv()` and `send()`).

#### Step 8: **Implement Command Parsing and Execution**
- Create a `CommandHandler` class that processes incoming messages and executes appropriate IRC commands.
- Implement basic commands:
  - `NICK` and `USER` for setting up client identity.
  - `JOIN` for joining a channel.
  - `PRIVMSG` for sending private messages.
- Implement operator-specific commands: `KICK`, `INVITE`, `TOPIC`, and `MODE`.

#### Step 9: **Create a `Channel` Class**
- Manage channel-related functionality:
  - Store channel members and their roles (operator or regular user).
  - Handle channel modes (`i`, `t`, `k`, `o`, `l`) and their effects.
  - Implement methods for adding/removing users, managing topics, and handling mode changes.

#### Step 10: **Authentication and Security**
- Ensure clients authenticate with the correct password upon connecting.
- Store and validate client states to manage registration and prevent unauthorized access.

#### Step 11: **Testing and Debugging**
- Regularly test your server with an IRC client (like `WeeChat`, `irssi`, or `HexChat`).
- Use `nc` (netcat) for simple testing and verifying data handling and partial message processing.
- Debug potential issues related to concurrency, partial reads, buffer overflows, and command parsing.

#### Step 12: **Ensure Code Quality**
- Write clean, modular, and well-documented code.
- Ensure robust error handling for edge cases like network errors, invalid commands, or failed operations.
- Follow best practices for C++98 coding standards.

#### Step 13: **Final Checks and Submission**
- Double-check all the implemented features against the project requirements.
- Ensure your `Makefile` works correctly and all source files are included.
- Test your server thoroughly to confirm compliance with the IRC protocol.

By following these steps, you’ll be well on your way to successfully implementing your IRC server (`ircserv`) in C++98. If you need more details on any particular step or code snippets, feel free to ask!
