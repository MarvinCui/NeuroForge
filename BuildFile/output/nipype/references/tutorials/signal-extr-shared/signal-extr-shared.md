# How To: Signal Extr Shared

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test signal extr shared

## Prerequisites

**Required Modules:**
- `os`
- `numpy`
- `testing`
- `pipeline`
- `pytest`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign wanted = value

```python
wanted = []
```

### Step 2: Call self._test_4d_label()

```python
self._test_4d_label(wanted, self.fake_4d_label_data)
```

### Step 3: Assign volume = unknown.flatten(...)

```python
volume = self.fake_fmri_data[:, :, :, vol].flatten()
```

### Step 4: Assign wanted_row = value

```python
wanted_row = []
```

### Step 5: Call wanted.append()

```python
wanted.append(wanted_row)
```

### Step 6: Assign region = unknown.flatten(...)

```python
region = self.fake_4d_label_data[:, :, :, reg].flatten()
```

### Step 7: Call wanted_row.append()

```python
wanted_row.append((volume * region).sum() / (region * region).sum())
```


## Complete Example

```python
# Workflow
wanted = []
for vol in range(self.fake_fmri_data.shape[3]):
    volume = self.fake_fmri_data[:, :, :, vol].flatten()
    wanted_row = []
    for reg in range(self.fake_4d_label_data.shape[3]):
        region = self.fake_4d_label_data[:, :, :, reg].flatten()
        wanted_row.append((volume * region).sum() / (region * region).sum())
    wanted.append(wanted_row)
self._test_4d_label(wanted, self.fake_4d_label_data)
```

## Next Steps


---

*Source: test_nilearn.py:105 | Complexity: Intermediate | Last updated: 2026-05-18*