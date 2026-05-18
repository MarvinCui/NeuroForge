# How To: Ch Names Comma

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that channel names containing commas are properly read.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `configparser`
- `datetime`
- `inspect`
- `re`
- `shutil`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test that channel names containing commas are properly read.'

```python
'Test that channel names containing commas are properly read.'
```

**Verification:**
```python
assert nperformed_replacements == len(replace_dict)
```

### Step 2: Assign replace_dict = value

```python
replace_dict = {'^Ch4=F4,': 'Ch4=F4\\\\1foo,', '^4\\s\\s\\s\\s\\sF4': '4     F4,foo '}
```

**Verification:**
```python
assert 'F4,foo' in raw.ch_names
```

### Step 3: Assign comma_vhdr = value

```python
comma_vhdr = tmp_path / 'test.vhdr'
```

### Step 4: Assign new_lines = value

```python
new_lines = []
```

### Step 5: Assign nperformed_replacements = 0

```python
nperformed_replacements = 0
```

**Verification:**
```python
assert nperformed_replacements == len(replace_dict)
```

### Step 6: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(comma_vhdr)
```

**Verification:**
```python
assert 'F4,foo' in raw.ch_names
```

### Step 7: Call shutil.copyfile()

```python
shutil.copyfile(src, tmp_path / dest)
```

### Step 8: Assign lines = fin.readlines(...)

```python
lines = fin.readlines()
```

### Step 9: Call fout.writelines()

```python
fout.writelines(new_lines)
```

### Step 10: Assign match = re.search(...)

```python
match = re.search(to_replace, line)
```

### Step 11: Call new_lines.append()

```python
new_lines.append(line)
```

### Step 12: Assign new = re.sub(...)

```python
new = re.sub(to_replace, replacement, line)
```

### Step 13: Call new_lines.append()

```python
new_lines.append(new)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test that channel names containing commas are properly read.'
replace_dict = {'^Ch4=F4,': 'Ch4=F4\\\\1foo,', '^4\\s\\s\\s\\s\\sF4': '4     F4,foo '}
for src, dest in zip((vhdr_path, vmrk_path, eeg_path), ('test.vhdr', 'test.vmrk', 'test.eeg')):
    shutil.copyfile(src, tmp_path / dest)
comma_vhdr = tmp_path / 'test.vhdr'
with open(comma_vhdr) as fin:
    lines = fin.readlines()
new_lines = []
nperformed_replacements = 0
for line in lines:
    for to_replace, replacement in replace_dict.items():
        match = re.search(to_replace, line)
        if match is not None:
            new = re.sub(to_replace, replacement, line)
            new_lines.append(new)
            nperformed_replacements += 1
            break
    else:
        new_lines.append(line)
assert nperformed_replacements == len(replace_dict)
with open(comma_vhdr, 'w') as fout:
    fout.writelines(new_lines)
raw = read_raw_brainvision(comma_vhdr)
assert 'F4,foo' in raw.ch_names
```

## Next Steps


---

*Source: test_brainvision.py:318 | Complexity: Advanced | Last updated: 2026-05-18*