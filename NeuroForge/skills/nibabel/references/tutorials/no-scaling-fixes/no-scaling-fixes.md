# How To: No Scaling Fixes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test no scaling fixes

## Prerequisites

**Required Modules:**
- `itertools`
- `logging`
- `os`
- `pickle`
- `re`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `_compression`
- `analyze`
- `arraywriters`
- `casting`
- `nifti1`
- `spatialimages`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign HC = value

```python
HC = self.header_class
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

### Step 3: Assign has_inter = value

```python
has_inter = HC.has_data_intercept
```

### Step 4: Assign slopes = value

```python
slopes = (1, 0, np.nan, np.inf, -np.inf)
```

### Step 5: Assign inters = value

```python
inters = (0, np.nan, np.inf, -np.inf) if has_inter else (0,)
```

### Step 6: Assign unknown = slope

```python
hdr['scl_slope'] = slope
```

### Step 7: Call self.assert_no_log_err()

```python
self.assert_no_log_err(hdr)
```

### Step 8: Assign unknown = inter

```python
hdr['scl_inter'] = inter
```


## Complete Example

```python
# Workflow
HC = self.header_class
if not HC.has_data_slope:
    return
hdr = HC()
has_inter = HC.has_data_intercept
slopes = (1, 0, np.nan, np.inf, -np.inf)
inters = (0, np.nan, np.inf, -np.inf) if has_inter else (0,)
for slope, inter in itertools.product(slopes, inters):
    hdr['scl_slope'] = slope
    if has_inter:
        hdr['scl_inter'] = inter
    self.assert_no_log_err(hdr)
```

## Next Steps


---

*Source: test_analyze.py:198 | Complexity: Advanced | Last updated: 2026-05-18*