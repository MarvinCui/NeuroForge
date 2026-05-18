# How To: Streamline Signal

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test streamline signal

## Prerequisites

**Required Modules:**
- `os.path`
- `nibabel`
- `numpy`
- `numpy.testing`
- `scipy.linalg`
- `dipy.core.gradients`
- `dipy.core.optimize`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.tracking.life`


## Step-by-Step Guide

### Step 1: Assign unknown = dpd.get_fnames(...)

```python
data_file, bval_file, bvec_file = dpd.get_fnames(name='small_64D')
```

### Step 2: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(bval_file, bvecs=bvec_file)
```

### Step 3: Assign evals = value

```python
evals = [0.0015, 0.0005, 0.0005]
```

### Step 4: Assign streamline1 = value

```python
streamline1 = [[[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]]
```

### Step 5: [life.streamline_signal(s, gtab, evals=evals) for s in streamline1]

```python
[life.streamline_signal(s, gtab, evals=evals) for s in streamline1]
```

### Step 6: Assign streamline2 = value

```python
streamline2 = [[[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]]]
```

### Step 7: [life.streamline_signal(s, gtab, evals=evals) for s in streamline2]

```python
[life.streamline_signal(s, gtab, evals=evals) for s in streamline2]
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(streamline2[0], streamline1[0])
```


## Complete Example

```python
# Workflow
data_file, bval_file, bvec_file = dpd.get_fnames(name='small_64D')
gtab = grad.gradient_table(bval_file, bvecs=bvec_file)
evals = [0.0015, 0.0005, 0.0005]
streamline1 = [[[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]]
[life.streamline_signal(s, gtab, evals=evals) for s in streamline1]
streamline2 = [[[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]]]
[life.streamline_signal(s, gtab, evals=evals) for s in streamline2]
npt.assert_array_equal(streamline2[0], streamline1[0])
```

## Next Steps


---

*Source: test_life.py:57 | Complexity: Advanced | Last updated: 2026-05-18*