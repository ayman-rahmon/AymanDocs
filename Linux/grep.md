# grep Cheat Sheet

A practical, copy-paste friendly guide for everyday work (logs, codebases, servers).

===

## Basics

```bash
grep "pattern" file
grep -n "pattern" file              # line numbers
grep -i "pattern" file              # case-insensitive
grep -w "word" file                 # whole word match
grep -F "literal.*[chars]" file     # fixed string (no regex)
grep -E "a|b|c" file                # extended regex (OR, +, ?, {})
```

Notes:
- `grep` uses **basic regex** by default. Use `-E` for extended regex.
- Quote your pattern to avoid shell expansion.

===

## Recursive search (project-wide)

```bash
grep -r "pattern" .                 # recursive
grep -rn "pattern" .                # recursive + line numbers
grep -rI "pattern" .                # ignore binary files
grep -r --include="*.ts" "pattern" .
grep -r --exclude="*.min.js" "pattern" .
grep -r --exclude-dir="node_modules" "pattern" .
```

Tip: for speed + .gitignore support, prefer `rg` (ripgrep) when available:
```bash
rg "pattern"
```

===

## Show context around matches (logs debugging)

```bash
grep -C 3 "error" app.log           # 3 lines before and after
grep -B 10 "error" app.log          # 10 lines before
grep -A 10 "error" app.log          # 10 lines after
```

===

## Multiple patterns

```bash
grep -E "error|failed|timeout" app.log
grep -e "error" -e "failed" app.log
grep -f patterns.txt app.log        # one pattern per line
```

`patterns.txt` example:
```text
error
failed
timeout
```

===

## Invert, count, list files

```bash
grep -v "debug" app.log             # invert match
grep -c "error" app.log             # count matches (per file)
grep -l "error" *.log               # list files that match
grep -L "error" *.log               # list files that do NOT match
```

===

## Useful output control

```bash
grep -o -E "ID=[0-9]+" file         # only the matching part
grep --color=always "error" app.log
grep -m 1 "pattern" file            # stop after first match
grep -H "pattern" file              # always show filename
grep -h "pattern" file1 file2       # hide filename
```

===

## Regex essentials (the ones you actually use)

### Anchors
```bash
grep "^ERROR" app.log               # starts with ERROR
grep "done$" app.log                # ends with done
```

### Character classes
```bash
grep -E "[0-9]{4}-[0-9]{2}-[0-9]{2}" app.log   # date like 2026-01-18
grep -E "[A-Za-z_][A-Za-z0-9_]*" file          # identifier-ish
```

### Quantifiers (need `-E`)
```bash
grep -E "colou?r" file              # optional
grep -E "ha+" file                  # one or more
grep -E "x{3,}" file                # 3 or more
```

### Any char and escaping
```bash
grep -E "a.*b" file                 # a then anything then b
grep "\[" file                     # literal [ (escape for shell + regex)
```

===

## Common dev tasks

### Find TODO / FIXME
```bash
grep -rn -E "TODO|FIXME" .
```

### Search for environment variables in Node
```bash
grep -rn "process\.env" .
```

### Find endpoints
```bash
grep -rn "/api/" .
grep -rn -E "GET |POST |PUT |DELETE " .
```

### Find config keys in JSON-ish
```bash
grep -rn '"gatewayCode"' .
grep -rn '"status"' .
```

### Find a function call style pattern (example)
```bash
grep -rn -E "verifyUserAccess\(access:\s*\{" .
```

===

## Log triage recipes (copy-paste)

### Top error lines (simple)
```bash
grep -i "error" app.log | head
```

### Count errors
```bash
grep -i "error" app.log | wc -l
```

### Exclude noisy lines then search
```bash
grep -v -E "healthcheck|heartbeat" app.log | grep -i "error"
```

### Find unique error messages (rough)
```bash
grep -i "error" app.log | sort | uniq -c | sort -nr | head
```

===

## grep with pipes (filters)

```bash
ps aux | grep -i node
journalctl -u nginx | grep -i "error"
docker logs my_container 2>&1 | grep -i "timeout"
```

Avoid matching the grep command itself:
```bash
ps aux | grep -i node | grep -v grep
```

===

## Binary files and weird encodings

```bash
grep -rI "pattern" .                # ignore binary
grep -a "pattern" file              # treat binary as text
```

===

## Quick reference for options

- `-r` recursive
- `-n` line numbers
- `-i` ignore case
- `-w` whole word
- `-v` invert
- `-c` count
- `-l` list matching files
- `-L` list non-matching files
- `-o` only match
- `-F` fixed string (no regex)
- `-E` extended regex
- `-A N` after context
- `-B N` before context
- `-C N` around context

===

## If you can install one thing: ripgrep

If available, `rg` replaces most grep usage and is faster and cleaner:
```bash
rg -n "pattern"
rg -i "pattern"
rg -g "*.ts" "pattern"              # include glob
rg -g "!node_modules/**" "pattern"
```
