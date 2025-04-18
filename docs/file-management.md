# Linux File Management Commands

This document covers essential Linux commands for file and directory management operations.

## Basic File Operations

### ls (List Directory Contents)

```bash
# Basic listing
$ ls

# Long format listing
$ ls -l

# Show hidden files
$ ls -a

# Human-readable file sizes
$ ls -lh

# Sort by modification time (newest first)
$ ls -lt

# Sort by size (largest first)
$ ls -lS

# Recursive listing
$ ls -R

# Show file type indicators
$ ls -F
```

### touch (Create or Update Files)

```bash
# Create a new empty file
$ touch newfile.txt

# Create multiple files
$ touch file1.txt