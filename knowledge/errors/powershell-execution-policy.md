# PowerShell Execution Policy Error

**Category:** errors
**Tags:** windows, powershell, batch, scripts
**Source:** Claude_Max
**Created:** 2025-02-03
**Confidence:** high

## Error

```
File ... cannot be loaded because running scripts is disabled on this system.
CategoryInfo: SecurityError
FullyQualifiedErrorId: UnauthorizedAccess
```

## Cause

Windows PowerShell has script execution disabled by default for security.

## Solutions

### Option 1: Avoid PowerShell in .bat files

Instead of:
```batch
powershell -Command "(Get-Content 'file.txt') -replace 'old', 'new' | Set-Content 'file.txt'"
```

Use pure batch or create file directly:
```batch
(
echo Line 1
echo Line 2
) > file.txt
```

### Option 2: Enable execution (requires admin)

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Option 3: Bypass for single command

```batch
powershell -ExecutionPolicy Bypass -Command "..."
```

## Recommendation

For .bat files that should work everywhere, avoid PowerShell entirely. Use:
- Pure batch commands
- Create files with `echo` and `>`
- Use Git Bash tools (sed, awk) if available

## Related

- [Windows batch scripting](../technologies/windows-batch.md)
