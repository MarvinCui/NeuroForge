# How To: Filmgls

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test filmgls

## Prerequisites

**Required Modules:**
- `nipype.interfaces.fsl.model`


## Step-by-Step Guide

### Step 1: Assign input_map2 = dict(...)

```python
input_map2 = dict(args=dict(argstr='%s'), autocorr_estimate_only=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--ac'), autocorr_noestimate=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--noest'), brightness_threshold=dict(argstr='--epith=%d'), design_file=dict(argstr='--pd=%s'), environ=dict(usedefault=True), fit_armodel=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--ar'), full_data=dict(argstr='-v'), in_file=dict(mandatory=True, argstr='--in=%s'), mask_size=dict(argstr='--ms=%d'), multitaper_product=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--mt=%d'), output_pwdata=dict(argstr='--outputPWdata'), output_type=dict(), results_dir=dict(argstr='--rn=%s', usedefault=True), smooth_autocorr=dict(argstr='--sa'), threshold=dict(usedefault=True, argstr='--thr=%f'), tukey_window=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--tukey=%d'), use_pava=dict(argstr='--pava'))
```


## Complete Example

```python
# Workflow
input_map2 = dict(args=dict(argstr='%s'), autocorr_estimate_only=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--ac'), autocorr_noestimate=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--noest'), brightness_threshold=dict(argstr='--epith=%d'), design_file=dict(argstr='--pd=%s'), environ=dict(usedefault=True), fit_armodel=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--ar'), full_data=dict(argstr='-v'), in_file=dict(mandatory=True, argstr='--in=%s'), mask_size=dict(argstr='--ms=%d'), multitaper_product=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--mt=%d'), output_pwdata=dict(argstr='--outputPWdata'), output_type=dict(), results_dir=dict(argstr='--rn=%s', usedefault=True), smooth_autocorr=dict(argstr='--sa'), threshold=dict(usedefault=True, argstr='--thr=%f'), tukey_window=dict(xor=['autocorr_estimate_only', 'fit_armodel', 'tukey_window', 'multitaper_product', 'use_pava', 'autocorr_noestimate'], argstr='--tukey=%d'), use_pava=dict(argstr='--pava'))
```

## Next Steps


---

*Source: test_FILMGLS.py:75 | Complexity: Beginner | Last updated: 2026-05-18*