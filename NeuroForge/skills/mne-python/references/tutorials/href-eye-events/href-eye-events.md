# How To: Href Eye Events

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Parsing file where Eye Event Data option was set to 'HREF'.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.eyelink._utils`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: "Test Parsing file where Eye Event Data option was set to 'HREF'."

```python
"Test Parsing file where Eye Event Data option was set to 'HREF'."
```

**Verification:**
```python
assert 'saccade' in raw.annotations.description
```

### Step 2: Assign out_file = value

```python
out_file = tmp_path / 'tmp_eyelink.asc'
```

**Verification:**
```python
assert 'fixation' in raw.annotations.description
```

### Step 3: Assign lines = fname_href.read_text.splitlines(...)

```python
lines = fname_href.read_text('utf-8').splitlines()
```

### Step 4: Call out_file.write_text()

```python
out_file.write_text('\n'.join(lines), encoding='utf-8')
```

### Step 5: Assign raw = read_raw_eyelink(...)

```python
raw = read_raw_eyelink(out_file)
```

**Verification:**
```python
assert 'saccade' in raw.annotations.description
```

### Step 6: Assign tokens = line.split(...)

```python
tokens = line.split()
```

### Step 7: Assign new_line = value

```python
new_line = '\t'.join(tokens) + '\n'
```

### Step 8: Assign unknown = new_line

```python
lines[li] = new_line
```

### Step 9: Assign href_sacc_vals = value

```python
href_sacc_vals = ['9999', '9999', '9999', '9999', '99.99', '999']
```

### Step 10: Assign unknown = href_sacc_vals

```python
tokens[5:5] = href_sacc_vals
```

### Step 11: Assign tokens = line.split(...)

```python
tokens = line.split()
```

### Step 12: Assign href_fix_vals = value

```python
href_fix_vals = ['9999.9', '9999.9', '999']
```

### Step 13: Assign unknown = href_fix_vals

```python
tokens[5:3] = href_fix_vals
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
"Test Parsing file where Eye Event Data option was set to 'HREF'."
out_file = tmp_path / 'tmp_eyelink.asc'
lines = fname_href.read_text('utf-8').splitlines()
for li, line in enumerate(lines):
    if not line.startswith(('ESACC', 'EFIX')):
        continue
    tokens = line.split()
    if line.startswith('ESACC'):
        href_sacc_vals = ['9999', '9999', '9999', '9999', '99.99', '999']
        tokens[5:5] = href_sacc_vals
    elif line.startswith('EFIX'):
        tokens = line.split()
        href_fix_vals = ['9999.9', '9999.9', '999']
        tokens[5:3] = href_fix_vals
    new_line = '\t'.join(tokens) + '\n'
    lines[li] = new_line
out_file.write_text('\n'.join(lines), encoding='utf-8')
raw = read_raw_eyelink(out_file)
assert 'saccade' in raw.annotations.description
assert 'fixation' in raw.annotations.description
```

## Next Steps


---

*Source: test_eyelink.py:503 | Complexity: Advanced | Last updated: 2026-05-18*