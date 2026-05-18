# How To: Bounds X0

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test to check if setting bounds for signal where initial value is
higher than subsequent values works.

These values are from the IVIM dataset which can be obtained by using
the `read_ivim` function from dipy.data.fetcher. These are values from
the voxel [160, 98, 33] which can be obtained by :

.. code-block:: python

   from dipy.data.fetcher import read_ivim
   img, gtab = read_ivim()
   data = load_nifti_data(img)
   signal = data[160, 98, 33, :]

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.reconst.ivim`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: '\n    Test to check if setting bounds for signal where initial value is\n    higher than subsequent values works.\n\n    These values are from the IVIM dataset which can be obtained by using\n    the `read_ivim` function from dipy.data.fetcher. These are values from\n    the voxel [160, 98, 33] which can be obtained by :\n\n    .. code-block:: python\n\n       from dipy.data.fetcher import read_ivim\n       img, gtab = read_ivim()\n       data = load_nifti_data(img)\n       signal = data[160, 98, 33, :]\n\n    '

```python
'\n    Test to check if setting bounds for signal where initial value is\n    higher than subsequent values works.\n\n    These values are from the IVIM dataset which can be obtained by using\n    the `read_ivim` function from dipy.data.fetcher. These are values from\n    the voxel [160, 98, 33] which can be obtained by :\n\n    .. code-block:: python\n\n       from dipy.data.fetcher import read_ivim\n       img, gtab = read_ivim()\n       data = load_nifti_data(img)\n       signal = data[160, 98, 33, :]\n\n    '
```

**Verification:**
```python
assert_array_equal(est_signal.shape, test_signal.shape)
```

### Step 2: Assign x0_test = np.array(...)

```python
x0_test = np.array([1.0, 0.13, 0.001, 0.0001])
```

### Step 3: Assign test_signal = ivim_prediction(...)

```python
test_signal = ivim_prediction(x0_test, gtab)
```

### Step 4: Assign ivim_fit = ivim_model_trr.fit(...)

```python
ivim_fit = ivim_model_trr.fit(test_signal)
```

### Step 5: Assign est_signal = ivim_fit.predict(...)

```python
est_signal = ivim_fit.predict(gtab)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(est_signal.shape, test_signal.shape)
```


## Complete Example

```python
# Workflow
'\n    Test to check if setting bounds for signal where initial value is\n    higher than subsequent values works.\n\n    These values are from the IVIM dataset which can be obtained by using\n    the `read_ivim` function from dipy.data.fetcher. These are values from\n    the voxel [160, 98, 33] which can be obtained by :\n\n    .. code-block:: python\n\n       from dipy.data.fetcher import read_ivim\n       img, gtab = read_ivim()\n       data = load_nifti_data(img)\n       signal = data[160, 98, 33, :]\n\n    '
x0_test = np.array([1.0, 0.13, 0.001, 0.0001])
test_signal = ivim_prediction(x0_test, gtab)
ivim_fit = ivim_model_trr.fit(test_signal)
est_signal = ivim_fit.predict(gtab)
assert_array_equal(est_signal.shape, test_signal.shape)
```

## Next Steps


---

*Source: test_ivim.py:372 | Complexity: Intermediate | Last updated: 2026-05-18*