# How To: Read Vectorview Selection

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading of Neuromag Vector View channel selections.

## Prerequisites

**Required Modules:**
- `pathlib`
- `pytest`
- `mne`
- `mne.io`


## Step-by-Step Guide

### Step 1: 'Test reading of Neuromag Vector View channel selections.'

```python
'Test reading of Neuromag Vector View channel selections.'
```

**Verification:**
```python
assert ch_names[i] in sel
```

### Step 2: Assign ch_names = value

```python
ch_names = ['MEG 2211', 'MEG 0223', 'MEG 1312', 'MEG 0412', 'MEG 1043', 'MEG 2042', 'MEG 2032', 'MEG 0522', 'MEG 1031']
```

**Verification:**
```python
assert sel == sel_info
```

### Step 3: Assign sel_names = value

```python
sel_names = ['Vertex', 'Left-temporal', 'Right-temporal', 'Left-parietal', 'Right-parietal', 'Left-occipital', 'Right-occipital', 'Left-frontal', 'Right-frontal']
```

**Verification:**
```python
assert len(all_ch) == len(left) + len(right)
```

### Step 4: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert len(set(left).intersection(set(right))) == 0
```

### Step 5: Assign all_ch = read_vectorview_selection(...)

```python
all_ch = read_vectorview_selection(['L', 'R'])
```

**Verification:**
```python
assert len(set(frontal).intersection(set(occipital))) == 0
```

### Step 6: Assign left = read_vectorview_selection(...)

```python
left = read_vectorview_selection('L')
```

**Verification:**
```python
assert ch_names_new[i] in sel
```

### Step 7: Assign right = read_vectorview_selection(...)

```python
right = read_vectorview_selection('R')
```

**Verification:**
```python
assert len(all_ch) == len(left) + len(right)
```

### Step 8: Assign frontal = read_vectorview_selection(...)

```python
frontal = read_vectorview_selection('frontal')
```

### Step 9: Assign occipital = read_vectorview_selection(...)

```python
occipital = read_vectorview_selection('Right-occipital')
```

**Verification:**
```python
assert len(set(frontal).intersection(set(occipital))) == 0
```

### Step 10: Assign ch_names_new = value

```python
ch_names_new = [ch.replace(' ', '') for ch in ch_names]
```

### Step 11: Assign raw_new = read_raw_fif(...)

```python
raw_new = read_raw_fif(raw_new_fname)
```

### Step 12: Assign sel = read_vectorview_selection(...)

```python
sel = read_vectorview_selection(name)
```

**Verification:**
```python
assert ch_names[i] in sel
```

### Step 13: Assign sel_info = read_vectorview_selection(...)

```python
sel_info = read_vectorview_selection(name, info=raw.info)
```

**Verification:**
```python
assert sel == sel_info
```

### Step 14: Assign sel = read_vectorview_selection(...)

```python
sel = read_vectorview_selection(name, info=raw_new.info)
```

**Verification:**
```python
assert ch_names_new[i] in sel
```

### Step 15: Call read_vectorview_selection()

```python
read_vectorview_selection(name, info='foo')
```


## Complete Example

```python
# Workflow
'Test reading of Neuromag Vector View channel selections.'
ch_names = ['MEG 2211', 'MEG 0223', 'MEG 1312', 'MEG 0412', 'MEG 1043', 'MEG 2042', 'MEG 2032', 'MEG 0522', 'MEG 1031']
sel_names = ['Vertex', 'Left-temporal', 'Right-temporal', 'Left-parietal', 'Right-parietal', 'Left-occipital', 'Right-occipital', 'Left-frontal', 'Right-frontal']
raw = read_raw_fif(raw_fname)
for i, name in enumerate(sel_names):
    sel = read_vectorview_selection(name)
    assert ch_names[i] in sel
    sel_info = read_vectorview_selection(name, info=raw.info)
    assert sel == sel_info
all_ch = read_vectorview_selection(['L', 'R'])
left = read_vectorview_selection('L')
right = read_vectorview_selection('R')
assert len(all_ch) == len(left) + len(right)
assert len(set(left).intersection(set(right))) == 0
frontal = read_vectorview_selection('frontal')
occipital = read_vectorview_selection('Right-occipital')
assert len(set(frontal).intersection(set(occipital))) == 0
ch_names_new = [ch.replace(' ', '') for ch in ch_names]
raw_new = read_raw_fif(raw_new_fname)
for i, name in enumerate(sel_names):
    sel = read_vectorview_selection(name, info=raw_new.info)
    assert ch_names_new[i] in sel
with pytest.raises(TypeError, match='must be an instance of Info or None'):
    read_vectorview_selection(name, info='foo')
```

## Next Steps


---

*Source: test_read_vectorview_selection.py:17 | Complexity: Advanced | Last updated: 2026-05-18*