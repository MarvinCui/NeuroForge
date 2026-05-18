# How To: Json With Encoding

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test json with encoding

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

### Step 1: Assign unknown = mkstemp(...)

```python
_, path_0 = mkstemp(dir=self.tmp_dir, suffix='.json')
```

**Verification:**
```python
assert test_data == fromFile(path_0, encoding=encoding_0)
```

### Step 2: Assign unknown = mkstemp(...)

```python
_, path_1 = mkstemp(dir=self.tmp_dir, suffix='.json')
```

**Verification:**
```python
assert test_data == fromFile(path_1, encoding=encoding_1)
```

### Step 3: Assign encoding_0 = 'utf-8'

```python
encoding_0 = 'utf-8'
```

### Step 4: Assign encoding_1 = 'utf-8-sig'

```python
encoding_1 = 'utf-8-sig'
```

### Step 5: Assign test_data = 'Test'

```python
test_data = 'Test'
```

**Verification:**
```python
assert test_data == fromFile(path_0, encoding=encoding_0)
```

### Step 6: Call json.dump()

```python
json.dump(test_data, f)
```

### Step 7: Call json.dump()

```python
json.dump(test_data, f)
```


## Complete Example

```python
# Workflow
_, path_0 = mkstemp(dir=self.tmp_dir, suffix='.json')
_, path_1 = mkstemp(dir=self.tmp_dir, suffix='.json')
encoding_0 = 'utf-8'
encoding_1 = 'utf-8-sig'
test_data = 'Test'
with open(path_0, 'w', encoding=encoding_0) as f:
    json.dump(test_data, f)
with open(path_1, 'w', encoding=encoding_1) as f:
    json.dump(test_data, f)
assert test_data == fromFile(path_0, encoding=encoding_0)
assert test_data == fromFile(path_1, encoding=encoding_1)
```

## Next Steps


---

*Source: test_filetools.py:77 | Complexity: Intermediate | Last updated: 2026-05-18*