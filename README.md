# Flare: Run your README.md like a Makefile

[![License: CC0](https://img.shields.io/badge/License-CC0-blue.svg)](LICENSE)

Flare merges documentation and scripts and lets you run code blocks directly from your `README.md`. Flare is lightweight, portable and has zero dependencies beyond standard Unix/Linux tools.

## tl;dr - Run your README.md
Add run targets to your README.md (or another document):
````markdown
## Run me
```bash [setup]{/bin/bash}
echo "Setting up environment..."
```
````
Copy flare to your project and run commands (README.md is the default):
```bash
./flare setup
```

## Why
Keeping documentation and project automization in sync is important for users and new developers. Flare makes it easy to avoid out-of-sync documentation and reduces redunant information by merging both into one document.

Flare acts as a command runner and is not meant to replace build tools but to make it easy to run parts of the documentation. Flare is:

- **Lightweight**: Flare is quite simple. It is in fact so simple that the default use case is to fork it whenever you need it. 
- **Portable**: Works on any Unix/Linux system without additional dependencies
- **Simple**: Single-file implementation, easy to understand and extend
- **Flexible**: Supports any interpreter or build system available on your system
- **Document-first**: Your markdown remains readable and usable as documentation
- **README-first**: By default works with your project's README.md
- **Permissive**: Flare is licensed under CC0. Do with it as you will.

## Installation

### Global installation
To run `flare` directly from command line, put `flare` in some location that is in your `path` environment variable.
If you are using bash, you can install flare by running (from within this repository):
```bash
./flare install
```
This executes the following script:

```bash [install]{/bin/bash}
# Create local bin directory if it doesn't exist
mkdir -p $HOME/.local/bin/

# Copy flare to the bin directory
cp flare $HOME/.local/bin/

# Make it executable
chmod +x $HOME/.local/bin/flare

# Add to PATH (if not already there)
if ! echo $PATH | grep -q "$HOME/.local/bin"; then
  echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
  source ~/.bashrc
  echo "Added ~/.local/bin to PATH"
fi
```
If you are not using bash, you probably need to adapt updating path.

You can now run flare by running `flare`.

### Local

No installation needed! Just copy the `flare` script to your project by running this inside the project directory:

```bash
# download flare
curl -fsSL https://raw.githubusercontent.com/glor/flare/refs/heads/main/flare -o flare
# make it executable
chmod +x flare
```
Then you can run flare locally with `./flare`.

## Make Your Markdown Files Executable

Add this to the top of your markdown file to make it directly executable:

```markdown
#!/usr/bin/env -S ./flare -f
```

Then make it executable and run it:

```bash
chmod +x README.md
./README.md         # List all commands
./README.md setup   # Run the setup command
```

This also works with files other than `README.md`.

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

Most markdown parsers and renderers remove command and interpreter so your document looks just like it used to. For end-user documentation, it is a good idea to add a code block on how to run a cell directly above.

## Usage
```bash
./flare -h
```
```
Usage: flare [options] [subcommand]

Options:
  -f FILE    Specify a markdown file to use (default: README.md)
  -h         Show this help message

If no subcommand is provided, lists all available subcommands in the notebook.
If a subcommand is provided, executes all code blocks tagged with that subcommand.

Examples:
  flare                     # List commands in README.md
  flare test                # Run [test] blocks in README.md
  flare -f notebook.md      # List commands in notebook.md
  flare -f notebook.md test # Run [test] blocks in notebook.md
```

## Examples

See [demo.md](demo.md) for a working example:

```bash
# Run with the demo file
./flare -f demo.md

# Run the test command from demo.md
./flare -f demo.md test
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

This project is licensed under the CC0 License which is similar to public domain. This means that you can use flare however you'd like and without citing my name. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- make
- https://github.com/0atman/blaze
- https://github.com/casey/just

Why "flare"? Because its like a blaze but sudden and usually brief.