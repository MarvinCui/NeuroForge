# How To: Pd As Tensor Variable Multiindex

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test pd as tensor variable multiindex

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pandas`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.sparse`
- `pytensor`
- `pytensor.compile`
- `pytensor.compile.builders`
- `pytensor.graph.basic`
- `pytensor.link.vm`
- `pytensor.tensor.subtensor`
- `pymc`
- `pymc.data`
- `pymc.distributions.dist_math`
- `pymc.distributions.distribution`
- `pymc.exceptions`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.vartypes`
- `cloudpickle`


## Step-by-Step Guide

### Step 1: Assign tuples = value

```python
tuples = [('L', 'Q'), ('L', 'I'), ('O', 'L'), ('O', 'I')]
```

**Verification:**
```python
assert isinstance(df.index, pd.MultiIndex)
```

### Step 2: Assign index = pd.MultiIndex.from_tuples(...)

```python
index = pd.MultiIndex.from_tuples(tuples, names=['Id1', 'Id2'])
```

### Step 3: Assign df = pd.DataFrame(...)

```python
df = pd.DataFrame({'A': [12.0, 80.0, 30.0, 20.0], 'B': [120.0, 700.0, 30.0, 20.0]}, index=index)
```

### Step 4: Assign np_array = value

```python
np_array = np.array([[12.0, 80.0, 30.0, 20.0], [120.0, 700.0, 30.0, 20.0]]).T
```

**Verification:**
```python
assert isinstance(df.index, pd.MultiIndex)
```

### Step 5: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(pt.as_tensor_variable(df).eval(), np_array)
```


## Complete Example

```python
# Workflow
tuples = [('L', 'Q'), ('L', 'I'), ('O', 'L'), ('O', 'I')]
index = pd.MultiIndex.from_tuples(tuples, names=['Id1', 'Id2'])
df = pd.DataFrame({'A': [12.0, 80.0, 30.0, 20.0], 'B': [120.0, 700.0, 30.0, 20.0]}, index=index)
np_array = np.array([[12.0, 80.0, 30.0, 20.0], [120.0, 700.0, 30.0, 20.0]]).T
assert isinstance(df.index, pd.MultiIndex)
np.testing.assert_array_equal(pt.as_tensor_variable(df).eval(), np_array)
```

## Next Steps


---

*Source: test_pytensorf.py:78 | Complexity: Intermediate | Last updated: 2026-05-18*