#!/usr/bin/env -S ./flare -f
# Demo for Flare
## Setup
To set up flare, just copy the flare script to your project and do:
```bash [setup]{/bin/bash}
chmod +x ./demo.md
```

## Usage
Flare let's you run markdown files with code blocks like this:
```bash
./demo.md test
```

### Test
```bash
flare -f demo.md test
```
```bash [test]{/bin/bash}
echo "hi"
```

Here, `test` is the subcommand and this code will only be executed when you provide this subcommand as an argument to the notebook.

## Python
You can also run Python:

```python [test]{/usr/bin/python3}
print("Running tests...")
```
