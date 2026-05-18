# How To: Prog List Helps

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test prog list helps

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `shutil`
- `subprocess`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign programs = _get_programs(...)

```python
programs = _get_programs(AFNI_ROOT)
```

### Step 2: Assign not_found = value

```python
not_found = []
```

### Step 3: Assign no_success = value

```python
no_success = []
```

### Step 4: Assign process = subprocess.run(...)

```python
process = subprocess.run([prog, '-help'], stderr=subprocess.PIPE, stdout=subprocess.DEVNULL)
```

### Step 5: Call print()

```python
print('PROGRAMS NOT FOUND:')
```

### Step 6: Call print()

```python
print('    ' + '\n    '.join(not_found))
```

### Step 7: Call print()

```python
print('PROGRAMS THAT FAILED:')
```

### Step 8: Call print()

```python
print('    ' + '\n    '.join(no_success))
```

### Step 9: Call not_found.append()

```python
not_found.append(prog)
```

### Step 10: Assign msg = unknown.format(...)

```python
msg = 'return code {}'.format(process.returncode)
```

### Step 11: Call no_success.append()

```python
no_success.append('{} ({})'.format(prog, msg))
```

### Step 12: Assign msg = unknown.decode(...)

```python
msg = process.stderr.splitlines()[-1].decode()
```


## Complete Example

```python
# Workflow
programs = _get_programs(AFNI_ROOT)
not_found = []
no_success = []
for prog in programs:
    if prog in SHOULD_NOT_BE_EXECUTABLE or prog in KNOWN_BROKEN_HELP:
        continue
    if shutil.which(prog) is None:
        not_found.append(prog)
        continue
    process = subprocess.run([prog, '-help'], stderr=subprocess.PIPE, stdout=subprocess.DEVNULL)
    if process.returncode != 0:
        msg = 'return code {}'.format(process.returncode)
        if process.stderr:
            msg = process.stderr.splitlines()[-1].decode()
        no_success.append('{} ({})'.format(prog, msg))
if not_found:
    print('PROGRAMS NOT FOUND:')
    print('    ' + '\n    '.join(not_found))
if no_success:
    print('PROGRAMS THAT FAILED:')
    print('    ' + '\n    '.join(no_success))
if not_found or no_success:
    raise ValueError('Not all help messages are running correctly')
```

## Next Steps


---

*Source: test_help_messages.py:39 | Complexity: Advanced | Last updated: 2026-05-18*