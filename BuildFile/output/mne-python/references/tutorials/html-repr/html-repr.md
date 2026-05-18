# How To: Html Repr

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test switching _repr_html_ between HTML and plain text.

## Prerequisites

**Required Modules:**
- `os`
- `subprocess`
- `sys`
- `contextlib`
- `pytest`
- `mne`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test switching _repr_html_ between HTML and plain text.'

```python
'Test switching _repr_html_ between HTML and plain text.'
```

**Verification:**
```python
assert r.startswith('<script type=')
```

### Step 2: Assign key = 'MNE_REPR_HTML'

```python
key = 'MNE_REPR_HTML'
```

**Verification:**
```python
assert r.endswith('</table>')
```

### Step 3: Assign existing_value = os.getenv(...)

```python
existing_value = os.getenv(key, None)
```

**Verification:**
```python
assert r.startswith('<pre>')
```

### Step 4: Assign unknown = 'True'

```python
os.environ[key] = 'True'
```

**Verification:**
```python
assert r.endswith('</pre>')
```

### Step 5: Assign info = mne.create_info(...)

```python
info = mne.create_info(10, 256)
```

### Step 6: Assign r = info._repr_html_(...)

```python
r = info._repr_html_()
```

**Verification:**
```python
assert r.startswith('<script type=')
```

### Step 7: Assign unknown = 'False'

```python
os.environ[key] = 'False'
```

### Step 8: Assign r = info._repr_html_(...)

```python
r = info._repr_html_()
```

**Verification:**
```python
assert r.startswith('<pre>')
```

### Step 9: Assign unknown = existing_value

```python
os.environ[key] = existing_value
```


## Complete Example

```python
# Workflow
'Test switching _repr_html_ between HTML and plain text.'
key = 'MNE_REPR_HTML'
existing_value = os.getenv(key, None)
os.environ[key] = 'True'
info = mne.create_info(10, 256)
r = info._repr_html_()
assert r.startswith('<script type=')
assert r.endswith('</table>')
os.environ[key] = 'False'
r = info._repr_html_()
assert r.startswith('<pre>')
assert r.endswith('</pre>')
del os.environ[key]
if existing_value is not None:
    os.environ[key] = existing_value
```

## Next Steps


---

*Source: test_misc.py:23 | Complexity: Advanced | Last updated: 2026-05-18*