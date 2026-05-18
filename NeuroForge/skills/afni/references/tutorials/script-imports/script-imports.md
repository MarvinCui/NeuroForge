# How To: Script Imports

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test script imports

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `pathlib`
- `sys`
- `subprocess`
- `afni_test_utils.tools`
- `pytest`

**Setup Required:**
```python
# Fixtures: data, python_interpreter
```

## Step-by-Step Guide

### Step 1: Assign binary_dir = value

```python
binary_dir = Path(shutil.which('afni')).parent
```

### Step 2: Assign py_files = list(...)

```python
py_files = list(binary_dir.glob('*.py'))
```

### Step 3: Assign possible_pymods = value

```python
possible_pymods = [f for f in py_files if not f.name[0] in '@ 1 2 3'.split()]
```

### Step 4: Assign known_py2 = value

```python
known_py2 = ['afni_restproc.py', 'afni_skeleton.py', 'afni_xmat.py', 'eg_main_chrono.py', 'fat_mat_sel.py', 'fat_mvm_gridconv.py', 'fat_mvm_prep.py', 'fat_mvm_review.py', 'fat_mvm_scripter.py', 'fat_roi_row.py', 'gui_uber_skel.py', 'gui_xmat.py', 'lib_dti_sundry.py', 'lib_fat_funcs.py', 'lib_fat_plot_sel.py', 'lib_surf_clustsim.py', 'lib_uber_align.py', 'lib_uber_skel.py', 'lpc_align.py', 'make_pq_script.py', 'make_stim_times.py', 'meica.py', 'neuro_deconvolve.py', 'parse_fs_lt_log.py', 'python_module_test.py', 'quick.alpha.vals.py', 'read_matlab_files.py', 'RetroTS.py', 'slow_surf_clustsim.py', 'uber_align_test.py', 'uber_proc.py', 'uber_skel.py', 'ui_xmat.py', 'unWarpEPI.py', 'xmat_tool.py', 'gui_uber_ttest.py', 'gui_uber_align_test.py', 'lib_qt_gui.py', 'gui_uber_subj.py', 'demoExpt.py', 'gui_xmat.py', 'lib_matplot.py', 'lib_RR_plot.py', 'lib_wx.py']
```

### Step 5: Assign not_importable = value

```python
not_importable = ['abids_json_tool.py', 'ClustExp_HistTable.py', 'quick.alpha.vals.py', 'abids_json_info.py', 'tedana_wrapper.py', 'BayesianGroupAna.py', 'abids_tool.py', 'ClustExp_StatParse.py']
```

### Step 6: Assign other_problems = value

```python
other_problems = ['lib_fat_Rfactor.py', 'fat_lat_csv.py']
```

### Step 7: Assign broken_imports = value

```python
broken_imports = {}
```

### Step 8: Call pytest.xfail()

```python
pytest.xfail('Not all modules are python3 compatible')
```

### Step 9: Call print()

```python
print(script)
```

### Step 10: Assign module_name = value

```python
module_name = script.stem
```

### Step 11: Assign failed_scripts = unknown.join(...)

```python
failed_scripts = ', '.join([p for p in broken_imports.keys()])
```

### Step 12: Call run_cmd()

```python
run_cmd(data, "%s -c 'import %s'" % (python_interpreter, module_name), workdir=binary_dir)
```

### Step 13: Assign unknown = e

```python
broken_imports[script.name] = e
```


## Complete Example

```python
# Setup
# Fixtures: data, python_interpreter

# Workflow
if python_interpreter == 'python3':
    pytest.xfail('Not all modules are python3 compatible')
binary_dir = Path(shutil.which('afni')).parent
py_files = list(binary_dir.glob('*.py'))
possible_pymods = [f for f in py_files if not f.name[0] in '@ 1 2 3'.split()]
known_py2 = ['afni_restproc.py', 'afni_skeleton.py', 'afni_xmat.py', 'eg_main_chrono.py', 'fat_mat_sel.py', 'fat_mvm_gridconv.py', 'fat_mvm_prep.py', 'fat_mvm_review.py', 'fat_mvm_scripter.py', 'fat_roi_row.py', 'gui_uber_skel.py', 'gui_xmat.py', 'lib_dti_sundry.py', 'lib_fat_funcs.py', 'lib_fat_plot_sel.py', 'lib_surf_clustsim.py', 'lib_uber_align.py', 'lib_uber_skel.py', 'lpc_align.py', 'make_pq_script.py', 'make_stim_times.py', 'meica.py', 'neuro_deconvolve.py', 'parse_fs_lt_log.py', 'python_module_test.py', 'quick.alpha.vals.py', 'read_matlab_files.py', 'RetroTS.py', 'slow_surf_clustsim.py', 'uber_align_test.py', 'uber_proc.py', 'uber_skel.py', 'ui_xmat.py', 'unWarpEPI.py', 'xmat_tool.py', 'gui_uber_ttest.py', 'gui_uber_align_test.py', 'lib_qt_gui.py', 'gui_uber_subj.py', 'demoExpt.py', 'gui_xmat.py', 'lib_matplot.py', 'lib_RR_plot.py', 'lib_wx.py']
not_importable = ['abids_json_tool.py', 'ClustExp_HistTable.py', 'quick.alpha.vals.py', 'abids_json_info.py', 'tedana_wrapper.py', 'BayesianGroupAna.py', 'abids_tool.py', 'ClustExp_StatParse.py']
other_problems = ['lib_fat_Rfactor.py', 'fat_lat_csv.py']
broken_imports = {}
for script in possible_pymods:
    if script.name in other_problems + not_importable:
        continue
    print(script)
    module_name = script.stem
    try:
        run_cmd(data, "%s -c 'import %s'" % (python_interpreter, module_name), workdir=binary_dir)
    except subprocess.CalledProcessError as e:
        broken_imports[script.name] = e
if broken_imports:
    failed_scripts = ', '.join([p for p in broken_imports.keys()])
    raise ValueError('The following scripts could not be imported: %s' % failed_scripts)
```

## Next Steps


---

*Source: test_python_imports.py:18 | Complexity: Advanced | Last updated: 2026-05-18*