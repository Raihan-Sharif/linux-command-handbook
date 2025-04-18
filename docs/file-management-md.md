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

For more advanced usage, see [examples/ls-examples.md](../examples/ls-examples.md)

### touch (Create or Update Files)

```bash
# Create a new empty file
$ touch newfile.txt

# Create multiple files
$ touch file1.txt file2.txt file3.txt

# Update access time only
$ touch -a file.txt

# Update modification time only
$ touch -m file.txt

# Set specific timestamp
$ touch -t 202304252030.45 file.txt  # Apr 25, 2023, 20:30:45
```

### cp (Copy)

```bash
# Copy a single file
$ cp source.txt destination.txt

# Copy multiple files to a directory
$ cp file1.txt file2.txt directory/

# Copy recursively (for directories)
$ cp -r source_dir/ destination_dir/

# Preserve all attributes
$ cp -a source.txt destination.txt

# Interactive (prompt before overwrite)
$ cp -i source.txt destination.txt

# Only copy if source is newer or destination doesn't exist
$ cp -u source.txt destination.txt
```

For more advanced usage, see [examples/cp-examples.md](../examples/cp-examples.md)

### mv (Move/Rename)

```bash
# Rename a file
$ mv oldname.txt newname.txt

# Move a file to a directory
$ mv file.txt /path/to/directory/

# Move multiple files
$ mv file1.txt file2.txt directory/

# Move a directory
$ mv source_dir/ destination_dir/

# Interactive (prompt before overwrite)
$ mv -i source.txt destination.txt

# No clobber (don't overwrite existing file)
$ mv -n source.txt destination.txt

# Move only if source is newer
$ mv -u source.txt destination.txt
```

### rm (Remove)

```bash
# Remove a file
$ rm file.txt

# Remove multiple files
$ rm file1.txt file2.txt

# Interactive deletion (ask before removing)
$ rm -i file.txt

# Remove recursively (for directories)
$ rm -r directory/

# Force removal without confirmation
$ rm -f file.txt

# Force recursive removal (be very careful!)
$ rm -rf directory/

# Remove empty directories
$ rmdir empty_directory/
```

### mkdir (Make Directory)

```bash
# Create a directory
$ mkdir new_directory

# Create multiple directories
$ mkdir dir1 dir2 dir3

# Create directory with specific permissions
$ mkdir -m 755 secured_directory

# Create parent directories as needed
$ mkdir -p parent/child/grandchild
```

## Advanced File Management

### ln (Link Files)

```bash
# Create a hard link
$ ln source.txt hardlink.txt

# Create a symbolic link
$ ln -s source.txt symlink.txt

# Create a symbolic link to a directory
$ ln -s /path/to/directory linkname

# Force creation of link
$ ln -sf target.txt symlink.txt
```

### find (Find Files)

```bash
# Find files by name
$ find /path -name "filename"

# Find files by pattern (case-insensitive)
$ find . -iname "*.txt"

# Find directories only
$ find . -type d

# Find files only
$ find . -type f

# Find files by size
$ find . -size +10M  # Files larger than 10MB
$ find . -size -1M   # Files smaller than 1MB

# Find by modification time
$ find . -mtime -7    # Modified in the last 7 days
$ find . -mtime +30   # Modified more than 30 days ago

# Find by permission
$ find . -perm 644    # Find files with exact permissions
$ find . -perm -u+x   # Find executable files

# Find and execute command
$ find . -name "*.log" -exec rm {} \;
$ find . -type f -size +100M -exec du -h {} \; | sort -nr
```

### dd (Disk Dump)

```bash
# Create a disk image
$ dd if=/dev/sda of=disk.img bs=4M status=progress

# Write an image to disk
$ dd if=disk.img of=/dev/sdb bs=4M status=progress

# Create a file of zeros (for testing)
$ dd if=/dev/zero of=test.img bs=1M count=100

# Create a random file
$ dd if=/dev/urandom of=random.data bs=1M count=1
```

### rsync (Remote Sync)

```bash
# Sync directories locally
$ rsync -av source_dir/ destination_dir/

# Sync to remote server
$ rsync -av source_dir/ user@remote:/path/to/dir/

# Sync from remote server
$ rsync -av user@remote:/path/to/dir/ local_dir/

# Dry run (show what would be done)
$ rsync -av --dry-run source/ destination/

# Sync with deletion (remove files that don't exist in source)
$ rsync -av --delete source/ destination/

# Sync with compression
$ rsync -avz source/ destination/

# Sync with bandwidth limit
$ rsync -av --progress --bwlimit=1000 source/ destination/
```

## File Compression and Archiving

### tar (Tape Archive)

```bash
# Create tar archive
$ tar -cf archive.tar file1 file2 directory/

# Extract tar archive
$ tar -xf archive.tar

# List contents of archive
$ tar -tf archive.tar

# Create gzipped tar archive
$ tar -czf archive.tar.gz directory/

# Create bzip2 compressed archive
$ tar -cjf archive.tar.bz2 directory/

# Extract gzipped archive
$ tar -xzf archive.tar.gz

# Extract to specific directory
$ tar -xf archive.tar -C /path/to/extract/

# Add files to existing archive
$ tar -rf archive.tar newfile.txt
```

### gzip/gunzip

```bash
# Compress a file
$ gzip file.txt

# Decompress a file
$ gunzip file.txt.gz

# Keep original file
$ gzip -k file.txt

# Set compression level (1-9, 9 is best)
$ gzip -9 file.txt

# Compress multiple files
$ gzip file1.txt file2.txt

# Compress all files in directory
$ gzip *
```

### zip/unzip

```bash
# Create zip archive
$ zip archive.zip file1 file2

# Create zip archive from directory
$ zip -r archive.zip directory/

# Add files to existing zip
$ zip -u archive.zip newfile.txt

# Extract zip archive
$ unzip archive.zip

# Extract to specific directory
$ unzip archive.zip -d /path/to/extract/

# List contents of zip file
$ unzip -l archive.zip

# Extract only specific files
$ unzip archive.zip "*.txt"
```

## File Attributes and Metadata

### stat (Display File Status)

```bash
# View file information
$ stat file.txt

# Format specific information
$ stat --format="%a %n" file.txt  # Permissions and name
```

### file (Determine File Type)

```bash
# Show file type
$ file document.pdf

# Brief format
$ file -b image.jpg

# Show MIME type
$ file --mime-type video.mp4
```

### chown (Change Owner)

```bash
# Change file owner
$ chown user file.txt

# Change owner and group
$ chown user:group file.txt

# Change recursively
$ chown -R user:group directory/

# Change symbolic link ownership
$ chown -h user:group symlink
```

### chgrp (Change Group)

```bash
# Change file group
$ chgrp developers file.txt

# Change recursively
$ chgrp -R developers directory/
```

### chmod (Change Mode/Permissions)

```bash
# Change permissions using octal notation
$ chmod 755 script.sh  # rwxr-xr-x

# Change permissions using symbolic notation
$ chmod u+x file.sh    # Add execute for user
$ chmod go-w file.txt  # Remove write for group and others
$ chmod a+r file.txt   # Add read for all

# Change recursively
$ chmod -R 644 directory/

# Apply only to files or directories
$ find directory -type f -exec chmod 644 {} \;
$ find directory -type d -exec chmod 755 {} \;
```

For more detailed permission management, see [examples/permissions-guide.md](../examples/permissions-guide.md)

## Special File Operations

### shred (Secure File Deletion)

```bash
# Overwrite file contents
$ shred file.txt

# Overwrite and remove file
$ shred -u file.txt

# Overwrite with specified number of passes
$ shred -n 10 -u file.txt
```

### truncate (Shrink or Extend File Size)

```bash
# Create empty file of specific size
$ truncate -s 1G large_file.img

# Shrink file to specific size
$ truncate -s 100M large_file.img
```

### split (Split Files)

```bash
# Split by size
$ split -b 1G large_file.img part_

# Split by line count
$ split -l 1000 large_file.txt output_

# Split with numeric suffixes
$ split -d -b 10M large_file.img segment_
```

### cat (Concatenate Files)

```bash
# Combine files
$ cat part1 part2 part3 > combined_file

# Create file with content
$ cat > newfile.txt << EOF
This is a new file
with multiple lines
EOF

# Append to file
$ cat >> file.txt << EOF
Additional content
EOF
```

## File Viewing and Editing

### cat (Display File Contents)

```