# How To: Round Trip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test round trip

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `numpy.testing`
- `arraywriters`
- `casting`
- `spatialimages`


## Step-by-Step Guide

### Step 1: Assign scaling_type = value

```python
scaling_type = np.float32
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(20111121)
```

### Step 3: Assign N = 10000

```python
N = 10000
```

### Step 4: Assign sd_10s = range(...)

```python
sd_10s = range(-20, 51, 5)
```

### Step 5: Assign iuint_types = value

```python
iuint_types = sctypes['int'] + sctypes['uint']
```

### Step 6: Assign nifti_supported = supported_np_types(...)

```python
nifti_supported = supported_np_types(Nifti1Header())
```

### Step 7: Assign iuint_types = value

```python
iuint_types = [t for t in iuint_types if t in nifti_supported]
```

### Step 8: Assign f_types = value

```python
f_types = [np.float32, np.float64]
```

### Step 9: Assign sd = value

```python
sd = 10.0 ** sd_10
```

### Step 10: Assign V_in = rng.normal(...)

```python
V_in = rng.normal(0, sd, size=(N, 1))
```

### Step 11: Assign info = np.iinfo(...)

```python
info = np.iinfo(in_type)
```

### Step 12: Assign unknown = value

```python
mn, mx = (info.min, info.max)
```

### Step 13: Assign type_range = value

```python
type_range = mx - mn
```

### Step 14: Assign center = value

```python
center = type_range / 2.0 + mn
```

### Step 15: Assign width = value

```python
width = type_range * float(sd)
```

### Step 16: Assign V_in = rng.normal(...)

```python
V_in = rng.normal(center, width, size=(N, 1))
```

### Step 17: Call check_arr()

```python
check_arr(sd_10, V_in, in_type, out_type, scaling_type)
```

### Step 18: Call check_arr()

```python
check_arr(sd, V_in, in_type, out_type, scaling_type)
```


## Complete Example

```python
# Workflow
scaling_type = np.float32
rng = np.random.RandomState(20111121)
N = 10000
sd_10s = range(-20, 51, 5)
iuint_types = sctypes['int'] + sctypes['uint']
nifti_supported = supported_np_types(Nifti1Header())
iuint_types = [t for t in iuint_types if t in nifti_supported]
f_types = [np.float32, np.float64]
for sd_10 in sd_10s:
    sd = 10.0 ** sd_10
    V_in = rng.normal(0, sd, size=(N, 1))
    for in_type in f_types:
        for out_type in iuint_types:
            check_arr(sd_10, V_in, in_type, out_type, scaling_type)
for sd in np.linspace(0.05, 0.5, 5):
    for in_type in iuint_types:
        info = np.iinfo(in_type)
        mn, mx = (info.min, info.max)
        type_range = mx - mn
        center = type_range / 2.0 + mn
        width = type_range * float(sd)
        V_in = rng.normal(center, width, size=(N, 1))
        for out_type in iuint_types:
            check_arr(sd, V_in, in_type, out_type, scaling_type)
```

## Next Steps


---

*Source: test_round_trip.py:100 | Complexity: Advanced | Last updated: 2026-05-18*