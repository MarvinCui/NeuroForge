# How To: Overlap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test overlap

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nipype.testing`
- `numpy`
- `nipype.algorithms.metrics`
- `numpy.testing`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign in1 = example_data(...)

```python
in1 = example_data('segmentation0.nii.gz')
```

### Step 2: Assign in2 = example_data(...)

```python
in2 = example_data('segmentation1.nii.gz')
```

### Step 3: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 4: Assign overlap = Overlap(...)

```python
overlap = Overlap()
```

### Step 5: Assign overlap.inputs.volume1 = in1

```python
overlap.inputs.volume1 = in1
```

### Step 6: Assign overlap.inputs.volume2 = in1

```python
overlap.inputs.volume2 = in1
```

### Step 7: Assign res = overlap.run(...)

```python
res = overlap.run()
```

### Step 8: Call check_close()

```python
check_close(res.outputs.jaccard, 1.0)
```

### Step 9: Assign overlap = Overlap(...)

```python
overlap = Overlap()
```

### Step 10: Assign overlap.inputs.volume1 = in1

```python
overlap.inputs.volume1 = in1
```

### Step 11: Assign overlap.inputs.volume2 = in2

```python
overlap.inputs.volume2 = in2
```

### Step 12: Assign res = overlap.run(...)

```python
res = overlap.run()
```

### Step 13: Call check_close()

```python
check_close(res.outputs.jaccard, 0.99705)
```

### Step 14: Assign overlap = Overlap(...)

```python
overlap = Overlap()
```

### Step 15: Assign overlap.inputs.volume1 = in1

```python
overlap.inputs.volume1 = in1
```

### Step 16: Assign overlap.inputs.volume2 = in2

```python
overlap.inputs.volume2 = in2
```

### Step 17: Assign overlap.inputs.vol_units = 'mm'

```python
overlap.inputs.vol_units = 'mm'
```

### Step 18: Assign res = overlap.run(...)

```python
res = overlap.run()
```

### Step 19: Call check_close()

```python
check_close(res.outputs.jaccard, 0.99705)
```

### Step 20: Call check_close()

```python
check_close(res.outputs.roi_voldiff, np.array([0.0063086, -0.0025506, 0.0]))
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
from nipype.algorithms.metrics import Overlap

def check_close(val1, val2):
    import numpy.testing as npt
    return npt.assert_almost_equal(val1, val2, decimal=3)
in1 = example_data('segmentation0.nii.gz')
in2 = example_data('segmentation1.nii.gz')
tmpdir.chdir()
overlap = Overlap()
overlap.inputs.volume1 = in1
overlap.inputs.volume2 = in1
res = overlap.run()
check_close(res.outputs.jaccard, 1.0)
overlap = Overlap()
overlap.inputs.volume1 = in1
overlap.inputs.volume2 = in2
res = overlap.run()
check_close(res.outputs.jaccard, 0.99705)
overlap = Overlap()
overlap.inputs.volume1 = in1
overlap.inputs.volume2 = in2
overlap.inputs.vol_units = 'mm'
res = overlap.run()
check_close(res.outputs.jaccard, 0.99705)
check_close(res.outputs.roi_voldiff, np.array([0.0063086, -0.0025506, 0.0]))
```

## Next Steps


---

*Source: test_Overlap.py:11 | Complexity: Advanced | Last updated: 2026-05-18*