# How To: Kmeans

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test kmeans

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `matplotlib.pyplot`
- `matplotlib.pyplot`


## Step-by-Step Guide

### Step 1: Assign X = value

```python
X = self.x[:, None]
```

### Step 2: Assign Xu = pm.gp.util.kmeans_inducing_points.flatten(...)

```python
Xu = pm.gp.util.kmeans_inducing_points(2, X).flatten()
```

### Step 3: Call npt.assert_allclose()

```python
npt.assert_allclose(np.asarray(self.centers), np.sort(Xu), rtol=0.05)
```

### Step 4: Assign X = pt.as_tensor_variable(...)

```python
X = pt.as_tensor_variable(self.x[:, None])
```

### Step 5: Assign Xu = pm.gp.util.kmeans_inducing_points.flatten(...)

```python
Xu = pm.gp.util.kmeans_inducing_points(2, X).flatten()
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(np.asarray(self.centers), np.sort(Xu), rtol=0.05)
```


## Complete Example

```python
# Workflow
X = self.x[:, None]
Xu = pm.gp.util.kmeans_inducing_points(2, X).flatten()
npt.assert_allclose(np.asarray(self.centers), np.sort(Xu), rtol=0.05)
X = pt.as_tensor_variable(self.x[:, None])
Xu = pm.gp.util.kmeans_inducing_points(2, X).flatten()
npt.assert_allclose(np.asarray(self.centers), np.sort(Xu), rtol=0.05)
```

## Next Steps


---

*Source: test_util.py:59 | Complexity: Intermediate | Last updated: 2026-05-18*