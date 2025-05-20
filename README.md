# Flare: Executable Markdown Notebooks for Unix/Linux

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Flare is a lightweight, portable tool that turns Markdown files into executable notebooks. Run code blocks directly from your documentation with zero dependencies beyond standard Unix/Linux tools.

## Features

- **Portable**: Works on any Unix/Linux system without additional dependencies
- **Simple**: Single-file implementation, easy to understand and extend
- **Flexible**: Supports any interpreter available on your system
- **Efficient**: No overhead, direct execution of code blocks
- **Document-first**: Your markdown remains readable and usable as documentation

## Installation

No installation needed! Just copy the `flare` script to your project:

```bash
# Clone the repository
git clone https://github.com/yourusername/flare-git.git

# Copy the flare script to your project
cp flare-git/flare your-project/
```

Make the script executable:

```bash
chmod +x flare
```

## Quick Start

1. Create a markdown file (e.g., `notebook.md`) with tagged code blocks:

```markdown
# My Notebook

## Setup
```bash [setup]{/bin/bash}
echo "Setting up environment..."
```

## Run Analysis
```python [analyze]{/usr/bin/python3}
print("Analyzing data...")
```
```

2. Run commands from your notebook:

```bash
# List available commands
./flare notebook.md

# Run a specific command
./flare notebook.md setup
./flare notebook.md analyze
```

## Make Your Markdown Files Executable

Add this to the top of your markdown file to make it directly executable:

```markdown
#!/usr/bin/env ./flare
```

Then make it executable and run it:

```bash
chmod +x notebook.md
./notebook.md         # List all commands
./notebook.md setup   # Run the setup command
```

## Markdown Format

Flare uses a simple syntax to specify runnable code blocks in your markdown:

````markdown
```language [command-name]{/path/to/interpreter}
your code here
```
````

Where:
- `language`: Markdown code block language (for syntax highlighting)
- `[command-name]`: The subcommand used to execute this block
- `{/path/to/interpreter}`: The interpreter to use (optional, defaults to `/bin/sh`)

## Usage

### As a Command-Line Tool

```bash
# List all available commands in a notebook
./flare notebook.md

# Run a specific command from a notebook
./flare notebook.md command-name
```

### As a Shebang in Markdown Files

As shown above, you can also make markdown files directly executable.

## Examples

See [demo.md](demo.md) for a working example:

```bash
# Make the demo executable
chmod +x demo.md

# List available commands
./demo.md

# Run the test command
./demo.md test
```

## Use Cases

- **DevOps Documentation**: Embed server setup/deployment scripts directly in documentation
- **Data Science**: Create reproducible research notebooks without Jupyter
- **Development Workflows**: Document and execute project setup tasks
- **Technical Tutorials**: Create fully executable technical guides
- **Server Administration**: Documentation that can be executed on any system without dependencies

## How It Works

Flare parses markdown files to find code blocks with the specified command tag. When a command is run, it:

1. Extracts the code from the block
2. Creates a temporary file with the code
3. Executes the code with the specified interpreter
4. Cleans up the temporary file

## Portability

Flare is designed to be extremely portable:

- Uses POSIX-compliant shell (`/bin/sh`)
- Only depends on standard Unix utilities (`grep`, `sed`, `mktemp`)
- Works on any Unix/Linux environment without additional installations
- Can execute any script that has an available interpreter

## Contributing

This project is considered finished. Fixes and improvements are welcome, especially if they improve usability and portability.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- https://github.com/0atman/blaze
- https://github.com/casey/just