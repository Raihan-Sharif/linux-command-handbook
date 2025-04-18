# Advanced `cp` Command Examples

The `cp` command is used to copy files and directories in Linux. This guide provides detailed examples and use cases to help you make the most of this essential command.

## Basic Syntax

```bash
cp [OPTIONS] SOURCE DESTINATION
```

## Common Options

| Option | Description |
|--------|-------------|
| `-r`, `--recursive` | Copy directories recursively |
| `-i`, `--interactive` | Prompt before overwrite |
| `-f`, `--force` | Force copy by removing the destination file if needed |
| `-u`, `--update` | Copy only when source is newer than destination |
| `-v`, `--verbose` | Explain what is being done |
| `-p`, `--preserve` | Preserve mode, ownership, and timestamps |
| `-a`, `--archive` | Same as -dR --preserve=all (preserves everything) |

## Basic Examples

### Copy a Single File

```bash
# Basic file copy
$ cp source.txt destination.txt

# Create a backup of the file
$ cp source.txt source.txt.bak

# Copy with verbose output
$ cp -v source.txt destination.txt
```

### Copy Multiple Files

```bash
# Copy multiple files to a directory
$ cp file1.txt file2.txt destination_directory/

# Copy all text files to a directory
$ cp *.txt destination_directory/
```

### Copy Directories

```bash
# Copy directory and its contents
$ cp -r source_directory/ destination_directory/

# Copy directory contents only (note the trailing slash and dot)
$ cp -r source_directory/. destination_directory/
```

## Advanced Usage

### Preserving File Attributes

```bash
# Preserve mode, ownership and timestamps
$ cp -p source.txt destination.txt

# Preserve all attributes (archive mode)
$ cp -a source_directory/ destination_directory/
```

### Interactive and Forced Copying

```bash
# Ask before overwriting
$ cp -i file.txt destination/

# Force overwrite without prompting
$ cp -f file.txt destination/

# Update only if source is newer
$ cp -u file.txt destination/
```

### Copying with Progress Feedback

```bash
# Using verbose
$ cp -v largefile.iso /media/usb/

# With progress bar (using pv)
$ pv source.iso | sudo dd of=/dev/sdb bs=4M
```

### Symbolic Links

```bash
# Copy the actual file, not the link
$ cp source_link destination.txt

# Copy the link itself
$ cp -P source_link destination_link

# Follow links
$ cp -L source_link destination.txt
```

## Advanced Examples

### Backup Before Copying

```bash
# Create numbered backups
$ cp --backup=numbered file.txt destination/file.txt

# Create simple backup with ~ suffix
$ cp --backup=simple file.txt destination/file.txt
```

### Copying File Trees

```bash
# Copy an entire directory structure preserving all attributes
$ cp -a /source/directory/ /destination/

# Copy directory structure without copying specific files
$ cp -r /source/directory/ /destination/ --exclude="*.log" --exclude="*.tmp"
```

### Selecting Files to Copy

```bash
# Copy only files matching pattern
$ find source/ -name "*.txt" -exec cp {} destination/ \;

# Copy only files modified in the last day
$ find source/ -mtime -1 -type f -exec cp {} destination/ \;

# Copy only files larger than 1MB
$ find source/ -size +1M -type f -exec cp {} destination/ \;
```

### Copying and Transforming Files

```bash
# Copy and rename with sequential numbers
$ i=1; for file in *.jpg; do cp "$file" "new_image_$((i++)).jpg"; done

# Copy and change extension
$ for file in *.txt; do cp "$file" "${file%.txt}.md"; done
```

## Special Use Cases

### System Administration

```bash
# Copy system configuration with proper permissions
$ sudo cp -a /etc/nginx/nginx.conf /etc/nginx/nginx.conf.backup

# Deploy configuration files
$ sudo cp -r ./configs/* /etc/application/ --preserve=mode,ownership
```

### Development Workflow

```bash
# Copy project files excluding version control
$ cp -r project/ project_copy/ --exclude=".git"

# Quick build folder replication
$ cp -ru src/* build/ # Only update newer files
```

### Media Management

```bash
# Create optimized copies of images
$ for img in *.jpg; do convert "$img" -resize 50% "small_$img"; done

# Create directory with sorted media files
$ mkdir -p photos_by_year/{2020..2022}
$ find . -name "*.jpg" -exec sh -c 'year=$(date -r "$1" +%Y); cp "$1" "photos_by_year/$year/"' _ {} \;
```

## Combining with Other Commands

```bash
# Copy only specified file types
$ find . -name "*.cpp" -o -name "*.h" | xargs cp -t destination/

# Copy the largest files
$ find . -type f -exec du -h {} \; | sort -rh | head -5 | awk '{print $2}' | xargs -I{} cp {} /destination/

# Copy files containing specific text
$ grep -l "TODO" *.cpp | xargs cp -t /destination/todos/
```

## Error Handling

```bash
# Continue after errors
$ cp -r --no-clobber source/* destination/ 2>/dev/null || true

# Log errors when copying
$ cp -r source/* destination/ 2>cp_errors.log
```

## Best Practices

1. **Use `-i` (interactive mode)** when copying to avoid accidentally overwriting files
2. **Use `-u` (update mode)** for synchronizing directories
3. **Use `-a` (archive mode)** when you need to preserve all file attributes
4. **Use `-v` (verbose mode)** to see what's happening during complex operations
5. **Create backups** before potentially destructive operations
6. **Test complex commands** on a small set of files before running on important data

## Common Pitfalls

### Forgetting Trailing Slashes

The presence or absence of trailing slashes can change behavior:

```bash
# Copy directory itself to destination
$ cp -r source destination/  # Result: destination/source/

# Copy directory contents to destination
$ cp -r source/ destination/  # Result: files copied directly under destination/
```

### Permission Issues

```bash
# Copy preserving permissions but with sudo
$ sudo cp -a source/* /destination/

# Fix permissions after copy if needed
$ sudo chown -R user:group /destination/
```

### Symbolic Link Handling

By default, `cp` follows symbolic links to the destination file. Use `-P` to copy the symlinks themselves.

## Alternative Tools

For more complex copying tasks, consider:

- `rsync`: Better for synchronizing directories and remote copying
- `dd`: For block-level copying (disk images, etc.)
- `tar`: For preserving permissions and combining files when transferring

Remember to always use caution when copying files, especially when using options like `-f` (force) that can overwrite existing files without warning.
