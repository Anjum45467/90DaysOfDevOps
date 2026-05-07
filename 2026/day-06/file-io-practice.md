# Linux READ, WRITE and APPEND Operations

---

## 1. Create an Empty File using touch

### Command

```bash
touch notes.txt
```

### Observation

- Created an empty file named `notes.txt`.
- Used for storing Linux practice notes.

---

## 2. Write Content into File using >

### Command

```bash
echo "Linux troubleshooting practice started." > notes.txt
```

### Observation

- Added first line into the file.
- `>` operator creates or overwrites file content.

---

## 3. Append Content using >>

### Command

```bash
echo "Learning file operations and redirection commands." >> notes.txt
```

### Observation

- Appended new content without deleting existing data.
- `>>` operator is used for appending content.

---

## 4. Use tee Command to Write and Display Output

### Command

```bash
echo "tee command writes and displays output simultaneously." | tee -a notes.txt
```

### Observation

- Displayed output on terminal and appended into file at the same time.
- `-a` option appends content instead of overwriting.

---

## 5. Read Full File using cat

### Command

```bash
cat notes.txt
```

### Observation

- Displayed complete content of the file.
- Useful for reading small text files quickly.

---

## 6. Read First 2 Lines using head

### Command

```bash
head -n 2 notes.txt
```

### Observation

- Displayed first 2 lines from the file.
- Useful for checking beginning of logs or configuration files.

---

## 7. Read Last 2 Lines using tail

### Command

```bash
tail -n 2 notes.txt
```

### Observation

- Displayed last 2 lines from the file.
- Commonly used for monitoring latest log entries.

---

# Final File Content

```text
Linux troubleshooting practice started.
Learning file operations and redirection commands.
tee command writes and displays output simultaneously.
```

---

# Key Learnings

- `touch` creates empty files.
- `>` overwrites file content.
- `>>` appends content.
- `cat` reads entire file.
- `head` reads starting lines.
- `tail` reads ending lines.
- `tee` displays and writes output simultaneously.
