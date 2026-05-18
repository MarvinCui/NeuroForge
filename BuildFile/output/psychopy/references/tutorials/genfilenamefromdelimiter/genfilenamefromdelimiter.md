# How To: Genfilenamefromdelimiter

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test genFilenameFromDelimiter

## Prerequisites

**Required Modules:**
- `shutil`
- `os`
- `sys`
- `json`
- `pickle`
- `pytest`
- `tempfile`
- `psychopy.tools.filetools`


## Step-by-Step Guide

### Step 1: Assign base_name = 'testfile'

```python
base_name = 'testfile'
```

**Verification:**
```python
assert extension == correct_extension
```

### Step 2: Assign delims = value

```python
delims = [',', '\t', None]
```

### Step 3: Assign correct_extensions = value

```python
correct_extensions = ['.csv', '.tsv', '.txt']
```

### Step 4: Assign filename = genFilenameFromDelimiter(...)

```python
filename = genFilenameFromDelimiter(base_name, delim)
```

### Step 5: Assign extension = value

```python
extension = os.path.splitext(filename)[1]
```

**Verification:**
```python
assert extension == correct_extension
```


## Complete Example

```python
# Workflow
base_name = 'testfile'
delims = [',', '\t', None]
correct_extensions = ['.csv', '.tsv', '.txt']
for delim, correct_extension in zip(delims, correct_extensions):
    filename = genFilenameFromDelimiter(base_name, delim)
    extension = os.path.splitext(filename)[1]
    assert extension == correct_extension
```

## Next Steps


---

*Source: test_filetools.py:29 | Complexity: Intermediate | Last updated: 2026-05-18*