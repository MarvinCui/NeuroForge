# How To: Dpss Windows

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test computation of DPSS windows.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test computation of DPSS windows.'

```python
'Test computation of DPSS windows.'
```

**Verification:**
```python
assert_array_almost_equal(dpss, dpss_ni)
```

### Step 2: Assign ni = pytest.importorskip(...)

```python
ni = pytest.importorskip('nitime')
```

**Verification:**
```python
assert_array_almost_equal(eigs, eigs_ni)
```

### Step 3: Assign N = 1000

```python
N = 1000
```

**Verification:**
```python
assert_array_almost_equal(dpss, dpss_ni)
```

### Step 4: Assign half_nbw = 4

```python
half_nbw = 4
```

**Verification:**
```python
assert_array_almost_equal(eigs, eigs_ni)
```

### Step 5: Assign Kmax = int(...)

```python
Kmax = int(2 * half_nbw)
```

### Step 6: Assign unknown = dpss_windows(...)

```python
dpss, eigs = dpss_windows(N, half_nbw, Kmax, low_bias=False)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(dpss, dpss_ni)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(eigs, eigs_ni)
```

### Step 9: Assign unknown = dpss_windows(...)

```python
dpss, eigs = dpss_windows(N, half_nbw, Kmax, low_bias=False)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(dpss, dpss_ni)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(eigs, eigs_ni)
```

### Step 12: Assign unknown = ni.algorithms.dpss_windows(...)

```python
dpss_ni, eigs_ni = ni.algorithms.dpss_windows(N, half_nbw, Kmax)
```

### Step 13: Assign unknown = ni.algorithms.dpss_windows(...)

```python
dpss_ni, eigs_ni = ni.algorithms.dpss_windows(N, half_nbw, Kmax)
```


## Complete Example

```python
# Workflow
'Test computation of DPSS windows.'
ni = pytest.importorskip('nitime')
N = 1000
half_nbw = 4
Kmax = int(2 * half_nbw)
dpss, eigs = dpss_windows(N, half_nbw, Kmax, low_bias=False)
with _record_warnings():
    dpss_ni, eigs_ni = ni.algorithms.dpss_windows(N, half_nbw, Kmax)
assert_array_almost_equal(dpss, dpss_ni)
assert_array_almost_equal(eigs, eigs_ni)
dpss, eigs = dpss_windows(N, half_nbw, Kmax, low_bias=False)
with _record_warnings():
    dpss_ni, eigs_ni = ni.algorithms.dpss_windows(N, half_nbw, Kmax)
assert_array_almost_equal(dpss, dpss_ni)
assert_array_almost_equal(eigs, eigs_ni)
```

## Next Steps


---

*Source: test_multitaper.py:14 | Complexity: Advanced | Last updated: 2026-05-18*