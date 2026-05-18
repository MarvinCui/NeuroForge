---
name: dipy
description: Local codebase analysis for dipy
doc_version: 
---

# dipy Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `dipy`
**Files Analyzed:** 0
**Languages:** 
**Analysis Depth:** surface

## When to Use This Skill

Use this skill when you need to:
- Understand the codebase architecture and design patterns
- Find implementation examples and usage patterns
- Review API documentation extracted from code
- Check configuration patterns and best practices
- Explore test examples and real-world usage
- Navigate the codebase structure efficiently

## ⚡ Quick Reference

### Codebase Statistics

**Languages:**

**Analysis Performed:**
- ✅ API Reference (C2.5)
- ✅ Dependency Graph (C2.6)
- ✅ Design Patterns (C3.1)
- ✅ Test Examples (C3.2)
- ✅ Configuration Patterns (C3.4)
- ✅ Architectural Analysis (C3.7)
- ✅ Project Documentation (C3.9)

### 🎨 Design Patterns Detected

*From C3.1 codebase analysis (confidence > 0.7)*

- **Adapter**: 1 instances

*Total: 1 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: test mcsd model delta** (complexity: 1.00)

```python
sh_order_max = 8
gtab = get_3shell_gtab()
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model = MultiShellDeconvModel(gtab, response)
iso = response.iso
theta, phi = (default_sphere.theta, default_sphere.phi)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    B = shm.real_sh_descoteaux_from_index(response.m_values, response.l_values, theta[:, None], phi[:, None])
wm_delta = model.delta.copy()
wm_delta[:iso] = 0.0
wm_delta = _expand(model.m_values, iso, wm_delta)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    for i, s in enumerate([0, 1000, 2000, 3500]):
        g = GradientTable(default_sphere.vertices * s)
        signal = model.predict(wm_delta, gtab=g)
        expected = np.dot(response.response[i, iso:], B.T)
        npt.assert_array_almost_equal(signal, expected)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    signal = model.predict(wm_delta, gtab=gtab)
fit = model.fit(signal)
m = model.m_values
npt.assert_array_almost_equal(fit.shm_coeff[m != 0], 0.0, 2)
```

**Workflow: test MultiShellDeconvModel response** (complexity: 1.00)

```python
gtab = get_3shell_gtab()
sh_order_max = 8
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model_1 = MultiShellDeconvModel(gtab, response, sh_order_max=sh_order_max)
responses = np.array([wm_response, gm_response, csf_response])
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model_2 = MultiShellDeconvModel(gtab, responses, sh_order_max=sh_order_max)
response_1 = model_1.response.response
response_2 = model_2.response.response
npt.assert_array_almost_equal(response_1, response_2, 0)
npt.assert_raises(ValueError, MultiShellDeconvModel, gtab, np.ones((4, 3, 4)))
npt.assert_raises(ValueError, MultiShellDeconvModel, gtab, np.ones((3, 3, 4)), iso=3)
```

**Workflow: test MultiShellDeconvModel** (complexity: 1.00)

```python
gtab = get_3shell_gtab()
mevals = np.array([wm_response[0, :3], wm_response[0, :3]])
angles = [(0, 0), (60, 0)]
S_wm, sticks = multi_tensor(gtab, mevals, S0=wm_response[0, 3], angles=angles, fractions=[30.0, 70.0], snr=None)
S_gm = gm_response[0, 3] * np.exp(-gtab.bvals * gm_response[0, 0])
S_csf = csf_response[0, 3] * np.exp(-gtab.bvals * csf_response[0, 0])
sh_order_max = 8
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
    model = MultiShellDeconvModel(gtab, response)
vf = [0.325, 0.2, 0.475]
signal = sum((i * j for i, j in zip(vf, [S_csf, S_gm, S_wm])))
fit = model.fit(signal)
S_pred_fit = fit.predict()
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    S_pred_model = model.predict(fit.all_shm_coeff)
npt.assert_array_almost_equal(S_pred_fit, S_pred_model, 0)
npt.assert_array_almost_equal(S_pred_fit, signal, 0)
```

**Workflow: test MSDeconvFit** (complexity: 1.00)

```python
gtab = get_3shell_gtab()
mevals = np.array([wm_response[0, :3], wm_response[0, :3]])
angles = [(0, 0), (60, 0)]
S_wm, sticks = multi_tensor(gtab, mevals, S0=wm_response[0, 3], angles=angles, fractions=[30.0, 70.0], snr=None)
S_gm = gm_response[0, 3] * np.exp(-gtab.bvals * gm_response[0, 0])
S_csf = csf_response[0, 3] * np.exp(-gtab.bvals * csf_response[0, 0])
sh_order_max = 8
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
    model = MultiShellDeconvModel(gtab, response)
vf = [0.325, 0.2, 0.475]
signal = sum((i * j for i, j in zip(vf, [S_csf, S_gm, S_wm])))
fit = model.fit(signal)
npt.assert_array_almost_equal(fit.volume_fractions, vf, 1)
```

**Workflow: test mask for response msmt nvoxels** (complexity: 1.00)

```python
gtab, data, _, _ = get_test_data(rng)
with warnings.catch_warnings(record=True) as w:
    wm_mask, gm_mask, csf_mask = mask_for_response_msmt(gtab, data, roi_center=None, roi_radii=(1, 1, 0), wm_fa_thr=0.7, gm_fa_thr=0.3, csf_fa_thr=0.15, gm_md_thr=0.001, csf_md_thr=0.0032)
npt.assert_equal(len(w), 1)
npt.assert_(issubclass(w[0].category, UserWarning))
npt.assert_('Some b-values are higher than 1200.' in str(w[0].message))
wm_nvoxels = np.sum(wm_mask)
gm_nvoxels = np.sum(gm_mask)
csf_nvoxels = np.sum(csf_mask)
npt.assert_equal(wm_nvoxels, 5)
npt.assert_equal(gm_nvoxels, 2)
npt.assert_equal(csf_nvoxels, 2)
with warnings.catch_warnings(record=True) as w:
    wm_mask, gm_mask, csf_mask = mask_for_response_msmt(gtab, data, roi_center=None, roi_radii=(1, 1, 0), wm_fa_thr=1, gm_fa_thr=0, csf_fa_thr=0, gm_md_thr=0, csf_md_thr=0)
    npt.assert_equal(len(w), 6)
    npt.assert_(issubclass(w[0].category, UserWarning))
    npt.assert_('Some b-values are higher than 1200.' in str(w[0].message))
    npt.assert_('No voxel with a FA higher than 1 were found' in str(w[1].message))
    npt.assert_('No voxel with a FA lower than 0 were found' in str(w[2].message))
    npt.assert_('No voxel with a MD lower than 0 were found' in str(w[3].message))
    npt.assert_('No voxel with a FA lower than 0 were found' in str(w[4].message))
    npt.assert_('No voxel with a MD lower than 0 were found' in str(w[5].message))
wm_nvoxels = np.sum(wm_mask)
gm_nvoxels = np.sum(gm_mask)
csf_nvoxels = np.sum(csf_mask)
npt.assert_equal(wm_nvoxels, 0)
npt.assert_equal(gm_nvoxels, 0)
npt.assert_equal(csf_nvoxels, 0)
```

**Workflow: test classify** (complexity: 1.00)

```python
imgseg = TissueClassifierHMRF()
nclasses = 4
beta = 0.1
tolerance = 0.0001
max_iter = 10
image = create_image()
npt.assert_(image.max() == 1.0)
npt.assert_(image.min() == 0.0)
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta, tolerance=tolerance)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta, max_iter=max_iter)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
masked_image = np.copy(image)
masked_image[masked_image.shape[0] // 2:, :, :] = 0
seg_init, seg_final, PVE = imgseg.classify(masked_image, nclasses, beta)
npt.assert_(seg_init.max() == nclasses)
npt.assert_(seg_init.min() == 0.0)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
npt.assert_(PVE.shape[-1] == nclasses)
imgseg = TissueClassifierHMRF(save_history=True)
seg_init, seg_final, PVE = imgseg.classify(200 * image, nclasses, beta, tolerance=tolerance)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
npt.assert_(imgseg.energies_sum[0] > imgseg.energies_sum[-1])
```

**Workflow: test msdki predict** (complexity: 1.00)

```python
dkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
pred = dkiM.predict(params_single, S0=100)
assert_array_almost_equal(pred, signal_sph)
pred = dkiM.predict(params_multi, S0=100)
assert_array_almost_equal(pred[:, :, 0, :], DWI[:, :, 0, :])
dkiF = dkiM.fit(signal_sph)
pred_single = dkiF.predict(gtab_3s, S0=100)
assert_array_almost_equal(pred_single, signal_sph)
dkiF = dkiM.fit(DWI)
pred_multi = dkiF.predict(gtab_3s, S0=100)
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
dkiF = dkiM.fit(signal_sph)
pred_single = dkiF.predict(gtab_3s)
assert_array_almost_equal(100 * pred_single, signal_sph)
dkiF = dkiM.fit(DWI)
pred_multi = dkiF.predict(gtab_3s)
assert_array_almost_equal(100 * pred_multi[:, :, 0, :], DWI[:, :, 0, :])
dkiF = dkiM.fit(DWI)
pred_multi = dkiF.predict(gtab_3s, S0=100 * np.ones(DWI.shape[:-1]))
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```

**Workflow: test errors** (complexity: 1.00)

```python
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab)
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab_3s, min_signal=-1)
mask_wrong = np.ones((2, 3, 1))
msdki_model = msdki.MeanDiffusionKurtosisModel(gtab_3s)
assert_raises(ValueError, msdki_model.fit, DWI, mask=mask_wrong)

def aux_test_fun(ob, ind):
    met = ob[ind].msk
    return met
mdkiF = msdki_model.fit(DWI)
assert_raises(IndexError, aux_test_fun, mdkiF, (0, 0, 0, 0))
met = aux_test_fun(mdkiF, (0, 0, 0))
assert_array_almost_equal(MKgt_multi[0, 0, 0], met)
assert_raises(ValueError, awf_from_msk, MKgt_multi, mask=mask_wrong)
```

**Workflow: test kurtosis to smt2 conversion** (complexity: 1.00)

```python
awf0 = 0
kexp0 = 0
kest0 = msk_from_awf(awf0)
assert_almost_equal(kest0, kexp0)
awf1 = 1
kexp1 = 2.4
kest1 = msk_from_awf(awf1)
assert_almost_equal(kest1, kexp1)
awf_test_array = np.linspace(0, 1, 100)
k_exp = msk_from_awf(awf_test_array)
awf_from_k = awf_from_msk(k_exp)
assert_array_almost_equal(awf_from_k, awf_test_array)
assert_array_almost_equal(awf_from_msk(np.array([-0.1, 2.5])), np.array([0.0, 1.0]))
assert_(np.isnan(awf_from_msk(np.array(np.nan))))
```

**Workflow: test smt2 metrics** (complexity: 1.00)

```python
AWFgt = awf_from_msk(MKgt_multi)
DIgt = 3 * MDgt_multi / (1 + 2 * (1 - AWFgt) ** 2)
RDe = DIgt * (1 - AWFgt)
VarD = 2 / 9 * (AWFgt * DIgt ** 2 + (1 - AWFgt) * (DIgt - RDe) ** 2)
MD = (AWFgt * DIgt + (1 - AWFgt) * (DIgt + 2 * RDe)) / 3
uFAgt = np.sqrt(3 / 2 * VarD[MD > 0] / (VarD[MD > 0] + MD[MD > 0] ** 2))
mdkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
mdkiF = mdkiM.fit(DWI)
assert_array_almost_equal(mdkiF.smt2f, AWFgt)
assert_array_almost_equal(mdkiF.smt2di, DIgt)
assert_array_almost_equal(mdkiF.smt2uFA[MD > 0], uFAgt)
mask = MKgt_multi > 0
AWF = awf_from_msk(MKgt_multi, mask=mask)
assert_array_almost_equal(AWF, AWFgt)
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 31
**Total Settings:** 529
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 31 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 97
**Categories:** 4

### Overview

- **README.rst** (`README.rst`)

### Guides

- **bibliography.rst** (`doc/user_guide/bibliography.rst`)
- **data.rst** (`doc/user_guide/data.rst`)
- **dataset_list.rst** (`doc/user_guide/dataset_list.rst`)
- **dependencies.rst** (`doc/user_guide/dependencies.rst`)
- **getting_started.rst** (`doc/user_guide/getting_started.rst`)
- *...and 4 more*

### Examples

- **README.md** (`doc/examples/README.md`)

### Other

- **CODE_OF_CONDUCT.md** (`.github/CODE_OF_CONDUCT.md`)
- **CONTRIBUTING.md** (`.github/CONTRIBUTING.md`)
- **ISSUE_TEMPLATE.md** (`.github/ISSUE_TEMPLATE.md`)
- **PULL_REQUEST_TEMPLATE.md** (`.github/PULL_REQUEST_TEMPLATE.md`)
- **README.rst** (`benchmarks/README.rst`)
- *...and 81 more*

*See `references/documentation/` for all project documentation*

## 📚 Available References

This skill includes detailed reference documentation:

- **Dependencies**: `references/dependencies/` - Dependency graph and analysis
- **Patterns**: `references/patterns/` - Detected design patterns
- **Examples**: `references/test_examples/` - Usage examples from tests
- **Configuration**: `references/config_patterns/` - Configuration patterns
- **Documentation**: `references/documentation/` - Project documentation

---

**Generated by Skill Seeker** | Codebase Analyzer with C3.x Analysis
