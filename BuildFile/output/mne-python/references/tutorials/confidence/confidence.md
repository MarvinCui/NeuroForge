# How To: Confidence

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test confidence limits.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.dipole`
- `mne.io`
- `mne.proj`
- `mne.simulation`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test confidence limits.'

```python
'Test confidence limits.'
```

**Verification:**
```python
assert_allclose(dip_check.pos, dip_xfit.pos, atol=0.0005)
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname_evo_full, 'Left Auditory', baseline=(None, 0))
```

**Verification:**
```python
assert_allclose(dip_check.gof, dip_xfit.gof, atol=0.5)
```

### Step 3: Call evoked.crop.pick()

```python
evoked.crop(0.08, 0.08).pick('meg')
```

**Verification:**
```python
assert_array_equal(dip_check.nfree, dip_xfit.nfree)
```

### Step 4: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(evoked.info)
```

**Verification:**
```python
assert_allclose(dip_check.khi2, dip_xfit.khi2, rtol=0.02)
```

### Step 5: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model((0.0, 0.0, 0.04), 0.08)
```

**Verification:**
```python
assert set(dip_check.conf.keys()) == set(dip_xfit.conf.keys())
```

### Step 6: Assign dip_py = value

```python
dip_py = fit_dipole(evoked, cov, sphere)[0]
```

**Verification:**
```python
assert_allclose(dip_check.conf[key], dip_xfit.conf[key], rtol=0.15, err_msg=key)
```

### Step 7: Assign fname_test = value

```python
fname_test = tmp_path / 'temp-dip.txt'
```

### Step 8: Call dip_py.save()

```python
dip_py.save(fname_test)
```

### Step 9: Assign dip_read = read_dipole(...)

```python
dip_read = read_dipole(fname_test)
```

### Step 10: Assign dip_xfit = read_dipole(...)

```python
dip_xfit = read_dipole(fname_dip_xfit_80)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(dip_check.pos, dip_xfit.pos, atol=0.0005)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(dip_check.gof, dip_xfit.gof, atol=0.5)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(dip_check.nfree, dip_xfit.nfree)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(dip_check.khi2, dip_xfit.khi2, rtol=0.02)
```

**Verification:**
```python
assert set(dip_check.conf.keys()) == set(dip_xfit.conf.keys())
```

### Step 15: Call assert_allclose()

```python
assert_allclose(dip_check.conf[key], dip_xfit.conf[key], rtol=0.15, err_msg=key)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test confidence limits.'
evoked = read_evokeds(fname_evo_full, 'Left Auditory', baseline=(None, 0))
evoked.crop(0.08, 0.08).pick('meg')
cov = make_ad_hoc_cov(evoked.info)
sphere = make_sphere_model((0.0, 0.0, 0.04), 0.08)
dip_py = fit_dipole(evoked, cov, sphere)[0]
fname_test = tmp_path / 'temp-dip.txt'
dip_py.save(fname_test)
dip_read = read_dipole(fname_test)
with pytest.warns(RuntimeWarning, match="'noise/ft/cm', 'prob'"):
    dip_xfit = read_dipole(fname_dip_xfit_80)
for dip_check in (dip_py, dip_read):
    assert_allclose(dip_check.pos, dip_xfit.pos, atol=0.0005)
    assert_allclose(dip_check.gof, dip_xfit.gof, atol=0.5)
    assert_array_equal(dip_check.nfree, dip_xfit.nfree)
    assert_allclose(dip_check.khi2, dip_xfit.khi2, rtol=0.02)
    assert set(dip_check.conf.keys()) == set(dip_xfit.conf.keys())
    for key in sorted(dip_check.conf.keys()):
        assert_allclose(dip_check.conf[key], dip_xfit.conf[key], rtol=0.15, err_msg=key)
```

## Next Steps


---

*Source: test_dipole.py:504 | Complexity: Advanced | Last updated: 2026-05-18*