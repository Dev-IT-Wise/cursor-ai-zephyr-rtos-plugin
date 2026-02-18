---
name: "Fix Permissions"
description: "Recursively set file permissions (chmod) for Docker/host access issues. Use a+rwx for dev environments only."
---
# fix-permissions

## Overview
Recursively sets permissions so all users can read, write, and execute files and directories. Use when you hit file access issues between a Docker container and the host (e.g. build artifacts or repo owned by different UIDs).

**Security:** `a+rwx` is very permissive. Use only in dev/Docker environments, not on production or shared systems.

## Command
Run from the **project root** (workspace directory):

```bash
sudo chmod -R a+rwx .
```

## Safer alternative
If you only need the host to read/write (and run dirs), use capital `X` so only directories get execute:

```bash
sudo chmod -R a+rX .
sudo chmod -R a+w .
```
