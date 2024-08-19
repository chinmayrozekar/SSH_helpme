
# tmux Command Line Documentation

## Overview
`tmux` is a terminal multiplexer that allows you to manage multiple terminal sessions from a single window. It's particularly useful for managing long-running processes, keeping sessions alive after disconnecting, and organizing workspaces.

## Installation
To install `tmux`, use the following command:
```bash
sudo apt-get install tmux
```

## Basic Commands

### 1. Starting a New Session
```bash
tmux new -s session_name
```
Starts a new `tmux` session with the specified name.

### 2. Detaching from a Session
```bash
tmux detach
```
Detaches from the current `tmux` session, leaving it running in the background.

### 3. Reattaching to a Session
```bash
tmux attach -t session_name
```
Reattaches to the specified `tmux` session.

### 4. Listing Sessions
```bash
tmux ls
```
Lists all active `tmux` sessions.

### 5. Killing a Session
```bash
tmux kill-session -t session_name
```
Terminates the specified `tmux` session.

## Pane Management

### 1. Splitting Windows
- **Horizontally**: 
  ```bash
  tmux split-window -h
  ```
- **Vertically**: 
  ```bash
  tmux split-window -v
  ```

### 2. Switching Between Panes
```bash
tmux select-pane -[UDLR]
```
Where `U`, `D`, `L`, and `R` are the directions (Up, Down, Left, Right).

### 3. Resizing Panes
```bash
tmux resize-pane -[UDLR] [size]
```
Resize the current pane in the specified direction by the given size.

## Window Management

### 1. Creating a New Window
```bash
tmux new-window -n window_name
```
Creates a new window with the specified name.

### 2. Navigating Between Windows
```bash
tmux select-window -t window_name
```
Switches to the specified window.

### 3. Renaming Windows
```bash
tmux rename-window window_name
```
Renames the current window to the specified name.

## Scripting with tmux
`tmux` can be scripted to automate session management. Example:
```bash
tmux new-session -d -s my_session
tmux send-keys -t my_session "echo 'Hello, World!'" C-m
tmux attach-session -t my_session
```
This script creates a new session, sends a command to it, and attaches to it.

## Troubleshooting

- **Lost connection**: Reattach to the session using `tmux attach -t session_name`.
- **Pane/Window layout issues**: Use `tmux select-layout even-horizontal` to reset layout.

## Additional Resources

For more detailed information, refer to the official `tmux` documentation or use:
```bash
man tmux
```
