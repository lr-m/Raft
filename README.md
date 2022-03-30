# Raft Consensus Algorithm
Implementation of the Raft Consensus Algorithm

## Research Paper
https://raft.github.io/raft.pdf

## Useful Visualisation
Interactive, good intro - http://thesecretlivesofdata.com/raft/
General, useful reference - https://raft.github.io/

## Running Instructions - Python

### Prerequisites
- Python 3.9 or later
- g++ with support for C++11
- Linux, native or on WSL2 (Mac OS X uses a different Clang implementation)
- For WSL2 Python users: Xming

Note: It is easiest to get the project up and running with a Linux machine.

### Steps
1. Navigate to the `Interface` directory.
2. For WSL2 users: Start XLaunch with `Multiple windows` support > `Start no client` > Check the `No Access Control` option.
3. Run ```python3 raft_interface.py```.
4. Wait for build to complete; a window with the Raft algorithm interface should show up.

## Implementation Details

This section details some of the main inner workings of the C++ code to make it easier to understand.

### JSON Library

Inter-process communication between Raft nodes uses the JSON format. C++ JSON library used is [nlohmann/json](https://github.com/nlohmann/json).

### Server
- The server class is essentially a sample implementation of a server that this algorithm is designed to run on. 
- It uses a thread to run the server_function in the class, which receives messages from other servers, and also sends details to the testing/web interface.
- The server has its own socket that it uses to receive messages, and also has the addresses of the other servers in the neighbours array, which is used to send messages between the servers.
- Server ID is used to determine the recipient server (stored alongside the address properties in neighbour struct).

### Manager
- This enables communication with the testing/web interfaces, and also manages initialisation of the servers.
- Has both send and receive sockets to communicate with the interfaces.
- The send function is utilised by the servers to communicate with the client.
- Port numbers for various functionality defined in the header, as well as the number of servers (limit of 5).

### Database
- This is the database that is instantiated on the servers, at the moment, it is an array of 5 integers. This is open to future expansion.
