🐚 Minishell Project

🚀 Features

🖥️ Custom prompt (minishell$)

🧠 Command parsing with support for quotes and variables

🔗 Pipes and redirection support: >, >>, <, <<

📦 Environment variable expansion and editing

🧬 Built-in commands: cd, echo, pwd, export, unset, env, exit

🛑 Signal handling (Ctrl+C, Ctrl+\)

🔄 Command chaining with heredocs

🗂️ Project Structure

minishell/
├── main.c              # Entry point and main loop
├── parser/             # Tokenizing, parsing, quotes
│   ├── lexer.c
│   ├── parser.c
│   └── quotes.c
├── executor/           # Fork, execve, redirection, pipe
│   ├── executor.c
│   ├── pipe.c
│   └── redirection.c
├── builtins/           # Built-in commands implementation
│   ├── cd.c
│   ├── export.c
│   ├── env.c
│   ├── unset.c
│   ├── exit.c
│   └── echo.c
├── env/                # Environment variable utils
│   └── env_utils.c
├── signals/            # Signal handling
│   └── signals.c
├── utils/              # Helper functions
│   ├── ft_split.c
│   ├── free_utils.c
│   └── string_utils.c

💡 Key Concepts Learned

🧠 Parsing & Tokenizing

Handle quotes ', ", escape characters, and $VAR

Support for multi-stage parsing: lexer → syntax tree

🔗 Pipes & Execution

Use of pipe(), fork(), dup2(), execve()

Execute chained commands with correct file descriptors

📁 Redirections

open(), close(), dup2() for >, <, >>, <<

Heredoc: Read input until limiter, store in temp file

🚦 Signal Management

signal(), sigaction() to handle SIGINT, SIGQUIT

Special handling inside heredoc and child processes

🧬 Builtins & Env

Internal handling without forking when necessary

Manage environment via linked list (export/unset)

Expand variables during parsing (e.g. $HOME, $?)

🧪 Example Commands to Test

$ ls -la | grep minishell
$ echo Hello > out.txt && cat < out.txt
$ export NAME=Ömer && echo $NAME
$ cat << EOF
MiniShell is awesome!
EOF
$ cd ../ && pwd
$ exit 42

🎓 Educational Gains

Mastery of Unix system calls (fork, exec, pipe)

File descriptor manipulation

Complex string and memory management in C

Understanding shell architecture from the ground up

📜 License & Acknowledgements

This project is part of the 42 Network curriculum.
Feel free to fork, learn, and contribute!

