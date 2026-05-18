---
name: nipype
description: Local codebase analysis for nipype
doc_version: 
---

# nipype Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `nipype`
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

- **Strategy**: 18 instances

*Total: 18 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Instantiate dict: test DenoiseImage inputs** (complexity: 1.00)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='-d %d'), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='-i %s', extensions=None, mandatory=True), noise_image=dict(extensions=None, hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_noise'), noise_model=dict(argstr='-n %s', usedefault=True), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='-o %s', extensions=None, hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_noise_corrected'), save_noise=dict(mandatory=True, usedefault=True, xor=['noise_image']), shrink_factor=dict(argstr='-s %s', usedefault=True), verbose=dict(argstr='-v'))
```

**Instantiate dict: test Cortex inputs** (complexity: 1.00)

```python
input_map = dict(args=dict(argstr='%s'), computeGCBoundary=dict(argstr='-g'), computeWGBoundary=dict(argstr='-w', usedefault=True), environ=dict(nohash=True, usedefault=True), includeAllSubcorticalAreas=dict(argstr='-a', usedefault=True), inputHemisphereLabelFile=dict(argstr='-h %s', extensions=None, mandatory=True), inputTissueFractionFile=dict(argstr='-f %s', extensions=None, mandatory=True), outputCerebrumMask=dict(argstr='-o %s', extensions=None, genfile=True), timer=dict(argstr='--timer'), tissueFractionThreshold=dict(argstr='-p %f', usedefault=True), verbosity=dict(argstr='-v %d'))
```

**Instantiate dict: test CFFConverter inputs** (complexity: 1.00)

```python
input_map = dict(creator=dict(), data_files=dict(), description=dict(usedefault=True), email=dict(), gifti_labels=dict(), gifti_surfaces=dict(), gpickled_networks=dict(), graphml_networks=dict(), license=dict(), nifti_volumes=dict(), out_file=dict(extensions=None, usedefault=True), publisher=dict(), references=dict(), relation=dict(), rights=dict(), script_files=dict(), species=dict(usedefault=True), timeseries_files=dict(), title=dict(), tract_files=dict())
```

**Instantiate dict: test TensorMetrics inputs** (complexity: 1.00)

```python
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), component=dict(argstr='-num %s', sep=',', usedefault=True), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), in_mask=dict(argstr='-mask %s', extensions=None), modulate=dict(argstr='-modulate %s'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_ad=dict(argstr='-ad %s', extensions=None), out_adc=dict(argstr='-adc %s', extensions=None), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_cl=dict(argstr='-cl %s', extensions=None), out_cp=dict(argstr='-cp %s', extensions=None), out_cs=dict(argstr='-cs %s', extensions=None), out_eval=dict(argstr='-value %s', extensions=None), out_evec=dict(argstr='-vector %s', extensions=None), out_fa=dict(argstr='-fa %s', extensions=None), out_rd=dict(argstr='-rd %s', extensions=None))
```

**Instantiate dict: test Dfs inputs** (complexity: 1.00)

```python
input_map = dict(args=dict(argstr='%s'), curvatureWeighting=dict(argstr='-w %f', usedefault=True), environ=dict(nohash=True, usedefault=True), inputShadingVolume=dict(argstr='-c %s', extensions=None), inputVolumeFile=dict(argstr='-i %s', extensions=None, mandatory=True), noNormalsFlag=dict(argstr='--nonormals'), nonZeroTessellation=dict(argstr='-nz', xor=('nonZeroTessellation', 'specialTessellation')), outputSurfaceFile=dict(argstr='-o %s', extensions=None, genfile=True), postSmoothFlag=dict(argstr='--postsmooth'), scalingPercentile=dict(argstr='-f %f'), smoothingConstant=dict(argstr='-a %f', usedefault=True), smoothingIterations=dict(argstr='-n %d', usedefault=True), specialTessellation=dict(argstr='%s', position=-1, requires=['tessellationThreshold'], xor=('nonZeroTessellation', 'specialTessellation')), tessellationThreshold=dict(argstr='%f'), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'), zeroPadFlag=dict(argstr='-z'))
```

**Instantiate dict: test CAT12Segment inputs** (complexity: 1.00)

```python
input_map = dict(affine_preprocessing=dict(field='extopts.APP', usedefault=True), affine_regularization=dict(field='opts.affreg', usedefault=True), cobra=dict(field='output.ROImenu.atlases.hammers', usedefault=True), csf_output_dartel=dict(field='output.CSF.dartel', usedefault=True), csf_output_modulated=dict(field='output.CSF.mod', usedefault=True), csf_output_native=dict(field='output.CSF.native', usedefault=True), gm_output_dartel=dict(field='output.GM.dartel', usedefault=True), gm_output_modulated=dict(field='output.GM.mod', usedefault=True), gm_output_native=dict(field='output.GM.native', usedefault=True), hammers=dict(field='output.ROImenu.atlases.cobra', usedefault=True), ignore_errors=dict(field='extopts.ignoreErrors', usedefault=True), in_files=dict(copyfile=False, field='data', mandatory=True), initial_segmentation=dict(field='extopts.spm_kamap', usedefault=True), internal_resampling_process=dict(field='extopts.restypes.optimal', maxlen=2, minlen=2, usedefault=True), jacobianwarped=dict(field='output.jacobianwarped', usedefault=True), label_dartel=dict(field='output.label.dartel', usedefault=True), label_native=dict(field='output.label.native', usedefault=True), label_warped=dict(field='output.label.warped', usedefault=True), las_dartel=dict(field='output.las.dartel', usedefault=True), las_native=dict(field='output.las.native', usedefault=True), las_warped=dict(field='output.las.warped', usedefault=True), local_adaptive_seg=dict(field='extopts.LASstr', usedefault=True), lpba40=dict(field='output.ROImenu.atlases.lpba40', usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), n_jobs=dict(field='nproc', mandatory=True, usedefault=True), neuromorphometrics=dict(field='output.ROImenu.atlases.neuromorphometrics', usedefault=True), output_labelnative=dict(field='output.labelnative', usedefault=True), own_atlas=dict(copyfile=False, field='output.ROImenu.atlases.ownatlas', mandatory=False), paths=dict(), power_spm_inhomogeneity_correction=dict(field='opts.biasacc', usedefault=True), save_bias_corrected=dict(field='output.bias.warped', usedefault=True), shooting_tpm=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='extopts.registration.shooting.shootingtpm', mandatory=False), shooting_tpm_template_1=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], mandatory=False), shooting_tpm_template_2=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], mandatory=False), shooting_tpm_template_3=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], mandatory=False), shooting_tpm_template_4=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], mandatory=False), skull_strip=dict(field='extopts.gcutstr', usedefault=True), surface_and_thickness_estimation=dict(field='surface', usedefault=True), surface_measures=dict(field='output.surf_measures', usedefault=True), tpm=dict(copyfile=False, field='tpm', mandatory=False), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), voxel_size=dict(field='extopts.vox', usedefault=True), warps=dict(field='output.warps', maxlen=2, minlen=2, usedefault=True), wm_hyper_intensity_correction=dict(field='extopts.WMHC', usedefault=True), wm_output_dartel=dict(field='output.WM.dartel', usedefault=True), wm_output_modulated=dict(field='output.WM.mod', usedefault=True), wm_output_native=dict(field='output.WM.native', usedefault=True))
```

**Instantiate dict: test CAT12Segment outputs** (complexity: 1.00)

```python
output_map = dict(bias_corrected_image=dict(extensions=None), csf_dartel_image=dict(extensions=None), csf_modulated_image=dict(extensions=None), csf_native_image=dict(extensions=None), gm_dartel_image=dict(extensions=None), gm_modulated_image=dict(extensions=None), gm_native_image=dict(extensions=None), label_files=dict(), label_roi=dict(extensions=None), label_rois=dict(extensions=None), lh_central_surface=dict(extensions=None), lh_sphere_surface=dict(extensions=None), mri_images=dict(), report=dict(extensions=None), report_files=dict(), rh_central_surface=dict(extensions=None), rh_sphere_surface=dict(extensions=None), surface_files=dict(), wm_dartel_image=dict(extensions=None), wm_modulated_image=dict(extensions=None), wm_native_image=dict(extensions=None))
```

**Instantiate dict: test VBMSegment inputs** (complexity: 1.00)

```python
input_map = dict(bias_corrected_affine=dict(field='estwrite.output.bias.affine', usedefault=True), bias_corrected_native=dict(field='estwrite.output.bias.native', usedefault=True), bias_corrected_normalized=dict(field='estwrite.output.bias.warped', usedefault=True), bias_fwhm=dict(field='estwrite.opts.biasfwhm', usedefault=True), bias_regularization=dict(field='estwrite.opts.biasreg', usedefault=True), cleanup_partitions=dict(field='estwrite.extopts.cleanup', usedefault=True), csf_dartel=dict(field='estwrite.output.CSF.dartel', usedefault=True), csf_modulated_normalized=dict(field='estwrite.output.CSF.modulated', usedefault=True), csf_native=dict(field='estwrite.output.CSF.native', usedefault=True), csf_normalized=dict(field='estwrite.output.CSF.warped', usedefault=True), dartel_template=dict(extensions=['.hdr', '.img', '.img.gz', '.nii'], field='estwrite.extopts.dartelwarp.normhigh.darteltpm'), deformation_field=dict(field='estwrite.output.warps', usedefault=True), display_results=dict(field='estwrite.extopts.print', usedefault=True), gaussians_per_class=dict(usedefault=True), gm_dartel=dict(field='estwrite.output.GM.dartel', usedefault=True), gm_modulated_normalized=dict(field='estwrite.output.GM.modulated', usedefault=True), gm_native=dict(field='estwrite.output.GM.native', usedefault=True), gm_normalized=dict(field='estwrite.output.GM.warped', usedefault=True), in_files=dict(copyfile=False, field='estwrite.data', mandatory=True), jacobian_determinant=dict(field='estwrite.jacobian.warped', usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), mrf_weighting=dict(field='estwrite.extopts.mrf', usedefault=True), paths=dict(), pve_label_dartel=dict(field='estwrite.output.label.dartel', usedefault=True), pve_label_native=dict(field='estwrite.output.label.native', usedefault=True), pve_label_normalized=dict(field='estwrite.output.label.warped', usedefault=True), sampling_distance=dict(field='estwrite.opts.samp', usedefault=True), spatial_normalization=dict(usedefault=True), tissues=dict(extensions=['.hdr', '.img', '.img.gz', '.nii'], field='estwrite.tpm'), use_mcr=dict(), use_sanlm_denoising_filter=dict(field='estwrite.extopts.sanlm', usedefault=True), use_v8struct=dict(min_ver='8', usedefault=True), warping_regularization=dict(field='estwrite.opts.warpreg', usedefault=True), wm_dartel=dict(field='estwrite.output.WM.dartel', usedefault=True), wm_modulated_normalized=dict(field='estwrite.output.WM.modulated', usedefault=True), wm_native=dict(field='estwrite.output.WM.native', usedefault=True), wm_normalized=dict(field='estwrite.output.WM.warped', usedefault=True))
```

**Instantiate dict: test LabelConfig inputs** (complexity: 1.00)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_config=dict(argstr='%s', extensions=None, position=-2), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), lut_aal=dict(argstr='-lut_aal %s', extensions=None), lut_basic=dict(argstr='-lut_basic %s', extensions=None), lut_fs=dict(argstr='-lut_freesurfer %s', extensions=None), lut_itksnap=dict(argstr='-lut_itksnap %s', extensions=None), nthreads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), spine=dict(argstr='-spine %s', extensions=None))
```

**Instantiate dict: test Retroicor inputs** (complexity: 1.00)

```python
input_map = dict(args=dict(argstr='%s'), card=dict(argstr='-card %s', extensions=None, position=-2), cardphase=dict(argstr='-cardphase %s', extensions=None, hash_files=False, position=-6), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), order=dict(argstr='-order %s', position=-5), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_file'], name_template='%s_retroicor', position=1), outputtype=dict(), resp=dict(argstr='-resp %s', extensions=None, position=-3), respphase=dict(argstr='-respphase %s', extensions=None, hash_files=False, position=-7), threshold=dict(argstr='-threshold %d', position=-4))
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 20
**Total Settings:** 283
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 20 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 42
**Categories:** 6

### Overview

- **README.rst** (`README.rst`)
- **THANKS.rst** (`THANKS.rst`)

### Workflows

- **workflow_failure.md** (`.github/workflows/workflow_failure.md`)

### Examples

- **README.md** (`examples/README.md`)

### Community

- **CODE_OF_CONDUCT.md** (`CODE_OF_CONDUCT.md`)

### Contributing

- **CONTRIBUTING.md** (`CONTRIBUTING.md`)

### Other

- **ISSUE_TEMPLATE.md** (`.github/ISSUE_TEMPLATE.md`)
- **PULL_REQUEST_TEMPLATE.md** (`.github/PULL_REQUEST_TEMPLATE.md`)
- **about.rst** (`doc/about.rst`)
- **0.X.X-changelog.rst** (`doc/changelog/0.X.X-changelog.rst`)
- **1.X.X-changelog.rst** (`doc/changelog/1.X.X-changelog.rst`)
- *...and 31 more*

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
