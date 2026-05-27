# rsync Cheatsheet

## Basic Syntax
```bash
rsync [options] source destination
```

---

## Most Common Commands

### Local copy
```bash
rsync -av /source/dir/ /destination/dir/
```

### Push to remote server
```bash
rsync -av /local/dir/ user@host:/remote/dir/
```

### Pull from remote server
```bash
rsync -av user@host:/remote/dir/ /local/dir/
```

### Dry run (preview without changing anything)
```bash
rsync -av --dry-run /source/ /destination/
```

### Mirror source exactly (delete extras in destination)
```bash
rsync -av --delete /source/ /destination/
```

### Resume interrupted transfer with progress
```bash
rsync -avzP /source/ /destination/
```

### Exclude a folder
```bash
rsync -av --exclude='venv/' /source/ /destination/
```

### Exclude multiple folders
```bash
rsync -av --exclude='venv/' --exclude='.venv/' --exclude='node_modules/' /source/ /destination/
```

### Exclude by pattern
```bash
rsync -av --exclude='*.log' /source/ /destination/
```

### Backup over WireGuard / SSH
```bash
rsync -avzP --delete /local/dir/ user@host:/backup/dir/
```

---

## Common Flags

| Flag | Meaning |
|------|---------|
| `-a` | Archive — preserves permissions, timestamps, symlinks, owner, group |
| `-v` | Verbose — print each file as it transfers |
| `-z` | Compress data during transfer |
| `-P` | Show progress + resume partial transfers |
| `-n` | Dry run — preview only, no changes |
| `--delete` | Delete destination files not in source (mirror mode) |
| `--exclude` | Skip matching files or directories |
| `-e ssh` | Explicitly use SSH as the transport |

---

## Trailing Slash Rule

The trailing slash on the **source** controls whether the folder itself or just its contents are copied.

```bash
rsync -av /src/dir  /dest/   # copies the folder → /dest/dir/
rsync -av /src/dir/ /dest/   # copies contents  → /dest/
```

---

## rsync vs cp

| Feature | rsync | cp |
|---|---|---|
| Resumes interrupted transfers | ✅ | ❌ |
| Skips unchanged files | ✅ | ❌ |
| Works over SSH | ✅ | ❌ |
| Mirror with deletes | ✅ | ❌ |
| Progress visibility | ✅ | ❌ |
| Preserves all metadata | ✅ (with `-a`) | Partial |

---

## Estimated Transfer Times for 80GB

| Connection | Speed | Estimated Time |
|---|---|---|
| Local SSD → SSD | ~500 MB/s | ~3 min |
| Local HDD → HDD | ~100 MB/s | ~15 min |
| Gigabit LAN | ~100 MB/s | ~15 min |
| WireGuard (LAN) | ~50–80 MB/s | ~20–30 min |
| Fast home upload | ~50 MB/s | ~30 min |
| Average home upload | ~10 MB/s | ~2.5 hrs |
