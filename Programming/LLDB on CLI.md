<!-- permalink: 6632506ec33abcc86e04a3ab7f4d3a47 DO NOT DELETE OR EDIT THIS LINE -->

# LLDB on CLI

1. Build with debug symbols
	* for spm
		* `swift build -c debug -Xswiftc -g`
1. run `lldb ./path/to/exe`
	* for spm, it'll be `swift build` followed by `lldb .build/debug/<your exe name>`
	* for spm tests, you can run `lldb .build/debug/<YourPackageName>PackageTests.xctest`
1. To set breakpoints
	* `breakpoint set --file FileName.swift --line 42`
1. `run`

## Cheatsheet

#### Starting LLDB
- **Launch LLDB with an executable**:
	- `lldb ./executable`

- **Attach to a running process by PID**:
	- `lldb -p <pid>`

- **Attach by process name**:
	- `lldb --attach-name <process-name>`

#### Basic Commands
- **Run the program**:
	- `run` or `r`

- **Continue execution**:
	- `continue` or `c`

- **Step over**:
	- `next` or `n`

- **Step into**:
	- `step` or `s`

- **Step out** (finish the current function):
	- `finish`

#### Breakpoints
- **Set a breakpoint by line number**:
	- `breakpoint set --file <file> --line <line-number>`

- **Set a breakpoint by function name**:
	- `breakpoint set --name <function-name>`

- **List all breakpoints**:
	- `breakpoint list`

- **Delete a breakpoint by ID**:
	- `breakpoint delete <breakpoint-id>`

#### Inspection
- **Print variable value**:
	- `print <variable-name>` or `p <variable-name>`

- **Examine memory**:
	- `memory read <address>`

- **Backtrace (stack trace)**:
	- `bt` or `thread backtrace`

- **List local variables**:
	- `frame variable` or `fr v`

- **Format output (e.g., hexadecimal)**:
	- `frame variable -f hex <variable-name>` or `p/x <variable-name>`

#### Modifying Execution
- **Set a variable's value**:
	- `expr <variable-name> = <value>`

#### Navigation
- **List source code**:
	- `list`

- **View disassembly**:
	- `disassemble` or `dis`

#### Exiting LLDB
- **Quit LLDB**:
	- `quit` or `exit`

#### Useful Aliases
- **Make your life simpler** by setting these up in an `.lldbinit` file: