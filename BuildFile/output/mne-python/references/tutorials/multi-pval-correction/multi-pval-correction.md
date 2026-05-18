# How To: Multi Pval Correction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test pval correction for multi comparison (FDR and Bonferroni).

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne.stats`


## Step-by-Step Guide

### Step 1: 'Test pval correction for multi comparison (FDR and Bonferroni).'

```python
'Test pval correction for multi comparison (FDR and Bonferroni).'
```

**Verification:**
```python
assert pval_bonferroni.ndim == 2
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert reject_bonferroni.ndim == 2
```

### Step 3: Assign X = rng.randn(...)

```python
X = rng.randn(10, 1000, 10)
```

**Verification:**
```python
assert_allclose(pval_bonferroni, (pval * 10000).clip(max=1))
```

### Step 4: Assign alpha = 0.05

```python
alpha = 0.05
```

**Verification:**
```python
assert_array_equal(reject_bonferroni, reject_expected)
```

### Step 5: Assign unknown = stats.ttest_1samp(...)

```python
T, pval = stats.ttest_1samp(X, 0)
```

**Verification:**
```python
assert_almost_equal(fwer, alpha, 1)
```

### Step 6: Assign n_samples = value

```python
n_samples = X.shape[0]
```

**Verification:**
```python
assert pval_fdr.ndim == 2
```

### Step 7: Assign n_tests = value

```python
n_tests = X.size / n_samples
```

**Verification:**
```python
assert reject_fdr.ndim == 2
```

### Step 8: Assign thresh_uncorrected = stats.t.ppf(...)

```python
thresh_uncorrected = stats.t.ppf(1.0 - alpha, n_samples - 1)
```

**Verification:**
```python
assert 0 <= reject_fdr.sum() - 50 <= 50 * 1.05
```

### Step 9: Assign unknown = bonferroni_correction(...)

```python
reject_bonferroni, pval_bonferroni = bonferroni_correction(pval, alpha)
```

**Verification:**
```python
assert thresh_uncorrected <= thresh_fdr <= thresh_bonferroni
```

### Step 10: Assign thresh_bonferroni = stats.t.ppf(...)

```python
thresh_bonferroni = stats.t.ppf(1.0 - alpha / n_tests, n_samples - 1)
```

**Verification:**
```python
assert np.all(fdr_correction(pval, alpha=0)[0] == 0)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(pval_bonferroni, (pval * 10000).clip(max=1))
```

**Verification:**
```python
assert 0 <= reject_fdr.sum() - 50 <= 50 * 1.05
```

### Step 12: Assign reject_expected = value

```python
reject_expected = pval_bonferroni < alpha
```

**Verification:**
```python
assert thresh_uncorrected <= thresh_fdr <= thresh_bonferroni
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(reject_bonferroni, reject_expected)
```

### Step 14: Assign fwer = np.mean(...)

```python
fwer = np.mean(reject_bonferroni)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(fwer, alpha, 1)
```

### Step 16: Assign unknown = fdr_correction(...)

```python
reject_fdr, pval_fdr = fdr_correction(pval, alpha=alpha, method='indep')
```

**Verification:**
```python
assert pval_fdr.ndim == 2
```

### Step 17: Assign thresh_fdr = np.min(...)

```python
thresh_fdr = np.min(np.abs(T)[reject_fdr])
```

**Verification:**
```python
assert 0 <= reject_fdr.sum() - 50 <= 50 * 1.05
```

### Step 18: Call pytest.raises()

```python
pytest.raises(ValueError, fdr_correction, pval, alpha, method='blah')
```

**Verification:**
```python
assert np.all(fdr_correction(pval, alpha=0)[0] == 0)
```

### Step 19: Assign unknown = fdr_correction(...)

```python
reject_fdr, pval_fdr = fdr_correction(pval, alpha=alpha, method='negcorr')
```

### Step 20: Assign thresh_fdr = np.min(...)

```python
thresh_fdr = np.min(np.abs(T)[reject_fdr])
```

**Verification:**
```python
assert 0 <= reject_fdr.sum() - 50 <= 50 * 1.05
```


## Complete Example

```python
# Workflow
'Test pval correction for multi comparison (FDR and Bonferroni).'
rng = np.random.RandomState(0)
X = rng.randn(10, 1000, 10)
X[:, :50, 0] += 4.0
alpha = 0.05
T, pval = stats.ttest_1samp(X, 0)
n_samples = X.shape[0]
n_tests = X.size / n_samples
thresh_uncorrected = stats.t.ppf(1.0 - alpha, n_samples - 1)
reject_bonferroni, pval_bonferroni = bonferroni_correction(pval, alpha)
thresh_bonferroni = stats.t.ppf(1.0 - alpha / n_tests, n_samples - 1)
assert pval_bonferroni.ndim == 2
assert reject_bonferroni.ndim == 2
assert_allclose(pval_bonferroni, (pval * 10000).clip(max=1))
reject_expected = pval_bonferroni < alpha
assert_array_equal(reject_bonferroni, reject_expected)
fwer = np.mean(reject_bonferroni)
assert_almost_equal(fwer, alpha, 1)
reject_fdr, pval_fdr = fdr_correction(pval, alpha=alpha, method='indep')
assert pval_fdr.ndim == 2
assert reject_fdr.ndim == 2
thresh_fdr = np.min(np.abs(T)[reject_fdr])
assert 0 <= reject_fdr.sum() - 50 <= 50 * 1.05
assert thresh_uncorrected <= thresh_fdr <= thresh_bonferroni
pytest.raises(ValueError, fdr_correction, pval, alpha, method='blah')
assert np.all(fdr_correction(pval, alpha=0)[0] == 0)
reject_fdr, pval_fdr = fdr_correction(pval, alpha=alpha, method='negcorr')
thresh_fdr = np.min(np.abs(T)[reject_fdr])
assert 0 <= reject_fdr.sum() - 50 <= 50 * 1.05
assert thresh_uncorrected <= thresh_fdr <= thresh_bonferroni
```

## Next Steps


---

*Source: test_multi_comp.py:20 | Complexity: Advanced | Last updated: 2026-05-18*